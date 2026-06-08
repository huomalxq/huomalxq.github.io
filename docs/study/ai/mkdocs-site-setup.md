# MkDocs 站点搭建

## 目标

为 `huomalxq.github.io` 搭一个结构清晰、后续容易维护的个人站点：

- 首页负责快速说明个人方向和核心入口。
- 简历页承载结构化网页简历，并保留 PDF 下载入口。
- 学习记录按主题分类，方便后续持续追加实验、复盘和工程笔记。

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

1. `MkDocs` 适合持续增长的学习记录，比手写多个静态 HTML 页面更容易维护。
2. `docs/` 只放内容源文件，构建产物由命令或 GitHub Actions 生成，职责更清楚。
3. 首页、简历和学习记录共享同一套样式与发布流程，后续维护成本更低。
4. 分类页只负责组织主题，具体经验放进独立笔记，避免页面越写越散。

## 后续维护建议

- 新增学习记录时，先判断它属于 `AI / Agent` 还是 `工程实践`。
- 如果某个主题超过 3-5 篇笔记，再单独拆出新的分类。
- 每次新增页面后，同步更新 `mkdocs.yml` 的导航。
- 笔记标题优先写具体对象和动作，例如“LangGraph Text2SQL 校验重试设计”。

## 发布检查清单

- `mkdocs.yml` 中的导航是否包含新页面。
- 页面内相对链接是否能从构建后的路径访问。
- 静态资源是否放在 `docs/assets/` 下。
- 构建前确认临时目录不会被提交，例如 `.mkdocs-out/` 已加入 `.gitignore`。
