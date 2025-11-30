---
title: 博客文件结构
date: 2025-11-20
group: 快速开始
description: 了解 Allay 博客的目录和文件组织方式
tags: ["Allay 入门", "文件结构", "快速开始"]
---

你的博客目录结构如下所示：

```
.
├── allay.toml      # 博客的配置文件，通常来自你使用的主题
├── content         # 你的 Markdown 文件存放于此
├── public          # 生成的静态文件将被放置在这里
├── shortcodes      # 可在此定义自定义短代码
├── static          # 可直接访问的静态文件
└── themes          # 主题目录
```

- `static/`：该目录包含静态文件，如图片和 PDF 文件。这些文件会在构建过程中直接复制到 `public/` 目录，并可通过 URL 直接访问。
- `content/`：该目录存放你的 Markdown 文件，每个 Markdown 文件代表博客中的一个页面。关于如何创建和组织 Markdown 文件，详见 [创建页面](../custom-contents/create-pages)。
- `public/`：构建博客后，生成的静态文件会放在此目录。你可以将该目录内容部署到你的 Web 服务器。
- `shortcodes/`：用于存放你自定义的短代码，可在 Markdown 文件中使用。关于短代码的创建和使用，详见 [短代码](../extra-functions/shortcode)。
- `themes/`：该目录包含博客的主题。你可以为每个主题创建子目录，每个主题可拥有自己的模板和静态文件。关于主题的自定义，详见 [主题](../themes/)。
- `allay.toml`：博客的主配置文件。你可以在此设置站点标题、基础 URL 和主题等参数。更多详情见 [配置](../configuration/)。
