---
title: 首页
---

<section class="home-hero">
  <div class="hero-copy">
    <p class="hero-eyebrow">LIN XIANGQING</p>
    <h1>林祥庆</h1>
    <p class="hero-lead">
      苏州大学计算机硕士在读。关注大模型推理、Agent 后端和后训练实验。
    </p>
    <div class="hero-pill-row">
      <span class="hero-pill">LLM 推理优化</span>
      <span class="hero-pill">数据分析 Agent</span>
      <span class="hero-pill">后训练实验</span>
    </div>
    <div class="home-actions">
      <a class="home-button home-button--primary" href="resume/">查看网页版简历</a>
      <a class="home-button home-button--secondary" href="study/">进入学习记录</a>
      <a class="home-button home-button--tertiary" href="assets/files/resume.pdf" target="_blank" rel="noopener">下载 PDF 简历</a>
    </div>
  </div>

  <aside class="hero-panel">
    <article class="hero-panel__card hero-panel__card--accent">
      <span class="hero-panel__eyebrow">Research</span>
      <strong>推测解码优化</strong>
      <p>围绕分支草稿、软拒绝和 KV Cache 复用做实验，端到端加速 1.41-3.31x。</p>
    </article>
    <article class="hero-panel__card">
      <span class="hero-panel__eyebrow">Internship</span>
      <strong>自然语言问数后端</strong>
      <p>基于 LangGraph 串联表结构召回、Text2SQL、SQL 校验重试和结果解释，表召回率提升至 81.6%。</p>
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
    <p>教育、科研、实习、技能和获奖。</p>
    <div class="portal-tags">
      <span>教育</span>
      <span>科研</span>
      <span>实习</span>
    </div>
  </a>
  <a class="portal-card portal-card--warm" href="study/">
    <p class="section-kicker">Knowledge Base</p>
    <h2>学习记录</h2>
    <p>项目复盘、实验记录和技术笔记。</p>
    <div class="portal-tags">
      <span>数据分析 Agent</span>
      <span>Teco-RAG</span>
      <span>项目笔记</span>
    </div>
  </a>
</section>

<section class="home-note">
  <div class="home-note__intro">
    <p class="section-kicker">Selected Work</p>
    <h2>项目与实验</h2>
    <p>从推理加速、问数 Agent 到 RAG 和后训练，记录可复现的结果。</p>
  </div>
  <div class="home-note__points">
    <article class="note-point">
      <strong>推测解码</strong>
      <p>分支草稿、软拒绝、KV Cache 复用，取得 1.41-3.31x 加速。</p>
    </article>
    <article class="note-point">
      <strong>自然语言问数</strong>
      <p>RAG 表结构召回、Text2SQL、SQL 校验重试，响应时间降至 30s。</p>
    </article>
    <article class="note-point">
      <strong>GSM8K 后训练</strong>
      <p>对比 LoRA SFT、DPO 与 GRPO，GRPO 最佳 accuracy 达到 0.688。</p>
    </article>
    <article class="note-point">
      <strong>Teco-RAG</strong>
      <p>优化文档切分、Embedding / Rerank、多查询、HyDE 和 BM25 检索。</p>
    </article>
  </div>
</section>
