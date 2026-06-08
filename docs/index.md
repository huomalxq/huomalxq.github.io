---
title: 首页
---

<section class="home-hero">
  <div class="hero-copy">
    <p class="hero-eyebrow">LIN XIANGQING / LLM & AGENT ENGINEERING</p>
    <h1>林祥庆：聚焦 LLM 推理加速、Agent 工作流与 AI 应用落地。</h1>
    <p class="hero-lead">
      苏州大学计算机科学与技术硕士在读，主要围绕 Speculative Decoding、RAG / Text2SQL Agent、LoRA SFT 与偏好对齐实验展开研究和工程实践。
    </p>
    <div class="hero-pill-row">
      <span class="hero-pill">Speculative Decoding</span>
      <span class="hero-pill">LangGraph Agent</span>
      <span class="hero-pill">LoRA / DPO / GRPO</span>
    </div>
    <div class="home-actions">
      <a class="home-button home-button--primary" href="resume/">查看个人简历</a>
      <a class="home-button home-button--secondary" href="study/">进入学习记录</a>
      <a class="home-button home-button--tertiary" href="assets/files/resume.pdf" target="_blank" rel="noopener">下载 PDF 简历</a>
    </div>
  </div>

  <aside class="hero-panel">
    <article class="hero-panel__card hero-panel__card--accent">
      <span class="hero-panel__eyebrow">Current Research</span>
      <strong>推测解码优化</strong>
      <p>参与基于软拒绝机制的分支推测解码方案设计，围绕草稿生成、token 采样与 KV Cache 复用开展实验。</p>
    </article>
    <article class="hero-panel__card">
      <span class="hero-panel__eyebrow">Recent Internship</span>
      <strong>Philips Agent 开发实习</strong>
      <p>基于 LangGraph 编排 RAG 表结构检索、Text2SQL、SQL 校验重试、代码执行与结果解释节点。</p>
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
    <p>集中展示教育经历、LLM 研究项目、Agent 实习经历、技术栈与竞赛获奖，方便招聘方快速浏览。</p>
    <div class="portal-tags">
      <span>Education</span>
      <span>Research</span>
      <span>Internship</span>
    </div>
  </a>
  <a class="portal-card portal-card--warm" href="study/">
    <p class="section-kicker">Knowledge Base</p>
    <h2>学习记录</h2>
    <p>把 AI、Agent、工程实践和站点搭建过程沉淀成可长期维护的笔记，用于复盘实验判断和技术路线。</p>
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
    <h2>当前主页重点呈现什么</h2>
    <p>这一版优先把最新简历里的研究、实习与可量化结果放到首屏和简历页，减少泛泛介绍，让访问者能更快判断技术方向和实践深度。</p>
  </div>
  <div class="home-note__points">
    <article class="note-point">
      <strong>LLM 推理优化</strong>
      <p>围绕长草稿推测解码、token 接受率、KV Cache 复用与生成质量稳定性做实验验证。</p>
    </article>
    <article class="note-point">
      <strong>Agent / RAG 工程</strong>
      <p>关注自然语言问数场景中表结构召回、Text2SQL、SQL 校验和结果解释的工作流编排。</p>
    </article>
    <article class="note-point">
      <strong>模型微调与对齐</strong>
      <p>基于 GSM8K 做多模型 LoRA SFT，并补充 DPO、GRPO 偏好对齐实验流程。</p>
    </article>
  </div>
</section>
