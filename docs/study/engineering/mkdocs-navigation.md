# MkDocs 导航维护记录

## 背景

MkDocs 的内容文件放在 `docs/` 目录下，但站点导航主要由根目录的 `mkdocs.yml` 控制。这个仓库已经按“首页、个人简历、学习记录”三类组织，因此后续新增学习记录时，重点是保持导航层级清晰。

## 过程

当前学习记录的导航结构大致是：

```yaml
nav:
  - 学习记录:
      - 学习总览: study/index.md
      - AI / Agent:
          - 分类说明: study/ai/index.md
      - 工程实践:
          - 分类说明: study/engineering/index.md
```

新增笔记时，文件路径和导航路径要保持一致。例如工程实践下的笔记可以这样加入：

```yaml
      - 工程实践:
          - 分类说明: study/engineering/index.md
          - Git 仓库维护流程: study/engineering/git-repository-workflow.md
```

需要注意 `mkdocs.yml` 对缩进比较敏感。列表层级错一格，构建时就可能报错，或者导航显示到错误位置。

## 结论

这个站点更适合采用“分类页 + 独立笔记页”的方式维护：

- `study/index.md` 负责展示学习记录总览和最近更新。
- `study/ai/index.md`、`study/engineering/index.md` 负责说明分类边界。
- 具体经验、命令和复盘写进单独 Markdown 页面。

这样做的好处是页面之间职责明确，后续新增内容时不会把总览页写得过长。

## 后续

如果学习记录数量继续增加，可以考虑按年份或专题再细分，例如：

- `study/engineering/deploy/`
- `study/engineering/debugging/`
- `study/ai/agent-workflow/`
