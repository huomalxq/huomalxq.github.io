# GSM8K 后训练实验复盘：LoRA SFT、DPO 与 GRPO

来源：本地 `GSM8K_MAIN_EXPERIMENT_REPORT.md`

## 实验目标

这组实验围绕 GSM8K 数学推理任务展开，核心问题是：在有限显存和训练成本下，如何通过后训练提升小尺寸模型的数学推理能力。

实验主线可以拆成四步：

1. 先评估多个候选模型在 GSM8K 上的基础能力。
2. 根据基础能力和训练成本选择主实验模型。
3. 对主模型做 LoRA SFT，观察不同 checkpoint 的效果变化。
4. 在 SFT 之外继续尝试 DPO 和 GRPO，比较偏好对齐与 reward-based RL 的收益。

除非特别说明，评估设置如下：

| 配置 | 取值 |
| --- | --- |
| Dataset | GSM8K test |
| Subset | random 500 samples |
| Seed | 42 |
| Decoding | greedy |
| Metric | final numeric answer exact match |
| eval batch size | 16 |
| max new tokens | 512 |

答案抽取规则是优先抽取模型输出中 `####` 后面的最终数字；如果没有 `####`，则抽取输出文本中的最后一个数字。

## 候选模型评估

第一阶段不是训练，而是判断不同模型在 GSM8K 上的初始能力。评估覆盖 Qwen2.5 和 Llama 系列，并比较 zero-shot 与 3-shot。

| Model | Type | 0-shot Acc | 3-shot Acc | Best |
| --- | --- | ---: | ---: | ---: |
| Qwen2.5-0.5B | Base | 0.262 | 0.124 | 0.262 |
| Qwen2.5-0.5B-Instruct | Instruct | 0.416 | 0.398 | 0.416 |
| Qwen2.5-1.5B | Base | 0.200 | 0.186 | 0.200 |
| Qwen2.5-1.5B-Instruct | Instruct | 0.650 | 0.602 | 0.650 |
| Qwen2.5-7B | Base | 0.808 | 0.098 | 0.808 |
| Qwen2.5-7B-Instruct | Instruct | 0.838 | 0.904 | 0.904 |
| Llama-3.1-8B | Base | 0.020 | 0.068 | 0.068 |
| Llama-3.1-8B-Instruct | Instruct | 0.864 | 0.810 | 0.864 |
| Llama-3.2-1B | Base | 0.030 | 0.028 | 0.030 |
| Llama-3.2-1B-Instruct | Instruct | 0.192 | 0.312 | 0.312 |

从结果看，Instruct 模型普遍明显强于 base 模型。Qwen2.5-7B-Instruct 和 Llama-3.1-8B-Instruct 的基础能力很强，但训练成本更高，且提升空间不容易体现。

最后主线选择 `Qwen2.5-1.5B` 作为 SFT 对象。它不是最强模型，但有三个优势：

- 原始 base 能力较弱，0-shot 只有 `100/500 = 0.200`。
- 同尺寸 Instruct 版本可以达到 `325/500 = 0.650`，说明 1.5B 规模本身有潜力。
- 两张 V100 32G 可以承受 LoRA SFT、DPO 和 GRPO 实验，成本更适合持续迭代。

## LoRA SFT 实验

SFT 前的主基线是 `Qwen2.5-1.5B` base，而不是 Instruct 版本。同尺寸 `Qwen2.5-1.5B-Instruct` 只作为参考线。

| Model | Setting | Correct | Accuracy |
| --- | --- | ---: | ---: |
| Qwen2.5-1.5B | 0-shot | 100/500 | 0.200 |
| Qwen2.5-1.5B | 3-shot | 93/500 | 0.186 |
| Qwen2.5-1.5B-Instruct | 0-shot | 325/500 | 0.650 |
| Qwen2.5-1.5B-Instruct | 3-shot | 301/500 | 0.602 |

SFT checkpoint 的观察重点有两个：

- 相比 base 0.200 提升了多少。
- 距离同尺寸 Instruct reference 0.650 还有多远。

### SFT 结果

| Run | Best Checkpoint | Correct | Accuracy | Delta vs Base | Delta vs Instruct Ref |
| --- | ---: | ---: | ---: | ---: | ---: |
| SFT 1 epoch, save_steps=50 | 50 | 321/500 | 0.642 | +0.442 | -0.008 |
| SFT 2 epochs | 100 | 307/500 | 0.614 | +0.414 | -0.036 |
| Light SFT | 100 | 318/500 | 0.636 | +0.436 | -0.014 |

SFT 1 epoch 的 checkpoint-50 是最好结果，把 Qwen2.5-1.5B base 从 0.200 拉到 0.642，几乎追平同尺寸 Instruct 模型的 0.650。

但这个结果也暴露了一个很重要的问题：继续训练没有继续提升，后续 checkpoint 反而下降。SFT 在这里更像是“格式和任务能力注入”，最佳点很早出现，训练过久会损失泛化。

因此，SFT 的结论不是“训得越久越好”，而是：

```text
轻量 SFT 有效，但必须早停。
如果继续追求 GSM8K accuracy，应该转向 reward-based RL，例如 GRPO。
```

## DPO 实验

DPO 使用 base model 在 GSM8K train split 上生成答案，再构造 preference pair。

构造逻辑如下：

```text
如果 base model 生成错误：
  chosen = GSM8K gold answer
  rejected = base model wrong completion
```

关键数据：

| 项目 | 数值 |
| --- | ---: |
| train generations | 3000 |
| base train generation accuracy | 2272/3000 = 0.7573 |
| preference pairs | 728 |
| beta | 0.1 |
| max steps | 300 |
| LoRA rank / alpha | 8 / 16 |

测试结果：

| Model / Method | Correct | Accuracy | Delta vs Instruct Ref |
| --- | ---: | ---: | ---: |
| Qwen2.5-1.5B-Instruct reference | 325/500 | 0.650 | 0 |
| DPO checkpoint-100 | 308/500 | 0.616 | -0.034 |
| DPO final / checkpoint-300 | 289/500 | 0.578 | -0.072 |

DPO 没有提升 GSM8K accuracy。checkpoint-100 比 final 更好，说明继续训练后出现明显过拟合或偏移。

这里的关键问题可能不是 DPO 方法本身，而是自动构造的 preference pair 质量不足。只用“base 错误答案 vs gold answer”构造偏好对，可能缺少高质量 reasoning trajectory，也容易让模型学到格式或答案片段，而不是稳定的推理策略。

## GRPO 实验

GRPO 使用最终答案正确性作为主要 reward，并加入轻量格式奖励。

| Case | Reward |
| --- | ---: |
| 答案正确且格式正确 | 1.1 |
| 答案正确但格式不完整 | 1.0 |
| 答案错误但格式正确 | 0.1 |
| 答案错误且格式错误 | 0.0 |

### GRPO 结果

| Model / Method | Correct | Accuracy | Delta vs Instruct Ref |
| --- | ---: | ---: | ---: |
| Qwen2.5-1.5B-Instruct reference | 325/500 | 0.650 | 0 |
| GRPO from Light SFT100, 100 steps | 322/500 | 0.644 | -0.006 |
| GRPO from Base, 100 steps | 326/500 | 0.652 | +0.002 |
| GRPO from Base, strong 300 steps | 344/500 | 0.688 | +0.038 |

strong 300 steps 是当前最佳结果，把 accuracy 从 reference 的 0.650 提升到 0.688，提升 `19/500`，也就是 `+3.8` 个百分点。

这组实验说明，对 GSM8K 这种最终答案可验证的任务，reward-based RL 比当前 DPO 构造方式更直接有效。只要 reward 设计能稳定判断最终答案，GRPO 可以通过采样和组内比较推动模型朝正确答案分布移动。

## 主线结果排序

| Rank | Method | Correct | Accuracy | Note |
| ---: | --- | ---: | ---: | --- |
| 1 | GRPO from Base, strong 300 steps | 344/500 | 0.688 | 当前最佳 |
| 2 | GRPO from Base, 100 steps | 326/500 | 0.652 | 基本持平 instruct reference |
| 3 | Qwen2.5-1.5B-Instruct reference | 325/500 | 0.650 | 同尺寸 instruct 参考线 |
| 4 | GRPO from Light SFT100 | 322/500 | 0.644 | 接近 instruct reference |
| 5 | SFT e1 checkpoint-50 | 321/500 | 0.642 | 最好 SFT |
| 6 | Light SFT checkpoint-100 | 318/500 | 0.636 | 轻 SFT 最好结果 |
| 7 | DPO checkpoint-100 | 308/500 | 0.616 | 低于 instruct reference |
| 8 | SFT e2 checkpoint-100 | 307/500 | 0.614 | 二轮 SFT 最好结果 |
| 9 | DPO final / checkpoint-300 | 289/500 | 0.578 | 明显掉点 |

## 关键参数理解

SFT 使用的 LoRA 参数：

| Parameter | Value | Meaning |
| --- | --- | --- |
| `r` / `lora_rank` | 16 | LoRA 低秩矩阵的秩 |
| `lora_alpha` | 32 | LoRA 缩放系数 |
| `alpha / r` | 2 | 实际 LoRA 更新缩放比例 |
| `lora_dropout` | 0.05 | 降低过拟合 |
| `target_modules` | q/k/v/o/gate/up/down | attention 和 MLP 主要线性层都加 LoRA |

这个设置覆盖 attention 与 MLP，容量比较强，所以能快速把 base 拉到接近 Instruct reference。但容量强也意味着更容易过拟合，解释了 checkpoint-50 最好、后续继续下降的现象。

GRPO strong 300 steps 的训练规模可以这样估算：

```text
global prompt batch = 2 * 2 GPUs * 2 = 8 prompts / step
num_generations = 4
completions per step = 8 * 4 = 32
max_steps = 300
total generated completions ~= 9600
```

相比 100 steps，300 steps 产生了更充分的采样和 reward 信号，因此最终超过了 Instruct reference。

## 经验总结

- 模型选择不一定选最强模型，而要选“有提升空间、训练成本可控、能体现实验变量”的模型。
- SFT 对 base model 的格式学习和任务适配非常有效，但需要早停。
- DPO 的效果高度依赖 preference pair 质量，自动构造的粗糙偏好对可能会把模型推偏。
- 对 GSM8K 这种答案可验证任务，GRPO 的 reward 设计更直接，strong 300 steps 当前收益最好。
- 实验记录不能只看最终 accuracy，也要看 checkpoint 曲线，否则很容易错过早期最佳点。

## 后续计划

- 继续评估 GRPO 300 / 400 / 500 steps 的 checkpoint 曲线。
- 对最佳 GRPO checkpoint 评估 full GSM8K test，而不仅是 random 500 subset。
- 若继续 SFT，只做轻量格式冷启动，不再长时间训练。
- 若继续 DPO，重新设计更高质量的 reasoning preference pair。

## 简历与面试表达

简历版：

> 基于 GSM8K 构建 Qwen2.5-1.5B 后训练实验流程，系统对比 base / instruct 模型、LoRA SFT、DPO 与 GRPO。使用 random 500 test subset、greedy decoding 和 final numeric exact match 进行统一评估。LoRA SFT 将 Qwen2.5-1.5B base 从 0.200 提升至 0.642，接近同尺寸 Instruct reference 0.650；进一步分析 checkpoint 曲线发现 SFT 需要早停。DPO 基于自动构造 preference pairs 训练后未带来提升，而 GRPO strong 300 steps 将 accuracy 提升至 0.688，较 Instruct reference 提升 3.8 个百分点。

一分钟表达：

> 我做过一组 GSM8K 后训练实验，目标是在有限显存下比较 SFT、DPO 和 GRPO 对小模型数学推理能力的提升。前期先评估 Qwen2.5 和 Llama 多个 base / instruct 模型，最后选择 Qwen2.5-1.5B，因为它的 base 只有 0.200，但同尺寸 instruct 有 0.650，说明模型规模有潜力且提升空间明显。SFT 阶段用 LoRA 把 base 提升到 0.642，但后续 checkpoint 掉点，说明需要早停。DPO 用自动构造的 preference pair 效果不好，最终低于 reference。GRPO 使用最终答案正确性 reward，strong 300 steps 达到 0.688，是当前最佳结果，也说明对答案可验证的数学任务，reward-based RL 更直接有效。
