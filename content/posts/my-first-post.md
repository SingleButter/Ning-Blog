+++
date = '2026-01-04T13:15:22-05:00'
draft = false

title = 'My First Post'

+++

# Zuning的第一个博客文章



在 GitHub Pages 上只显示框架而不显示内容，通常是由以下几个常见原因导致的。你可以对照你的项目逐一排查：

### 1. 文章处于“草稿”状态（最常见原因）

Hugo 默认不会渲染标记为草稿的文章。

- **检查方法**：打开 `content/` 文件夹下的 Markdown 文件（如 `my-first-post.md`）。
- **解决方法**：查看文件顶部的元数据（Front Matter），将 `draft: true` 改为 **`draft: false`**。
- **原因**：如果你在本地运行 `hugo server -D` 能看到内容，但在 GitHub 上看不到，通常是因为 `-D` 参数强制渲染了草稿，而 GitHub 上的正式构建命令通常不带 `-D`。
