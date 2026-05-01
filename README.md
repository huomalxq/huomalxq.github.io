# huomalxq.github.io

基于 `MkDocs` 搭建的个人主页，包含两个主要入口：

- `个人简历`
- `学习记录`

## 本地预览

```bash
pip install -r requirements.txt
mkdocs serve
```

默认访问地址：`http://127.0.0.1:8000`

## 目录说明

- `docs/index.md`：主页
- `docs/resume/`：简历页面与 PDF
- `docs/study/`：学习记录
- `docs/assets/stylesheets/extra.css`：站点自定义样式
- `.github/workflows/deploy.yml`：GitHub Pages 自动部署

## 发布方式

推送到 `main` 分支后，GitHub Actions 会自动构建并部署站点。
