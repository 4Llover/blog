---
title: "小黑的宝藏 — 博客搭建记录"
published: 2026-08-13
description: "记录使用 Firefly 主题模板搭建个人博客的完整过程，包括选型、配置、部署和内容迁移。"
tags: [Astro, 博客, Firefly, Web开发, Vercel]
category: 开发日志
pinned: true
---

一直想搭建一个属于自己的个人博客，用来记录生活、分享技术、整理收藏。经过一番调研，最终选择了 Firefly 主题模板。

## 为什么选 Firefly

选主题时考虑了几个因素：

1. **好看** — 第一印象很重要，Firefly 的设计清新简洁
2. **技术栈现代** — 基于 Astro 7 + Svelte 5 + Tailwind CSS 4
3. **功能丰富** — 支持微动态、相册、书签导航、评论系统等
4. **高度可定制** — 25+ 个配置模块，几乎每个细节都能调

对比了几个主流方案：
- **Hugo** — 快但模板语言学习成本高
- **Hexo** — 生态成熟但主题偏旧
- **NotionNext** — 好看但不够灵活
- **Firefly** — 现代技术栈 + 好看 + 功能全 → 就它了

## 技术架构

```
Astro 7 (框架)
├── Svelte 5 (交互组件)
├── Tailwind CSS 4 (样式)
├── Markdown/MDX (内容)
└── Vercel (部署)
```

- **内容管理**: Obsidian (Vault = 项目根目录)
- **版本控制**: Git + GitHub
- **部署**: Vercel (git push 自动部署)
- **域名**: www.blackboytreasure.cn

## 搭建过程

### 1. 克隆模板

```bash
git clone https://github.com/CuteLeaf/Firefly.git
cd Firefly
pnpm install
```

### 2. 修改配置

核心配置在 `src/config/` 目录下，主要改了：
- `siteConfig.ts` — 站点名称、描述、URL
- `profileConfig.ts` — 个人信息和社交链接
- `navBarConfig.ts` — 导航栏结构
- `backgroundWallpaper.ts` — 背景壁纸和横幅

### 3. 部署到 Vercel

安装 Vercel 适配器：

```bash
pnpm add @astrojs/vercel
```

配置 `astro.config.mjs`：

```js
import vercel from '@astrojs/vercel/static';
export default defineConfig({
  adapter: vercel(),
});
```

然后连接 GitHub 仓库，Vercel 会自动构建和部署。

### 4. 配置自定义域名

在 Vercel Dashboard 添加域名 `www.blackboytreasure.cn`，然后在腾讯云 DNS 添加：
- A 记录：`@` → `76.76.21.21`
- CNAME 记录：`www` → `cname.vercel-dns.com`

## 使用体验

Firefly 的配置系统做得很好，几乎不需要改代码就能定制大部分功能。Obsidian 集成也很方便，写文章就像写笔记一样自然。

目前博客支持的功能：
- 博客文章（Markdown/MDX）
- 微动态
- 相册
- 书签导航
- 旅行地图
- 分类/标签/归档
- 搜索（PageFind）

后续可能会开启评论系统和友链页面。

## 致谢

- [Firefly](https://github.com/CuteLeaf/Firefly) — 博客主题模板
- [Astro](https://astro.build/) — 站点框架
- [Vercel](https://vercel.com/) — 部署平台

---

这篇既是博客的第一篇文章，也是搭建过程的记录。希望这个博客能一直更新下去。
