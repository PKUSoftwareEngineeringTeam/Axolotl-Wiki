---
title: Allay 模板
raw: true
---

Allay 使用模板系统来定义博客的外观和布局。模板文件通常采用 HTML 格式，并包含特定的占位符，用于动态插入内容。

如果你仅是博客创作者，通常不需要直接修改模板文件。你可以通过修改配置文件和内容文件来定制博客的外观。

另外，你也许想要学习一些模板语法，以便在内容中使用自定义短代码或变量。那么下面的章节将对你有所帮助。

## 配置文件

Allay 模板的配置文件通常命名为 `theme.toml`，位于主题目录下。该文件定义了主题的基本信息和参数。 例如：

```toml
# Default Allay site configuration
baseUrl = "http://axolotl.wiki"
title = "Axolotl Wiki"
theme = "Axolotl"
description = "Official Axolotl Wiki"
author = "Allay Developer"
[params]
title = "Allay Blog"
```

你可以将theme指定为你想使用的主题名称，该主题应位于 `themes/` 目录下。

## 布局

所有的 Allay 模板都应放在 `templates` 目录下。 有些主题会有多个模板文件：

- `page.html`：常规页面的默认模板。
- `*.html`：更多自定义页面模板。

### 自定义模板布局

并非所有页面都应使用相同的布局。你可以在 front matter 中通过 `template` 字段为每个页面指定不同的模板。例如：

`content/about/index.md`：

```md
---
title: About Me
template: about.html  #(假设templates目录下有about.html)
---

Hello, this is the about page.
```

更多详情请参见[布局](./layout.md)。

### 模板语法

allay有自己独特的语法系统，用于在模板中插入动态内容。你可以使用占位符来引用变量、条件语句和循环等。例如：

```html
<h1>{: .title :}</h1>
{- if .user.logged_in -}
<p>欢迎回来，{: .user.name :}!</p>
{- end -}
```

在此之前，最好了解一下[变量](variables.md)和[作用域](scope.md)的概念。接下来我们将学习allay基本语法。

### 基本语法标记

- `{: 表达式 :}` - 输出表达式的结果
- `{- 命令 -}` - 执行控制命令（条件、循环等）
- `{< 短代码 >}` - 使用功能扩展
- `{{ 原样文本 }}` - 输出不转义的内容

### 快速开始

#### 变量输出

```html
<p>{: .page_title :}</p>
<p>{: $username :}</p>
```

#### 条件判断

```html
{- if .show_content -}
<div>{: .content :}</div>
{- else -}
<p>内容暂不可用</p>
{- end -}
```

#### 循环遍历

```html
<ul>
{- for $item: .items -}
    <li>{: $item.name :}</li>
{- end -}
</ul>
```

#### 包含其他模板

```html
{- include "header.html" -}
<main>主要内容</main>
{- include "footer.html" -}
```

### 核心概念

1. **变量** - 使用`$`前缀定义变量，如`$title`
2. **作用域** - 使用`.`访问当前上下文，如`.user.name`
3. **命令块** - 用`{- -}`包裹控制逻辑
4. **输出块** - 用`{: :}`包裹要显示的内容

这个简明的语法系统让你能轻松创建动态模板，同时保持代码的清晰和可维护性。更多详情请参见[命令和语法](./commands.md)，这个文档的最后还总结了allay所有的语法生成规则，建议仔细阅读。

## 实战

最后我们给出了一个[实战](practice.md)的例子，希望能给用户提供一个参考。
