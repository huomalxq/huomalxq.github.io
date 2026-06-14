---
title: 学习记录
---

<section class="study-hero">
  <div class="study-hero__copy">
    <p class="section-kicker">PROJECT NOTEBOOK</p>
    <h1>学习记录</h1>
    <p>这里集中整理项目复盘和面试表达，把本地项目材料沉淀成可浏览、可回顾、可继续补充的 Markdown 记录。</p>
    <div class="hero-pill-row">
      <span class="hero-pill">项目复盘</span>
      <span class="hero-pill">面试表达</span>
      <span class="hero-pill">长期维护</span>
    </div>
    <div class="home-actions home-actions--compact">
      <a class="home-button home-button--tertiary" href="https://github.com/huomalxq/huomalxq.github.io" target="_blank" rel="noopener">返回 GitHub 仓库</a>
    </div>
  </div>

  <article class="study-hero__card">
    <span class="hero-panel__eyebrow">Current Notes</span>
    <strong>项目复盘与基础笔记</strong>
    <p>当前保留数据分析 Agent、开放原子大赛 Teco-RAG、GSM8K 后训练实验与大模型系统基础五篇记录，去掉原来的分类层级。</p>
  </article>
</section>

<section class="study-grid study-grid--wide">
  <a class="study-card" href="data-analysis-agent/">
    <span class="study-card__label">Project Review</span>
    <strong>数据分析 Agent 后端项目</strong>
    <span>复盘自然语言问数后端、LangGraph 工作流、RAG 检索、SQL 校验重试和结果分析闭环。</span>
    <em class="study-card__meta">FastAPI / LangGraph / Milvus / Vertica / vLLM</em>
  </a>
  <a class="study-card" href="teco-rag-project-summary/">
    <span class="study-card__label">Project Review</span>
    <strong>开放原子大赛 Teco-RAG</strong>
    <span>整理 RAG baseline、文档切分、Embedding/Rerank 选型、多查询、HyDE、BM25 和参数调优。</span>
    <em class="study-card__meta">Milvus / bge / Rerank / Qwen / BM25</em>
  </a>
  <a class="study-card" href="gsm8k-post-training-experiments/">
    <span class="study-card__label">LLM Training</span>
    <strong>GSM8K 后训练实验复盘</strong>
    <span>整理 Qwen2.5-1.5B 的 LoRA SFT、DPO、GRPO 主线实验、关键指标和面试表达。</span>
    <em class="study-card__meta">GSM8K / LoRA SFT / DPO / GRPO / Qwen2.5</em>
  </a>
  <a class="study-card" href="llm-algo-leetcode/llm-data-types-and-precision/">
    <span class="study-card__label">LLM Systems</span>
    <strong>大模型数据格式与混合精度</strong>
    <span>总结 FP32、FP16、BF16、TF32、FP8 的显存占用、数值范围、训练稳定性和硬件演进。</span>
    <em class="study-card__meta">FP16 / BF16 / AMP / A100 / H100</em>
  </a>
  <a class="study-card" href="llm-algo-leetcode/llm-gpu-architecture-and-memory/">
    <span class="study-card__label">LLM Systems</span>
    <strong>GPU 架构与内存层级</strong>
    <span>梳理 Tensor Core、CUDA Core、HBM、SRAM、FlashAttention 与多卡互连的核心关系。</span>
    <em class="study-card__meta">Tensor Core / HBM / SRAM / NVLink</em>
  </a>
</section>

<section class="study-feed">
  <p class="section-kicker">Note Index</p>
  <h2>笔记目录</h2>
  <div class="feed-list">
    <article class="feed-item">
      <time datetime="2026-06-14">项目</time>
      <div>
        <strong><a href="data-analysis-agent/">数据分析 Agent 后端项目复盘</a></strong>
        <p>整理自然语言问数项目的背景、架构、关键问题、解决方案和面试表达。</p>
      </div>
    </article>
    <article class="feed-item">
      <time datetime="2026-06-14">项目</time>
      <div>
        <strong><a href="teco-rag-project-summary/">开放原子大赛 Teco-RAG 项目总结</a></strong>
        <p>整理 RAG 系统从 baseline 到检索优化的实验过程、关键策略和项目收获。</p>
      </div>
    </article>
    <article class="feed-item">
      <time datetime="2026-06-14">项目</time>
      <div>
        <strong><a href="gsm8k-post-training-experiments/">GSM8K 后训练实验复盘</a></strong>
        <p>整理 LoRA SFT、DPO、GRPO 在 GSM8K 上的主线结果、关键参数和方法选择。</p>
      </div>
    </article>
    <article class="feed-item">
      <time datetime="2026-06-14">学习</time>
      <div>
        <strong><a href="llm-algo-leetcode/llm-data-types-and-precision/">大模型数据格式与混合精度知识点总结</a></strong>
        <p>梳理大模型训练和推理中常见数据格式、BF16 训练优势、FP32 主权重、A100/ H100 精度能力。</p>
      </div>
    </article>
    <article class="feed-item">
      <time datetime="2026-06-14">学习</time>
      <div>
        <strong><a href="llm-algo-leetcode/llm-gpu-architecture-and-memory/">GPU 物理架构、内存层级与核心硬件单元总结</a></strong>
        <p>总结 GPU 架构演进、Tensor Core、Memory Bound、FlashAttention 的 SRAM 优化和节点内通信。</p>
      </div>
    </article>
  </div>
</section>

<section class="study-columns">
  <div class="study-feed">
    <p class="section-kicker">Recent Updates</p>
    <h2>最近更新</h2>
    <div class="feed-list">
      <article class="feed-item">
        <time datetime="2026-06-14">2026.06.14</time>
        <div>
          <strong>补充 GSM8K 后训练实验复盘</strong>
          <p>将本地 GSM8K 主线实验报告整理为 LoRA SFT、DPO、GRPO 对比笔记。</p>
        </div>
      </article>
      <article class="feed-item">
        <time datetime="2026-06-14">2026.06.14</time>
        <div>
          <strong>补充 GPU 架构与内存层级笔记</strong>
          <p>整理 Datawhale 页面中的 Tensor Core、GPU 内存层级、FlashAttention 与多卡互连知识点。</p>
        </div>
      </article>
      <article class="feed-item">
        <time datetime="2026-06-14">2026.06.14</time>
        <div>
          <strong>补充大模型数据格式与混合精度笔记</strong>
          <p>整理 Datawhale 页面中的 FP16、BF16、TF32、FP8 与混合精度训练知识点。</p>
        </div>
      </article>
      <article class="feed-item">
        <time datetime="2026-06-14">2026.06.14</time>
        <div>
          <strong>整理本地项目材料为两篇学习记录</strong>
          <p>移除原来的多层分类，将两份本地 Markdown 整理为独立项目复盘页面。</p>
        </div>
      </article>
      <article class="feed-item">
        <time datetime="2026-06-08">2026.06.08</time>
        <div>
          <strong>同步新版简历与主页定位</strong>
          <p>将首页、简历页和学习记录入口统一到 LLM 系统、Agent 工程与模型训练实验方向。</p>
        </div>
      </article>
      <article class="feed-item">
        <time datetime="2026-05-01">2026.05.01</time>
        <div>
          <strong>搭建个人主页与学习记录站点骨架</strong>
          <p>完成 GitHub Pages、MkDocs 配置、首页入口设计和知识库分类。</p>
        </div>
      </article>
    </div>
  </div>

  <div class="study-principles">
    <p class="section-kicker">Writing Rules</p>
    <h2>记录原则</h2>
    <div class="principle-grid">
      <article class="principle-card">
        <strong>单页单项目</strong>
        <p>一篇笔记围绕一个项目或一次复盘展开，避免多个不相关主题混在一起。</p>
      </article>
      <article class="principle-card">
        <strong>首页做目录</strong>
        <p>学习记录首页直接展示当前笔记，减少多层分类带来的查找成本。</p>
      </article>
      <article class="principle-card">
        <strong>标题要可搜索</strong>
        <p>标题写清项目名和主题，方便站内导航、浏览器搜索和 Git 历史回溯。</p>
      </article>
    </div>
  </div>
</section>
