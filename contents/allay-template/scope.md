---
title: 作用域
raw: true
description: Allay 模板系统中的变量作用域
tags: ["Allay 功能", "模板", "作用域"]
date: 2025-11-24
group: Allay 模板
---

`templates` 目录中的每个 html 文件都有自己的变量作用域。使用 `{: . :}` 访问当前作用域。

## 子作用域（Child Scope）

为简化操作，Allay 提供了 `with` 指令用于创建子作用域。

举个例子，假设当前变量作用域如下：

```toml
title = "Hello, world!"
[author]
name = "John Doe"
age = 30
```

下面两个代码片段是等价的：

```html
<p>{: .author.name :}</p>
```

```html
{- with .author -}
<p>{: .name :}</p>
{- end -}
```

## 全局作用域（Global Scope）

Allay 会解析你的配置文件（如 `allay.toml` 的 `Param`），并将内容传递到全局作用域。你可以通过 `site` 对象的 `param` 字段在模板中访问任意配置变量：

`allay.toml`：

```toml
[Param]
footer = "Axolotl Theme, 2025"
```

`footer.html`：

```html
{: site.param.footer :}
```

## Markdown 页面作用域（Markdown Page Scope）

对于每个 markdown 页面，Allay 会解析其 front-matter 并传递到页面作用域。

在常规页面（如 `page.html`）的 [模板](./layouts) 中，可以通过当前页面对象 `.` 直接访问 front-matter 参数，并通过特殊变量 `.content` 获取 markdown 文件内容。

基本用法示例：

`content/some-path/index.md`：

```md
---
title: Test
date: 2024-01-01
description: This is a test page.
tags: ["test", "example"]
---
Hello, this is a test page.
```

`templates/page.html`：

```html
<h1>{: .title :}</h1>
<p>{: .date :}</p>
<p>{: .description :}</p>
<ul>
    {- for $tag in .tags -}
    <li>{: $tag :}</li>
    {- end -}
</ul>
<div>
    {: .content :}
</div>
```

对于`index.html`，可以通过 `site` 对象的 `pages` 字段访问所有页面。`pages` 是所有 markdown 页面组成的数组，每个页面都具有上述相同的作用域。

在 `index.html` 中列出所有页面的示例：

```html
<ul>
    {- for $page: site.pages -}
        {- with $page -}
        <li>
            <a href="{: .url :}">{: .title :}</a>
            <p>{: .description :}</p>
        </li>
        {- end -}
    {- end -}
</ul>
```
