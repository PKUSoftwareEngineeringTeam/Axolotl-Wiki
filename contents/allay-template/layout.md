---
title: 自定义布局
raw: true
description: 创建和使用自定义布局模板
tags: ["Allay 功能", "模板", "布局"]
date: 2025-11-23
group: Allay 模板
---

## 布局

所有的 Allay 模板都应放在 `templates` 目录下。你至少需要包含 `page.html` 作为常规页面的默认模板。

当 markdown--[front matter](../custom-contents/front-matter) 中未指定 url 字段时，Allay 会使用 `page.html` 模板渲染页面。

### 自定义模板布局

并非所有页面都应使用相同的布局。你可以在 front matter 中通过 `template` 字段为每个页面指定不同的模板。例如：

`content/about/index.md`：

```md
---
title: About Me
template: about.html
---

Hello, this is the about page.
```

`templates/about.html`：

```html
<body>
    <h1>About Me</h1>
    <p>{: .content :}</p>
</body>
```

这样，你可以为博客中的不同类型页面创建自定义布局。只需确保指定的模板文件存在于 `templates` 目录中即可。
