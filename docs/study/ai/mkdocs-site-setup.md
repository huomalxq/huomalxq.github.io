# MkDocs 站点搭建

## 目标

为 `huomalxq.github.io` 搭一个结构清晰、后续容易维护的个人站点：

- 首页只保留两个核心入口。
- 简历页直接承载 PDF。
- 学习记录按主题分类，适合长期追加。

## 当前结构

```text
docs/
├─ index.md
├─ resume/
│  └─ index.md
├─ study/
│  ├─ index.md
│  ├─ ai/
│  │  ├─ index.md
│  │  └─ mkdocs-site-setup.md
│  └─ engineering/
│     ├─ index.md
│     └─ note-template.md
└─ assets/
   ├─ files/
   └─ stylesheets/
```

## 为什么这样组织

1. `MkDocs` 很适合做持续增长的学习记录，而不是一次性静态页面。
2. 首页只做导航，不承担过多内容，后续扩展不会破坏结构。
3. 简历 PDF 和学习笔记都纳入同一个发布流程，维护成本更低。

## 后续维护建议

- 新增学习记录时，优先放到已有分类下。
- 如果某个主题笔记变多，再单独拆一个新分类。
- 每次新增页面后，同步更新 `mkdocs.yml` 的导航。

