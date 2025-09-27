# Allay 模板实战：构建主页文章列表

本指南将通过构建一个显示两篇文章的主页，串联讲解 Commands、Layouts、Scope 和 Variables 的实际应用。
非开发用户无需关注涉及templates文件夹的内容。

## 项目结构

```
content/
├── index.md          # 主页内容
├── post-1/
│   └── index.md      # 第一篇文章
└── post-2/
    └── index.md      # 第二篇文章

templates/
├── index.html        # 主页模板
├── base.html         # 基础布局模板
└── components/
    └── post-card.md  # 文章卡片组件
```

## 第一步：创建文章内容

先创建两篇文章，放在 `content/post-1/index.md` 和 `content/post-2/index.md`。

#### 第一篇文章 `content/post-1/index.md`
```markdown
---
title: "Allay 模板系统入门指南"
date: 2024-01-15
description: "学习如何使用 Allay 模板系统创建漂亮的静态网站"
excerpt: "本文介绍了 Allay 模板系统的基本概念和核心功能..."
tags: ["allay", "模板", "入门"]
---

这里是文章的完整内容...
```

#### 第二篇文章 `content/post-2/index.md`
```markdown
---
title: "高级模板技巧与最佳实践"
date: 2024-01-20  
description: "探索 Allay 模板系统的高级功能和性能优化技巧"
excerpt: "深入了解条件渲染、循环优化和模板继承等高级功能..."
tags: ["allay", "高级", "性能"]
---

这里是文章的完整内容...
```

## 第二步：创建基础布局模板

注：非模版开发用户无需关注

`templates/base.html`:

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{: block "title" :}我的博客{: end :}</title>
    <link rel="stylesheet" href="/css/style.css">
</head>
<body>
    <header>
        <h1>我的技术博客</h1>
        <nav>首页 | 关于 | 归档</nav>
    </header>

    <main>
        {: block "content" :}
        <!-- 内容将由子模板填充 -->
        {: end :}
    </main>

    <footer>
        <p>&copy; 2024 我的博客. 使用 Allay 构建.</p>
    </footer>
</body>
</html>
```

## 第三步：创建文章卡片组件

`templates/components/post-card.md`:

```markdown
{--
  文章卡片组件
  接收参数：文章对象 $post
-}
<article class="post-card">
    <h3>{: $post.title :}</h3>
    
    {- if $post.date -}
    <time class="post-date">
        {: format_date $post.date "2006年1月2日" :}
    </time>
    {- end -}
    
    {- if $post.description -}
    <p class="post-description">
        {: truncate $post.description 25 :}...
    </p>
    {- end -}
    
    {- if $post.tags -}
    <div class="post-tags">
        {- for $tag: $post.tags -}
        <span class="tag">{: $tag :}</span>
        {- end -}
    </div>
    {- end -}
    
    <a href="{: $post.url :}" class="read-more">阅读全文</a>
</article>
```

## 第四步：创建主页模板

`templates/index.html`:

```html
{- extends "base.html" -}

{: block "title" :}
最新文章 - 我的博客
{: end :}

{: block "content" :}
<section class="hero">
    <h2>欢迎访问我的博客</h2>
    <p>这里分享技术知识和学习心得</p>
</section>

<section class="recent-posts">
    <h2>最新文章</h2>
    
    {- set $recent_posts (slice site.Pages 0 2) -}
    
    {- if $recent_posts -}
    <div class="posts-grid">
        {- for $post: $recent_posts -}
        {- include "components/post-card.md" $post -}
        {- end -}
    </div>
    {- else -}
    <p>暂无文章，敬请期待...</p>
    {- end -}
</section>

<section class="blog-stats">
    <h3>博客统计</h3>
    <p>总共 {: len site.Pages :} 篇文章</p>
    
    {- set $all_tags (list) -}
    {- for $post: site.Pages -}
        {- if $post.tags -}
            {- for $tag: $post.tags -}
                {- set $all_tags (append $all_tags $tag) -}
            {- end -}
        {- end -}
    {- end -}
    
    <p>总共 {: len $all_tags :} 个标签</p>
</section>
{: end :}
```

## 第五步：创建主页内容

`content/index.md`:

```markdown
---
title: "欢迎来到我的技术博客"
description: "分享编程知识、技术教程和学习资源"
template: index.html
---

这里的内容不会被显示，因为使用了自定义模板。
但 front matter 中的元数据可以在模板中通过 `.title` 和 `.description` 访问。
```

## 功能解析

### 1. Scope（作用域）应用
- **全局作用域**: `site.Pages` 访问所有页面
- **页面作用域**: `$post.title`, `$post.date` 访问文章属性
- **局部作用域**: `$recent_posts`, `$all_tags` 局部变量

### 2. Commands（命令）使用
```html
{- set $recent_posts (slice site.Pages 0 2) -}  <!-- 设置变量 -->
{- for $post: $recent_posts -}                  <!-- 循环遍历 -->
{- if $post.tags -}                            <!-- 条件判断 -->
{- include "components/post-card.md" $post -}   <!-- 包含组件 -->
{- end -}                                       <!-- 结束块 -->
```

### 3. Variables（变量）操作
```html
{: $post.title :}                          <!-- 直接输出 -->
{: format_date $post.date "2006年1月2日" :} <!-- 函数处理 -->
{: truncate $post.description 25 :}        <!-- 文本截断 -->
{: len site.Pages :}                       <!-- 获取长度 -->
```

### 4. Layouts（布局）管理

- **基础布局**: `base.html` 提供整体页面结构
- **模板继承**: `index.html` 继承并重写内容块
- **组件化**: `post-card.md` 可重用的文章卡片

详细用法请参见：

- [Commands 指令详解](./commands.md)
- [Scope 作用域详解](./scope.md)
- [Variables 变量详解](./variables.md)
- [Layouts 布局详解](./layouts.md)

## 最终渲染结果

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>最新文章 - 我的博客</title>
    <link rel="stylesheet" href="/css/style.css">
</head>
<body>
    <header>
        <h1>我的技术博客</h1>
        <nav>首页 | 关于 | 归档</nav>
    </header>

    <main>
        <section class="hero">
            <h2>欢迎访问我的博客</h2>
            <p>这里分享技术知识和学习心得</p>
        </section>

        <section class="recent-posts">
            <h2>最新文章</h2>
            <div class="posts-grid">
                <article class="post-card">
                    <h3>Allay 模板系统入门指南</h3>
                    <time class="post-date">2024年1月15日</time>
                    <p class="post-description">学习如何使用 Allay 模板系统创建漂亮的静态网站...</p>
                    <div class="post-tags">
                        <span class="tag">allay</span>
                        <span class="tag">模板</span>
                        <span class="tag">入门</span>
                    </div>
                    <a href="/post-1/" class="read-more">阅读全文</a>
                </article>
                
                <article class="post-card">
                    <h3>高级模板技巧与最佳实践</h3>
                    <time class="post-date">2024年1月20日</time>
                    <p class="post-description">探索 Allay 模板系统的高级功能和性能优化技巧...</p>
                    <div class="post-tags">
                        <span class="tag">allay</span>
                        <span class="tag">高级</span>
                        <span class="tag">性能</span>
                    </div>
                    <a href="/post-2/" class="read-more">阅读全文</a>
                </article>
            </div>
        </section>

        <section class="blog-stats">
            <h3>博客统计</h3>
            <p>总共 3 篇文章</p>
            <p>总共 6 个标签</p>
        </section>
    </main>

    <footer>
        <p>&copy; 2024 我的博客. 使用 Allay 构建.</p>
    </footer>
</body>
</html>
```

这个实战示例展示了如何将 Allay 模板系统的各个功能模块有机结合，创建一个功能完整、结构清晰的博客主页。
