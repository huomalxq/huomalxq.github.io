# GPU 物理架构、内存层级与核心硬件单元总结

来源：[Datawhale LLM-Algo-LeetCode：GPU Architecture and Memory](https://datawhalechina.github.io/llm-algo-leetcode/01_Hardware_Math_and_Systems/03_GPU_Architecture_and_Memory.html)

## 核心结论

大模型计算性能不只取决于算力峰值，还取决于数据能不能足够快地喂给计算单元。Transformer 中的 GEMM、Attention、MLP 等计算既可能受算力限制，也可能受显存带宽限制。

理解 GPU 架构时，可以抓住三条主线：

- Tensor Core 负责把矩阵乘法跑快。
- HBM、L2、SRAM、寄存器决定数据搬运成本。
- NVLink、NVSwitch、PCIe 决定多卡通信上限。

高性能 CUDA/Triton 算子的本质，就是把计算映射到 Tensor Core，并尽量减少慢速 HBM 的读写。

## 1. NVIDIA GPU 架构演进

NVIDIA 从 V100 到 H100、Blackwell 的演进，核心围绕两件事：更强的低精度矩阵计算能力，以及更高的内存和互连带宽。

| 架构 | 代表 GPU | 关键变化 | 对大模型的意义 |
| --- | --- | --- | --- |
| Volta | V100 | 首次引入 Tensor Core，支持 FP16 混合精度矩阵乘加 | 深度学习矩阵计算进入 Tensor Core 时代 |
| Ampere | A100 | 支持 TF32、BF16，更高 HBM 带宽，更大 L2 Cache，引入 MIG、稀疏 Tensor Core | 成为大模型训练的工业标配 |
| Hopper | H100 | 原生 FP8、Transformer Engine、Thread Block Cluster、TMA | 针对 Transformer 训练和推理继续降低精度、提高吞吐 |
| Blackwell | B100/B200 | 第二代 Transformer Engine，支持 FP4，更强 NVLink | 面向生成式 AI 和万亿参数模型集群优化 |

可以把这条路线理解成：

```text
FP16 Tensor Core -> BF16/TF32 -> FP8 Transformer Engine -> FP4 与更强互连
```

每一代都在降低有效计算精度、提高矩阵吞吐，并同步增强显存带宽和多卡通信能力。

## 2. Tensor Core 与 CUDA Core 的区别

普通 CUDA Core 更像标量计算单元，适合执行单个数值的乘加：

```text
d = a * b + c
```

Tensor Core 是为矩阵乘法设计的硬件单元，执行的是矩阵乘加：

```text
D = A * B + C
```

对 Transformer 来说，Attention 的 QK 矩阵乘、Softmax 后乘 V、MLP 中的线性层，主体都是大规模 GEMM。因此只要数据格式、矩阵形状和布局能让运算落到 Tensor Core 上，吞吐就会远高于普通 CUDA Core。

Tensor Core 的常见特点：

- 使用 FP16、BF16、FP8 等低精度格式做乘法。
- 用更高精度累加器保留结果稳定性，例如 FP32 accumulate。
- 对密集矩阵乘法非常友好。
- 性能提升通常来自硬件专用矩阵路径，而不是普通标量并行。

面试里可以这样回答：

> CUDA Core 主要做标量 FMA，Tensor Core 直接做矩阵 MMA。Transformer 里大部分计算都是 GEMM，所以 Tensor Core 能把低精度矩阵乘法吞吐拉到非常高，是现代大模型训练和推理的核心硬件单元。

## 3. GPU 内存层级

GPU 内存层级可以看成金字塔：越靠近计算单元，速度越快、容量越小；越远离计算单元，容量越大、访问越慢。

| 层级 | 位置/范围 | 特点 | 风险或用途 |
| --- | --- | --- | --- |
| Registers | 每个线程私有 | 最快，容量极小 | 变量过多会发生 register spilling |
| Shared Memory / SRAM | 每个 SM 内部，Block 内线程共享 | 很快，容量通常只有几百 KB | 高性能算子做 tiling 和线程协作的关键 |
| L2 Cache | 所有 SM 共享 | 容量几十 MB，缓存 HBM 读写 | 缓解重复访问 HBM 的成本 |
| HBM / Global Memory | GPU 全局显存 | 容量大，带宽高但相对片上存储慢 | 模型权重、KV Cache、激活值主要放在这里 |

关键理解：

- 寄存器和 SRAM 是片上资源，离计算单元近，但容量紧张。
- HBM 容量大，适合放大模型权重和中间状态，但访问代价高。
- 算子性能常常不是算不过来，而是数据搬不够快。

如果每个小操作都频繁读写 HBM，就会出现 Memory Bound。PyTorch 中多个算子分开执行时，常常会把中间结果写回 HBM，再被下一个算子读出，带来大量访存开销。

## 4. 为什么大模型推理常常是 Memory Bound

大模型推理时，尤其是 decode 阶段，每一步只生成一个或少量 token。此时计算量不一定很大，但每一步都要读取大量模型权重和 KV Cache。

可以粗略理解为：

```text
算力足够，但权重和 KV Cache 从 HBM 搬到计算单元的速度不够快
```

典型 Memory Bound 现象：

- GPU 利用率不高，但显存带宽接近瓶颈。
- Batch 很小时，矩阵乘法规模不够大，Tensor Core 吃不满。
- KV Cache 随上下文长度增长，占用显存并增加读写压力。
- 多个小算子反复读写 HBM，中间结果搬运成本超过计算本身。

优化方向通常包括：

- 算子融合，减少中间结果写回 HBM。
- Tiling，把小块数据放入 SRAM 复用。
- 量化，减少权重和 KV Cache 的字节数。
- 使用 FlashAttention、PagedAttention 等内存友好的算法。

## 5. FlashAttention 如何利用 SRAM

标准 Attention 会先计算：

```text
S = QK^T
```

如果序列长度是 `N`，中间注意力矩阵 `S` 的规模是 `N × N`。传统实现会把 `S` 写回 HBM，再读出来做 Softmax，然后再写回 HBM，最后再读出来和 `V` 相乘。这会产生巨大的 `O(N^2)` HBM 读写。

FlashAttention 的核心不是减少数学计算量，而是减少 HBM 访存：

1. 将 Q、K、V 切成 block。
2. 每次只把能放进 SRAM 的小块加载到片上内存。
3. 在 SRAM 内计算局部 `QK^T`。
4. 用 Online Softmax 在块内维护最大值和归一化项，避免保存完整注意力矩阵。
5. 直接和对应的 V block 相乘，只把最终输出写回 HBM。

结果是：

```text
传统 Attention：频繁读写 O(N^2) 中间矩阵
FlashAttention：主要读写 Q/K/V/O，避免落地完整注意力矩阵
```

所以 FlashAttention 的本质是 I/O-aware Attention：它利用 SRAM 做 tiling 和 fusion，把访存瓶颈从 HBM 转移到片上高速存储。

## 6. PCIe、NVLink 与 NVSwitch

单卡装不下模型或需要提升吞吐时，就会进入多卡训练和推理。此时瓶颈可能从计算和显存，转移到 GPU 之间的通信。

| 连接方式 | 特点 | 影响 |
| --- | --- | --- |
| PCIe | 通用总线，带宽较低，可能经过 PCIe Switch 或 CPU | 多卡通信延迟高、带宽低 |
| NVLink | NVIDIA GPU-to-GPU 高速互连 | 节点内 GPU 通信带宽显著高于 PCIe |
| NVSwitch | 让节点内多张 GPU 接近全互连 | 更适合 All-Reduce、All-Gather 等集合通信 |

对于张量并行、流水线并行、ZeRO、MoE 等场景，通信拓扑会直接影响训练效率。

例如：

- Tensor Parallel 常依赖频繁 All-Reduce。
- ZeRO 会产生参数、梯度、优化器状态的分片通信。
- MoE 可能带来 All-to-All token dispatch。

所以在分布式大模型里，不能只看单卡 TFLOPs，还要看节点内互连、跨节点网络和通信算子的匹配。

## 7. 面试速记

- V100 首次引入 Tensor Core，A100 成为 BF16/TF32 大模型训练标配，H100 引入 FP8 和 Transformer Engine。
- CUDA Core 做标量 FMA，Tensor Core 做矩阵 MMA。
- Transformer 的主要计算是 GEMM，因此 Tensor Core 是大模型吞吐的核心。
- GPU 内存层级从快到慢大致是：寄存器、SRAM、L2、HBM。
- 大模型推理常常是 Memory Bound，因为 decode 阶段要频繁读取权重和 KV Cache。
- FlashAttention 不减少理论计算量，而是减少 HBM 读写，避免落地 `N × N` 注意力矩阵。
- Triton/CUDA 优化的核心思路是 tiling、fusion、减少 HBM 访问、提高 Tensor Core 利用率。
- PCIe 是通用互连，NVLink/NVSwitch 是高带宽 GPU 通信基础，对多卡训练很关键。

## 8. 一句话总结

GPU 高性能大模型计算的关键，不只是“有多少 TFLOPs”，而是能否把矩阵乘法送上 Tensor Core，并让数据尽量停留在寄存器、SRAM、L2 这些高速层级里，少走 HBM 和慢速互连。
