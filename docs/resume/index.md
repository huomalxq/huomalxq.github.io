---
title: 个人简历
---

<section class="resume-sheet">
  <header class="resume-top">
    <div class="resume-top__copy">
      <p class="resume-kicker">CURRICULUM VITAE</p>
      <h1>林祥庆</h1>
      <p class="resume-tagline">计算机科学与技术硕士在读，关注 LLM 推理加速、Agent 工作流、RAG / Text2SQL 与模型微调对齐。</p>
      <div class="resume-badge-row">
        <span>Speculative Decoding</span>
        <span>LangGraph / RAG</span>
        <span>LoRA SFT & Preference Alignment</span>
      </div>
      <div class="home-actions home-actions--compact">
        <a class="home-button home-button--primary" href="../assets/files/resume.pdf" target="_blank" rel="noopener">下载 PDF 简历</a>
        <a class="home-button home-button--tertiary" href="https://github.com/huomalxq/huomalxq.github.io" target="_blank" rel="noopener">返回 GitHub 仓库</a>
      </div>
    </div>
    <div class="resume-contact">
      <a href="tel:19857150257">19857150257</a>
      <a href="mailto:1192428849@qq.com">1192428849@qq.com</a>
    </div>
  </header>

  <div class="resume-metric-grid">
    <article class="resume-metric">
      <span>Inference Speedup</span>
      <strong>1.41-3.31x</strong>
      <p>不同模型设置下的端到端推理加速，同时保持输出质量稳定。</p>
    </article>
    <article class="resume-metric">
      <span>Table Recall</span>
      <strong>61.4% -> 81.6%</strong>
      <p>通过补充表字段、业务样例与指标口径描述提升 RAG 表结构召回。</p>
    </article>
    <article class="resume-metric">
      <span>Response Time</span>
      <strong>50s -> 30s</strong>
      <p>定位主要耗时节点后调整工作流编排和代码执行流程。</p>
    </article>
  </div>

  <div class="resume-layout">
    <aside class="resume-rail">
      <article class="resume-sidecard">
        <p class="resume-sidecard__label">当前关注</p>
        <ul class="resume-mini-list">
          <li>长草稿推测解码、软拒绝机制与 KV Cache 复用</li>
          <li>LangGraph 编排 RAG、Text2SQL、SQL 校验与结果解释</li>
          <li>多模型 LoRA SFT、DPO / GRPO 偏好对齐实验流程</li>
        </ul>
      </article>

      <article class="resume-sidecard">
        <p class="resume-sidecard__label">技术栈</p>
        <div class="resume-skill-groups">
          <div class="resume-skill-group">
            <strong>LLM / 训练</strong>
            <div class="resume-skills">
              <span>PyTorch</span>
              <span>Transformers</span>
              <span>LLaMA-Factory</span>
              <span>TRL</span>
              <span>PEFT</span>
              <span>LoRA</span>
              <span>DPO</span>
              <span>GRPO</span>
            </div>
          </div>
          <div class="resume-skill-group">
            <strong>Agent / RAG</strong>
            <div class="resume-skills">
              <span>LangChain</span>
              <span>LangGraph</span>
              <span>RAG</span>
              <span>Text2SQL</span>
              <span>vLLM</span>
              <span>Ollama</span>
            </div>
          </div>
          <div class="resume-skill-group">
            <strong>开发与部署</strong>
            <div class="resume-skills">
              <span>Python</span>
              <span>FastAPI</span>
              <span>Flask</span>
              <span>Vue3</span>
              <span>Docker</span>
              <span>MySQL</span>
              <span>Nginx</span>
            </div>
          </div>
        </div>
      </article>

      <article class="resume-sidecard">
        <p class="resume-sidecard__label">获奖情况</p>
        <div class="resume-awards">
          <article class="resume-award">
            <strong>第二届开放原子大赛 Teco-RAG 大模型开发任务挑战赛三等奖</strong>
            <span>2025.04</span>
            <p>独立完成，奖金 2 万元</p>
          </article>
          <article class="resume-award">
            <strong>第二届开放原子大赛 Tecorigin 算子开发任务挑战赛优秀奖</strong>
            <span>2025.04</span>
            <p>独立完成，奖金 5 千元</p>
          </article>
          <article class="resume-award">
            <strong>第十四届中国大学生服务外包创新创业大赛国家三等奖</strong>
            <span>2023.07</span>
          </article>
          <article class="resume-award">
            <strong>2023 年华为智能基座奖学金</strong>
            <span>2023</span>
          </article>
          <article class="resume-award">
            <strong>2022 中国移动创客马拉松大赛最具发展潜力奖</strong>
            <span>2022.10</span>
            <p>奖金 1 万元</p>
          </article>
        </div>
      </article>
    </aside>

    <div class="resume-main">
      <section class="resume-sectioncard">
        <p class="section-kicker">Education</p>
        <h2>教育经历</h2>

        <article class="resume-item">
          <div class="resume-item__head">
            <strong>苏州大学（211） · 计算机科学与技术学院</strong>
            <span>2024.09 - 2027.06</span>
          </div>
          <p>硕士研究生（推免） · 计算机科学与技术（学硕） · 导师：贾俊铖</p>
        </article>

        <article class="resume-item">
          <div class="resume-item__head">
            <strong>浙江工业大学 · 计算机科学与技术学院</strong>
            <span>2020.10 - 2024.06</span>
          </div>
          <p>本科 · 计算机科学与技术 · 辅修：智能科学与技术</p>
        </article>
      </section>

      <section class="resume-sectioncard">
        <p class="section-kicker">Research & Projects</p>
        <h2>项目 / 科研经历</h2>

        <article class="resume-card">
          <div class="resume-item__head">
            <strong>LLM 模型推理加速（推测解码优化）</strong>
            <span>2025.04 - 至今</span>
          </div>
          <p class="resume-tech">PyTorch · Transformers · Speculative Decoding · KV Cache</p>
          <ul>
            <li>针对长草稿推测解码中无效计算较多、加速收益不稳定的问题，参与基于软拒绝机制的分支推测解码方案设计，围绕草稿生成、token 采样、KV Cache 复用等环节进行实验验证与论文撰写。</li>
            <li>设计不同草稿长度、采样设置与模型配置下的消融对比实验，分析 Token 接受率、推理耗时与生成质量之间的变化关系，为方法有效性和适用场景提供实验支撑。</li>
            <li>构建推理速度、Token 接受率与生成质量等指标的对比实验，方案在不同模型设置下取得约 1.41-3.31x 端到端推理加速，并保持输出质量稳定；目前有 1 篇 EMNLP 论文在投。</li>
          </ul>
        </article>

        <article class="resume-card">
          <div class="resume-item__head">
            <strong>基于 GSM8K 的多模型 LoRA SFT 与偏好对齐实验</strong>
            <span>2025.01 - 2025.03</span>
          </div>
          <p class="resume-tech">LLaMA-Factory · TRL · PEFT · LoRA · DPO · GRPO</p>
          <ul>
            <li>面向数学推理任务中指令格式、解题过程与最终答案输出不稳定的问题，基于 LLaMA-Factory 搭建可复用的 LoRA SFT 流程，将 GSM8K 清洗并整理为数学推理指令样例。</li>
            <li>围绕 LLaMA3 / Qwen2.5 系列模型设计统一训练配置与评测模板，支持从小参数模型到 7B / 8B 模型的横向对比，分析模型规模、指令微调状态对 SFT 效果的影响。</li>
            <li>基于 TRL 在 SFT checkpoint 上进行 DPO 与 GRPO 微调，构造 chosen-rejected 偏好样例并设计答案正确性 / 格式奖励函数，形成覆盖 SFT、偏好数据构造与偏好对齐的完整实验流程。</li>
          </ul>
        </article>
      </section>

      <section class="resume-sectioncard">
        <p class="section-kicker">Internship</p>
        <h2>实习经历</h2>

        <article class="resume-card">
          <div class="resume-item__head">
            <strong>Philips · Agent 开发实习生（苏州）</strong>
            <span>2026.03 - 2026.05</span>
          </div>
          <p class="resume-tech">LangChain / LangGraph · Agent · vLLM · RAG · Ollama · Workflow · Docker · FastAPI</p>
          <ul>
            <li>面向企业自然语言问数中表结构召回、SQL 校验与结果解释链路分散的问题，基于 LangGraph 编排 RAG 表结构检索、Text2SQL、SQL 校验重试、代码执行与结果解释节点。</li>
            <li>针对表结构召回不足的问题，补充表字段、业务样例与指标口径描述，优化 RAG 召回方法，将数据表召回率从 61.4% 提升至 81.6%。</li>
            <li>编写自动测试脚本输出召回率、节点耗时与端到端响应时间等指标，定位主要耗时节点后调整工作流编排和代码执行流程，将业务响应时间从 50s 降至 30s。</li>
          </ul>
        </article>

        <article class="resume-card">
          <div class="resume-item__head">
            <strong>上海诺基亚贝尔股份有限公司 · 后端开发 / 数据清洗实习生（杭州）</strong>
            <span>2023.09 - 2024.01</span>
          </div>
          <ul>
            <li>面向 Robot Framework 自动化测试脚本生成的模型微调需求，负责后端接口实现与训练数据准备；对原有 Robot Framework 自动化测试代码进行清洗、解析与样例提取，完成格式规范化和微调训练数据构造。</li>
          </ul>
        </article>
      </section>
    </div>
  </div>
</section>
