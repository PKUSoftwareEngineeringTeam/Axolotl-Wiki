---
title: 快速开始
raw: true
---

欢迎使用 Allay 博客引擎！本指南将帮助你快速创建并运行你的第一个 Allay 博客。

## 安装 Allay

首先，你需要安装 Allay。你可以通过以下两种方式获取：

1. **下载预编译版本（推荐）**：访问我们的 <https://github.com/PKUSoftwareEngineeringTeam/Allay/releases> 获取最新的预编译二进制文件

2. **从源码构建**：

   ```sh
   # 克隆仓库
   git clone https://github.com/PKUSoftwareEngineeringTeam/Allay
   
   # 构建项目
   cd Allay
   cargo build --release
   
   # 验证安装
   ./target/release/allay --version
   ```

建议将可执行文件添加到系统 PATH 中以便全局使用。

## 安装allay插件

如果你使用的是vscode编辑器，强烈建议安装allay插件以获得更好的编辑体验。请按照以下步骤操作：

### （Todo）

## 初始化

现在，在命令行新建一个文件夹存放你的博客，然后输入

```sh
allay new
allay init
```

## 博客目录结构

现在，你的 Allay 博客包含以下主要目录和文件：

```
.
├── allay.toml      # 博客配置文件
├── contents/         # Markdown 内容文件
├── public/          # 生成的静态文件
├── shortcodes/      # 自定义短代码
├── static/          # 静态资源（图片、PDF等）
└── themes/          # 主题目录
```

简单来说，`contents/` 目录用于存放你的博客内容，`static/` 目录用于存放静态资源（如图片），`themes/` 目录用于存放博客主题。更多详情请参见 [文件结构](./file-structure)。

## 选择你的主题

allay支持用户创作自己的主题，同时也提供一套官方的主题以供选择。我们先从官方主题开始。

```sh
cd themes
#  选择官方主题
git clone https://github.com/PKUSoftwareEngineeringTeam/Axolotl.git
```

## 启动本地服务器

好了，万事具备！让我们启动allay引擎！

进入你的博客目录，运行以下命令启动本地开发服务器：

```sh
allay server
```

我们的本地服务器现已启动！

---
这将：

- 在 `public/` 目录生成静态文件
- 启动本地服务器（默认地址：`http://localhost:8000`）
- 自动检测 `content/` 目录的更改并实时更新

如果端口 8000 已被占用，你可以通过配置指定其他端口。

---

当然，如果你已经安装了vscode插件，你可以点击右上角的眼睛图标，直接在vscode中启动本地服务器，并预览博客效果。

## 开始创作

现在你可以：

1. 在 `content/` 目录中创建 Markdown 文件来编写博客内容
2. 将图片等静态资源放入 `static/` 目录
3. 通过修改 `allay.toml` 文件来自定义博客配置
4. 在浏览器/vscode中查看实时更新

尽情享受你的博客创作之旅吧！

## More....

如果你想要了解更多allay“隐藏”语法，请阅读[allay模版](../allay-template/)

如果你想要学习如何更好的创建和管理自定义内容，请阅读[自定义内容](../custom-contents/)

如果你是我们的高阶用户，想要创作自己的主题，请阅读[自定义主题](../custom-themes/)
