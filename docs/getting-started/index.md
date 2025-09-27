# 开始使用

欢迎使用 Allay 博客引擎！本指南将帮助你快速创建并运行你的第一个 Allay 博客。

## 安装 Allay

首先，你需要安装 Allay。你可以通过以下两种方式获取：

1. **下载预编译版本（推荐）**：访问我们的 https://github.com/PKUSoftwareEngineeringTeam/Allay/releases 获取最新的预编译二进制文件

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

## 博客目录结构

你的 Allay 博客包含以下主要目录和文件：

```
.
├── allay.toml      # 博客配置文件
├── content/         # Markdown 内容文件
├── public/          # 生成的静态文件
├── shortcodes/      # 自定义短代码
├── static/          # 静态资源（图片、PDF等）
└── themes/          # 主题目录
```
简单来说，`content/` 目录用于存放你的博客内容，`static/` 目录用于存放静态资源（如图片），`themes/` 目录用于存放博客主题。更多详情请参见 [文件结构](./file-structure.md)。

## 启动本地服务器

进入你的博客目录，运行以下命令启动本地开发服务器：

```sh
allay server
```

这将：
- 在 `public/` 目录生成静态文件
- 启动本地服务器（默认地址：`http://localhost:8000`）
- 自动检测 `content/` 目录的更改并实时更新

如果端口 8000 已被占用，你可以通过配置指定其他端口。

## 开始创作

现在你可以：
1. 在 `content/` 目录中创建 Markdown 文件来编写博客内容
2. 将图片等静态资源放入 `static/` 目录
3. 通过修改 `allay.toml` 文件来自定义博客配置
4. 在浏览器中查看实时更新

尽情享受你的博客创作之旅吧！