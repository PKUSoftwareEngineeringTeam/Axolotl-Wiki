## 创建页面

你可以通过将 Markdown 文件添加到 `content` 目录，在 Allay 中创建自定义页面。当你运行 `allay build` 或 `allay server` 命令时，每个 Markdown 文件都会被转换为静态 HTML 页面。

所有 Markdown 文件都应在文件顶部包含 front-matter 元数据。关于可用的元数据字段，请参见 [Front-matter](./front-matter.md)。

## 文件组织

除非在 front-matter 中指定了 "url" 字段，否则页面的 URL 会根据文件路径自动生成。需要注意的是，文件名为 `index.md` 的文件具有特殊意义，它会被视为该目录的根页面。

例如，以下文件结构：

```
content
├── about.md
├── blog
│   ├── index.md
│   └── first-post.md
└── projects
    └── project1.md
```

生成的 `public` 目录下的 HTML 文件为：

```
public
├── about.html          # 来自 about.md
├── blog
│   ├── index.html      # 来自 blog/index.md
│   └── first-post.html # 来自 blog/first-post.md
└── projects
    └── project1.html   # 来自 projects/project1.md
```
