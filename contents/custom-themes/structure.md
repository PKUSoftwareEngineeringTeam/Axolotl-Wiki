---
title: 主题文件结构
raw: true
---

## 文件结构

你的主题应按照特定的目录结构组织，以确保 Allay 引擎能够正确定位并应用你的自定义样式。以下是主题文件所需的结构：

```
.
├── allay.toml   # 可选的主题配置文件
├── assets       # 存放图片、字体、CSS、JavaScript 等资源的目录
├── i18n         # 存放本地化文件的目录
├── pages        # 页面文件目录
│   ├── 404.html        # 404 错误页模板
│   ├── index.html      # 主页模板
│   └── page.html       # 普通页面模板
├── templates   # HTML 模板目录
└── theme-meta.toml  # 主题元数据文件
```

`allay.toml` 文件是可选的，但如果你希望为主题用户提供默认配置参数，建议添加。

`theme-meta.toml` 文件是必需的，它包含主题的元数据，使 Allay 引擎能够识别你的主题。以下是 `theme-meta.toml` 文件的示例：

```toml
# Allay 主题的 theme-meta 模板

name = "Axolotl"
license = "GPL-3.0-only"
licenselink = "https://www.gnu.org/licenses/gpl-3.0-standalone.html"
description = "Allay 官方主题"
homepage = "https://github.com/PKUSoftwareEngineeringTeam/Axolotl"
demosite = "https://github.com/PKUSoftwareEngineeringTeam/Axolotl-Wiki"

tags = ["clean", "light", "personal"]
min_version = "0.1.0"

[author]
name = "LeoDreamer"
homepage = "https://leodreamer2004.github.io"
```
