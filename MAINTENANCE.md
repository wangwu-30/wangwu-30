# Archē & The Weave Maintenance Notes

这个仓库是 `wangwu-30/wangwu-30`，因此根目录 `README.md` 会显示在 GitHub 个人主页上。站点维护说明单独放在这里，避免把内部说明暴露到 profile 页面。

## 目录结构

- `index.md`：站点首页
- `columns.md`：专栏列表页
- `columns/arche-and-the-weave.md`：当前专栏导言页
- `book.md`：旧 `/book/` 链接的跳转页
- `blog.md`：Blog 列表页
- `Archē & The Weave.md`：当前专栏的内部风格 guide，不对外展示
- `_chapters/`：书的正文章节，每篇都是一个独立 Markdown 文件
- `_data/columns.yml`：专栏信息、入口与简短风格摘要
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
   - `column_id`：可选；不写时默认归入当前专栏 `arche-and-the-weave`
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

## 如何新增一个专栏

1. 在 `_data/columns.yml` 里追加一项：

```yml
- id: new-column
  order: 2
  title: 新专栏名
  brand: Project Name
  permalink: /columns/new-column/
  description: 面向读者的专栏简介
  sidebar_description: 侧栏里的简短说明
  style_guide: your-guide.md
  style_summary: 冷静、锋利、带有哲学张力。
```

2. 在 `columns/` 目录下新建对应页面，例如 `columns/new-column.md`。
3. 新专栏下的章节在 front matter 里补 `column_id: new-column`。
4. 如果需要新的卷结构，也在 `_data/volumes.yml` 里补新的卷条目；侧栏只会显示当前专栏里实际存在章节的卷。

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

GitHub Pages 在线构建不依赖本机环境，但如果想本地预览，需要先准备 Jekyll 运行环境。

- Jekyll 官方当前要求 Ruby 2.7 或更高版本。
- 当前仓库没有内置 `Gemfile`，走的是“直接交给 GitHub Pages Actions 构建”的路径。

准备好本地 Jekyll 后，可以在仓库根目录执行：

```bash
jekyll serve
```

然后访问终端输出的本地地址。
