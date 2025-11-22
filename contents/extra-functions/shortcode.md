---
title: 额外功能——短代码
raw: true
---

短代码是 Allay 的一个强大功能，允许你在 Markdown 文件中嵌入动态内容。它类似于编程语言中的宏或函数，可以复用代码片段，并通过传递参数来自定义行为。

## 定义

所有短代码应定义在 `shortcodes` 目录下。每个短代码会绑定到同名的 HTML/Markdown 文件。你可以通过以下语法在 Markdown 文件中使用这些短代码：

```
{< shortcode_name params... >}
```

## 示例

### 自闭合短代码

`shortcodes/note.md`：

```md
![Note](https://img.shields.io/badge/Note-Important-brightgreen)
```

在你的 Markdown 中：

```md
这里是一个提示徽章：{< note />}
```

### 块级短代码

`shortcodes/closure.html`：

```html
<div class="closure">{: .inner :}</div>
```

在你的 Markdown 中：

```md
{< closure >}
这里是一些重要内容。
{</ closure >}
```

内部内容会被放置在模板中的 `{: .inner :}` 位置。

### 带参数的短代码

`shortcodes/say.html`：

```html
<div class="say">{- param.0 -}</div>
```

在你的 Markdown 中：

```md
{< say "Hello, World!" >}
```

## 递归短代码模板

`shortcodes/warning.html`：

```html
<div class="warning">
    {- include "warning-badge" -}
    <div class="content">{: .inner :}</div>
</div>
```

`shortcodes/warning-badge.md`：

```md
![Warning](https://img.shields.io/badge/Warning-Important-red)
```

在你的 Markdown 中：

```md
{< warning >}
这是一个警告信息。
{</ warning >}
```

> 短代码实际上是包含模板的语法糖。`{< note "Hello!" />}` 等价于 `{- include "note" this "Hello" -}`。你也可以直接使用 `include`。
