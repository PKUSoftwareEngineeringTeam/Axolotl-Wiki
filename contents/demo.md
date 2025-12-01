---
title: Allay 展示
description: 我们是简单易用的 Allay 引擎！
tags: ["Demo", "Vue", "前端开发", "JavaScript"]
raw: true
date: 2025-11-30
---

以下内容展示了 Markdown 下常见的语法渲染效果。

## Vue 前端开发

**Vue** 是一个用于构建用户界面的渐进式 JavaScript 框架。它专注于通过声明式渲染和组件化开发来简化前端开发过程。

> **为什么选择 Vue？**
>
> Vue 的核心库只关注视图层，易于上手，并与其他库或现有项目进行整合。它采用虚拟 DOM 技术，提高了渲染性能。
>
> *"Vue 的设计理念是渐进式 - 你可以从一个简单的功能开始，逐步扩展到完整的应用。"* — Vue 官方团队

### 🎯 Vue 版本对比

我们这里进行一组对比：

| 特性 | Vue 2.x | Vue 3.x |
|------|---------|---------|
| **API 风格** | 选项式 API | 组合式 API |
| **路由** | Vue Router 3 | Vue Router 4 |
| **状态管理** | Vuex 3 | Vuex 4 / Pinia |
| **浏览器支持** | 支持 IE9+ | 不支持 IE |
| **包大小** | ~20KB | ~10KB (gzipped) |

### ✨ Vue 核心特性

1. **声明式渲染**
   - 模板语法简洁易懂
   - 数据绑定自动更新
   - 条件渲染和列表渲染

2. **组件系统**
   - 可复用的 UI 组件
   - 单向数据流
   - 组件间通信

3. **生态系统**
   - Vue Router - 官方路由
   - Vuex/Pinia - 状态管理
   - Vue DevTools - 开发调试

### 📝 示例代码

你可以用 `{{` 和 `}}` 来插入代码块：

```html
<template>
    <div class="vue-demo">
        <h1 :class="{ active: isActive }">{{ message }}</h1>
        <button @click="handleClick" :disabled="isLoading">
            {{ isLoading ? '加载中...' : '点击我' }}
        </button>
        <ul v-if="items.length">
            <li v-for="item in items" :key="item.id">
                {{ item.name }}
            </li>
        </ul>
        <p v-else>暂无数据</p>
    </div>
</template>

<script>
export default {
    data() {
        return {
            message: "Hello, Vue!",
            isActive: true,
            isLoading: false,
            items: [
                { id: 1, name: 'Vue 2' },
                { id: 2, name: 'Vue 3' },
            ]
        };
    },
    methods: {
        async handleClick() {
            this.isLoading = true;
            await new Promise(resolve => setTimeout(resolve, 1000));
            this.message = "操作完成！";
            this.isLoading = false;
        }
    },
    mounted() {
        console.log('组件已挂载');
    }
};
</script>

<style scoped>
.vue-demo {
    padding: 20px;
    max-width: 600px;
    margin: 0 auto;
}
</style>
```

### 🚀 快速开始

#### 安装 Vue

```bash
# 使用 npm
npm install vue@next

# 使用 yarn
yarn add vue@next

# 使用 CDN
<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
```

### 📚 学习资源

- [Vue 官方文档](https://vuejs.org/) - 最权威的学习资料
- [Vue Mastery](https://www.vuemastery.com/) - 视频教程
- [Vue School](https://vueschool.io/) - 互动课程

### 🎓 学习路径

- [x] 了解 Vue 基础概念
- [x] 学习模板语法和数据绑定
- [ ] 掌握组件开发
- [ ] 学习状态管理
- [ ] 掌握路由配置
- [ ] 学习性能优化

(勾选框不会被渲染为交互式元素)

---

**Vue** 的流行度持续增长，根据 2024 年前端框架调研<sup>[1]</sup>，Vue 在开发者满意度中排名前列。

*Vue 3 的性能提升主要体现在：*

- ~55% 更快的渲染速度
- ~45% 更小的包大小
- 更好的 TypeScript 支持

---

*本文档使用 Allay 引擎渲染，展示了 Markdown 的各种语法特性。*

<small>参考文献: [1] State of JS 2024 Survey</small>

**Happy Coding!** 🎉
