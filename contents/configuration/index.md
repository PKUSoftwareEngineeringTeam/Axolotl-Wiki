---
title: Allay 配置指南
raw: true
date: 2025-11-21
group: 配置
description: 配置你的 Allay 博客以满足你的需求
tags: ["Allay 配置", "博客设置", "自定义"]
---

Allay 可以通过在站点根目录放置一个 `allay.toml` 文件进行配置。该文件允许你设置各种参数，以控制站点的行为和外观。

配置文件是全局的，会影响整个站点。

可用的配置选项包括：

- `baseUrl`：你的网站的基础 URL。
- `title`：你的网站标题。
- `theme`：你的网站所使用的主题。
- `params`：可在模板中访问的自定义参数表。

默认的配置如下：

```sh
# Default Allay site configuration
baseUrl = "http://axolotl.wiki"
title = "Axolotl Wiki"
theme = "Axolotl"
description = "Official Axolotl Wiki"
author = "Allay Developer"
[params]
title = "Allay Blog"
```

自定义的参数列表的变量名可以与[params]上面的重复。这些参数是你博客的全局参数。比如，你可以这样写：

```sh
# allay.toml
...(默认配置)
author = 张三
```

```sh
# 自我介绍.md
我的名字叫{:site.title:},...
```

这样，一些你经常用到的数据就可以存储在配置文件中。
