---
title: 指令
raw: true
description: Allay 模板引擎的语法和使用方法详解
tags: ["Allay 功能", "模板", "语法"]
date: 2025-11-27
group: Allay 模板
---

## 基本语法

在 Allay 模板中，使用以下标记：

- `{- -}`：命令块，用于控制流程
- `{: :}`：表达式块，用于输出内容
- `{< >}`：短代码块，用于扩展功能
- `{% %}`：注释块，用于添加注释
- `{{ }}`：不转义文本块，用于原样输出。也可以在 [front-matter](../custom-contents/front-matter) 添加字段 `raw: true` 来禁用整个文件的转义。

所有表达式块都会被求值并替换为其结果。

## 变量和表达式

### 变量定义和使用

```html
{- set $name = "Allay" -}
{- set $count = 10 -}
{: $name :} <!-- 输出: Allay -->
{: $count + 5 :} <!-- 输出: 15 -->
```

### 字段访问

```html
{- set $user = .current_user -}
{: $user.name :}        <!-- 访问 name 字段 -->
{: $user.profile.age :} <!-- 嵌套字段访问 -->
{: .title :}            <!-- 访问当前作用域的 title 字段 -->
```

### 表达式支持

Allay 支持丰富的表达式：

```html
<!-- 算术运算 -->
{: 10 + 5 :}     <!-- 15 -->
{: $price * 1.1 :} <!-- 价格加 10% -->

<!-- 比较运算 -->
{- if $score >= 60 -}及格{- end -}
{- if $name == "admin" -}管理员{- end -}

<!-- 逻辑运算 -->
{- if $logged_in && $is_admin -}欢迎管理员{- end -}
{- if !$visible -}隐藏内容{- end -}

<!-- 字符串操作 -->
{: "Hello " + $name + "!" :}
```

## 控制流程命令

### `set` - 变量赋值

在当前作用域创建或修改变量。

```html
{- set $title = .page_title -}
{- set $count = $count + 1 -}
{- set $full_name = $first_name + " " + $last_name -}
<h1>{: $title :}</h1>
```

### `for` - 循环遍历

遍历列表或集合，支持索引变量。

```html
<!-- 基本遍历 -->
<ul>
    {- for $item: .products -}
    <li>{: $item.name :} - ${: $item.price :}</li>
    {- end -}
</ul>

<!-- 带索引的遍历 -->
<ol>
    {- for $product, $index: .products -}
    <li>{: $index + 1 :}. {: $product.name :}</li>
    {- end -}
</ol>
```

### `if` / `else` - 条件判断

根据条件渲染不同内容。

```html
<!-- 简单条件 -->
{- if .user.is_admin -}
<button>管理面板</button>
{- end -}

<!-- 条件分支 -->
{- if .score >= 90 -}
<p>优秀</p>
{- else if .score >= 60 -}
<p>及格</p>
{- else -}
<p>不及格</p>
{- end -}

<!-- 复杂条件 -->
{- if .user.logged_in && (.user.role == "admin" || .user.role == "editor") -}
<p>欢迎，{: .user.name :}</p>
{- end -}
```

### `with` - 作用域切换

进入对象的作用域，简化字段访问。

```html
<!-- 不使用 with -->
{: .article.author.name :}
{: .article.author.email :}

<!-- 使用 with 简化 -->
{- with .article.author -}
<p>作者: {: .name :}</p>
<p>邮箱: {: .email :}</p>
{- end -}

<!-- 如果 with 对象不存在，则跳过渲染 -->
{- with .not_exist_field -}
<p>不会渲染此内容</p>
{- end -}
```

## 模板组织和复用

### `include` - 模板包含

包含其他模板文件，支持参数传递。`include` 默认在主题的 `templates` 目录下查找模板文件，`.html` 后缀可省略。有关作用域的传递，请参看 [作用域](./scope)。

```html
<!-- 包含头部模板，使用当前作用域 -->
{- include "header.html" -}

<!-- 包含文章模板，传递特定作用域和参数 -->
{- include "components/article" .current_article "特色文章" -}
```

在被包含的模板中，使用 `param` 访问传递的参数：

```html
<!-- components/article.html -->
<article class="article">
    <h2>{: .title :}</h2>
    <div class="meta">{: param.0 :}</div> <!-- 显示 "特色文章" -->
    <div class="content">{: .content :}</div>
</article>
```

### 短代码系统

短代码与 `include` 功能类似。用于扩展模板功能，请参看 [短代码](../extra-functions/shortcode)。

## 特殊变量和作用域

### 内置变量

```html
{: this :}        <!-- 当前作用域对象 -->
{: site.title :}  <!-- 站点全局变量 -->
{: pages :}       <!-- 页面集合 -->
{: param.0 :}     <!-- 第一个参数 -->
{: param.1 :}     <!-- 第二个参数 -->
```

### 作用域规则

```html
<!-- 全局作用域 -->
{- set $global_var = "可在任何地方访问" -}

<!-- 循环内的作用域 -->
{- for $item: .items -}
    {- set $local_var = "只在循环内有效" -}
    {: $local_var :} <!-- 正常 -->
{- end -}
{: $local_var :} <!-- 错误，变量不存在 -->

<!-- with 块内的修改 -->
{- with .user -}
    {- set $temp = .name -} <!-- 不影响原对象 -->
{- end -}
```
