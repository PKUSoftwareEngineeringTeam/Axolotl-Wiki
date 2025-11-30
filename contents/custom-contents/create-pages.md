---
title: 创建自定义页面
raw: true
description: 在 Allay 博客中创建和组织自定义页面
date: 2025-11-24
group: 自定义内容
tags: ["Allay 内容", "自定义页面", "Markdown"]
---

## 创建页面

你可以通过将 Markdown 文件添加到 `content` 目录，在 Allay 中创建自定义页面。当你运行 `allay build` 或 `allay server` 命令时，每个 Markdown 文件都会被转换为静态 HTML 页面。

所有 Markdown 文件都应在文件顶部包含 front-matter 元数据。关于可用的元数据字段，请参见 [Front-matter](./front-matter)。

## 文件组织

除非在 front-matter 中指定了 "url" 字段，否则页面的 URL 会根据文件路径自动生成。需要注意的是，文件名为 `index.md` 的文件具有特殊意义，它会被视为该目录的根页面。

例如，以下文件结构：

```
content
├── about.md
├── blog
│   ├── index.md
│   └── first-post.md
└── projects
    └── project1.md
```

生成的 `public` 目录下的 HTML 文件为：

```
public
├── about.html          # 来自 about.md
├── blog
│   ├── index.html      # 来自 blog/index.md
│   └── first-post.html # 来自 blog/first-post.md
└── projects
    └── project1.html   # 来自 projects/project1.md
```

如果你采用了类似的多级目录，并写有多个对应的[模版布局](../allay-template/layout),那么你可以在目录的index文件和其他文件中采用不同的template配置。比如：

`public/blog/index.html`:

```md
---
title: My School Blog 
template: index.html
---

Welcome to my school series! This is the index page.
```

`public/blog/first-post.html`:

```md
---
title: Orientation Day
template: page.html
---

Hello, this is my first post of this series.
...
```
