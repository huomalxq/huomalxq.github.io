---
title: 首页
---

<section class="home-hero">
  <div class="hero-copy">
    <p class="hero-eyebrow">LIN XIANGQING / LLM SYSTEMS & AGENT ENGINEERING</p>
    <h1>面向 LLM 推理效率与 Agent 落地的计算机硕士。</h1>
    <p class="hero-lead">
      我是林祥庆，苏州大学计算机科学与技术硕士在读。当前重点做推测解码优化、企业问数 Agent 工作流，以及基于 LoRA / DPO / GRPO 的模型微调与偏好对齐实验。
    </p>
    <div class="hero-pill-row">
      <span class="hero-pill">Speculative Decoding</span>
      <span class="hero-pill">LangGraph Agent</span>
      <span class="hero-pill">LoRA / DPO / GRPO</span>
    </div>
    <div class="home-actions">
      <a class="home-button home-button--primary" href="resume/">查看网页版简历</a>
      <a class="home-button home-button--secondary" href="study/">进入学习记录</a>
      <a class="home-button home-button--tertiary" href="assets/files/resume.pdf" target="_blank" rel="noopener">下载 PDF 简历</a>
    </div>
  </div>

  <aside class="hero-panel">
    <article class="hero-panel__card hero-panel__card--accent">
      <span class="hero-panel__eyebrow">Current Research</span>
      <strong>让大模型生成更快、更稳</strong>
      <p>围绕长草稿推测解码中的无效计算和收益波动，参与软拒绝机制与分支草稿策略设计，并验证 KV Cache 复用效果。</p>
    </article>
    <article class="hero-panel__card">
      <span class="hero-panel__eyebrow">Recent Internship</span>
      <strong>把自然语言问数做成可运行流程</strong>
      <p>在 Philips 实习中用 LangGraph 编排表结构 RAG、Text2SQL、SQL 校验重试、代码执行和结果解释节点。</p>
    </article>
    <div class="hero-signal">
      <div>
        <b>1.41-3.31x</b>
        <span>端到端推理加速</span>
      </div>
      <div>
        <b>81.6%</b>
        <span>数据表召回率</span>
      </div>
      <div>
        <b>30s</b>
        <span>业务响应时间</span>
      </div>
    </div>
  </aside>
</section>

<section class="portal-grid">
  <a class="portal-card" href="resume/">
    <p class="section-kicker">Resume</p>
    <h2>个人简历</h2>
    <p>按招聘阅读节奏整理教育、研究、实习、技术栈与获奖信息，突出可量化结果和工程职责。</p>
    <div class="portal-tags">
      <span>Education</span>
      <span>Research</span>
      <span>Internship</span>
    </div>
  </a>
  <a class="portal-card portal-card--warm" href="study/">
    <p class="section-kicker">Knowledge Base</p>
    <h2>学习记录</h2>
    <p>沉淀 AI / Agent 实验、工程实践和站点维护过程，把临时经验变成可回溯的技术笔记。</p>
    <div class="portal-tags">
      <span>AI / Agent</span>
      <span>Engineering</span>
      <span>Notes</span>
    </div>
  </a>
</section>

<section class="home-note">
  <div class="home-note__intro">
    <p class="section-kicker">Focus</p>
    <h2>主页想让访问者先看到什么</h2>
    <p>比起罗列经历，这里优先回答三个问题：研究在解决什么效率问题，实习中把 Agent 落到了哪条业务链路，训练实验覆盖了哪些完整流程。</p>
  </div>
  <div class="home-note__points">
    <article class="note-point">
      <strong>LLM 推理优化</strong>
      <p>用消融实验解释草稿长度、采样配置、Token 接受率和生成质量之间的关系。</p>
    </article>
    <article class="note-point">
      <strong>Agent / RAG 工程</strong>
      <p>把表结构召回、SQL 生成、校验重试和解释输出拆成可观测、可调优的工作流节点。</p>
    </article>
    <article class="note-point">
      <strong>模型微调与对齐</strong>
      <p>从 GSM8K 数据整理到 SFT checkpoint，再到偏好样例与奖励函数，跑通对齐实验链路。</p>
    </article>
  </div>
</section>
