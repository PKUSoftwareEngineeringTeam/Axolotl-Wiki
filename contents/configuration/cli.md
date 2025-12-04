---
title: 命令行工具
raw: true
date: 2025-11-21
group: 配置
description: 有关 Allay 命令行工具的使用说明
tags: ["Allay 配置", "CLI"] 
---

allay 命令行工具是管理和构建 Allay 博客的主要方式，并提供了一些自定义选项。以下是常用命令及其说明：

```bash
allay [COMMAND] [OPTIONS]
```

### 全局参数

- `-h`, `--help`：显示帮助信息
- `-V`, `--version`：显示版本信息
- `-r`, `--root <PATH>`：指定博客根目录，默认为当前目录
- `--online`：启用在线模式，此时会读取 `allay.toml` 中的 `base_url` 作为站点根 URL。此特性主要用于处理网站绝对路径 `href="/foo/bar` 的路由问题。

### 子命令

- `new/init`：创建一个新的 Allay 博客项目

  ```bash
  allay init
  allay new <path>
  ```

  `allay init` 相当于在当前目录执行 `allay new .`。默认方式下，CLI 会询问用户是否要自动下载并应用默认主题。如果你希望跳过交互式提示，可以使用 `--skip-theme` 参数。

- `build`：构建博客，生成静态文件

  ```bash
  allay build
  ```
  
- `serve`：启动本地开发服务器，支持热重载

  ```bash
  allay serve
  ```

  - `-p`, `--port <PORT>`：指定服务器端口，默认为 `8000`
  - `-a`, `--address <ADDRESS>`：指定服务器地址，默认为 `127.0.0.1`
  - `--open`：启动服务器后自动在浏览器中打开站点
