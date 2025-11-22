---
template: "about.html" 
hidden: true
friends:
    - url: "https://github.com/"
      name: "GitHub"
      intro: "世界软件由此而起"
    - url: "https://gohugo.io"
      name: "Hugo"
      intro: "快速且灵活的静态网站生成器，本引擎的灵感来源"
    - url: "https://rust-lang.org"
      name: "Rust"
      intro: "安全且高效的系统编程语言"
---

# Building the Future of Static Blogging.

---

## 🚀 About Us & Our Mission

We are an open-source development team dedicated to creating simple, modern, and high-performance tools for content creators and developers.

Our core mission is to simplify the process of publishing beautiful personal blogs by leveraging modern technologies like **Rust** and **Markdown**. We strive to make blogging effortless and highly customizable.

---

## ✨ Our Core Projects

Here are the main projects and open-source assets maintained by our organization:

### 1. Allay Engine

**A simple, highly configurable static site generator written in Rust.**

Allay transforms your Markdown files into production-ready static HTML websites, focusing on speed and developer experience.

## 🔑 Key Features of Allay

* **Markdown First:** Write all your content using **Markdown** and optional **Front-matter** metadata (YAML or TOML supported) for configuration.
* **Fast by Design:** Built on **Rust** for superior performance and concurrency.
* **Flexible Templating:** Use custom commands (`for`, `if`, `with`, `set`) and substitutions to build sophisticated layouts and dynamic pages.
* **Shortcodes & Includes:** Easily embed reusable and dynamic content blocks within your Markdown using **Shortcodes**.
* **Live Preview:** Develop with the built-in development server (`allay server`) which supports hot-reloading for immediate feedback on changes.
* **Customizable Layouts:** Assign specific layouts (templates) to individual pages directly from the page's Front-matter.

---

## 💡 Get Started

To create your first blog with Allay, follow these quick steps:

1. **Install Allay:** Follow the instructions on the [Allay Engine GitHub Releases page](https://github.com/PKUSoftwareEngineeringTeam/Allay/releases) or build from source.

2. **Initialize Your Site:**

   ```bash
   allay new <my-blog-name>
   cd <my-blog-name>
   ```

3. **Start Developing:**

   ```bash
   allay server
   ```

   Your blog will be available locally at `http://localhost:8000`.

🔗 **Full Documentation:** [Read the full User Documentation](https://pkusoftwareengineeringteam.github.io/Axolotl-Wiki/)

---

## 👋 Community & Contribution

We welcome contributions from everyone! Whether you are looking to fix a bug, suggest a new feature, or improve documentation, your help is appreciated.

* **Report Issues:** Found a bug or have a feature idea for the Engine, Theme, or Extension? Please open an issue on the relevant repository's **[Issue Tracker]** (e.g., [Allay Engine Issues](https://github.com/PKUSoftwareEngineeringTeam/Allay/issues)).
* **Developers:** Start with the [Developer Documentation](https://github.com/PKUSoftwareEngineeringTeam/Allay/blob/main/doc/dev/developer-guide.md) to understand the project structure and best practices.
