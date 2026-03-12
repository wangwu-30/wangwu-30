# Archē & The Weave

一个为 GitHub Pages 准备的 Jekyll 写作站点：既可以维护一本按卷章展开的书，也可以持续发布按时间更新的 blog。

## 目录结构

- `index.md`：站点首页
- `book.md`：书籍导言页
- `blog.md`：Blog 列表页
- `_chapters/`：书的正文章节，每篇都是一个独立 Markdown 文件
- `_posts/`：Blog 文章，使用 Jekyll 标准日期文件名
- `_data/volumes.yml`：卷的信息与顺序
- `_layouts/`：首页、书页、章节页、blog 页布局
- `assets/css/site.css`：站点视觉样式
- `.github/workflows/pages.yml`：GitHub Pages 自动发布工作流

## 如何新增一章

1. 在 `_chapters/` 里复制一篇现有文件。
2. 修改文件顶部 front matter：
   - `title`：中文标题
   - `title_en`：英文副标题
   - `chapter_label`：例如 `第三章`
   - `volume`：对应 `_data/volumes.yml` 里的 `id`
   - `order`：卷内顺序
   - `book_order`：全书顺序
3. 在 front matter 下方继续写 Markdown 正文。

## 如何新增一卷

在 `_data/volumes.yml` 里追加一项：

```yml
- id: new-volume
  order: 2
  label: 第二卷
  title: 新卷名
  title_en: The New Volume
  description: 这一卷的概述
```

然后把章节的 `volume` 指向这个 `id`。

## 如何新增一篇 Blog

在 `_posts/` 目录里新建文件，命名格式如下：

```text
YYYY-MM-DD-your-slug.md
```

例如：

```text
2026-03-12-notes-on-writing-systems.md
```

文件顶部最少只需要：

```md
---
title: "文章标题"
description: "可选摘要"
---
```

然后在 front matter 下方继续写 Markdown 正文。

## 发布到 GitHub Pages

1. 在 GitHub 创建仓库并推送当前目录内容。
2. 如果仓库名是 `username.github.io`，保留 `_config.yml` 中的 `baseurl: ""`。
3. 如果仓库名是普通项目名，例如 `arche-book`，把 `_config.yml` 改成 `baseurl: "/arche-book"`。
4. 到 GitHub 仓库的 `Settings > Pages`，确认发布来源为 `GitHub Actions`。
5. 推送到 `main` 分支后，工作流会自动构建并发布。

## 本地预览

GitHub Pages 在线构建不依赖你本机环境，但如果你想在本地预览，需要先准备 Jekyll 运行环境。

- Jekyll 官方当前要求 Ruby 2.7 或更高版本。
- 当前这个仓库没有内置 `Gemfile`，走的是“直接交给 GitHub Pages Actions 构建”的路径。

准备好本地 Jekyll 后，可以在仓库根目录执行：

```bash
jekyll serve
```

然后访问终端输出的本地地址。
