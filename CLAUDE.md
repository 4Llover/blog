# ljt_4llover - 个人博客

## 项目概述
基于 [Firefly](https://github.com/CuteLeaf/Firefly) 模板搭建的个人博客。
Firefly 是一款基于 Astro 的清新美观静态博客主题，1800+ stars。

## 技术栈
- **框架**: Astro 7 + Svelte 5（交互组件）
- **样式**: Tailwind CSS 4
- **内容**: MDX/Markdown，frontmatter 驱动
- **搜索**: Pagefind（客户端全文搜索）
- **包管理器**: pnpm（必须，项目强制要求）

## 核心命令
```bash
pnpm dev          # 开发服务器 localhost:4321
pnpm build        # 生产构建
pnpm preview      # 预览生产构建
pnpm new-post <filename>  # 新建文章
```

## 项目结构（关键）
```
src/
  config/           # 所有配置文件（站点、导航、侧边栏、评论等）
    siteConfig.ts   # 站点核心配置（标题、描述、语言等）
    navBarConfig.ts # 导航栏
    sidebarConfig.ts# 侧边栏布局
    ...             # 20+ 可配置模块
  content/
    posts/          # 博客文章（.md/.mdx）
    spec/           # 特殊页面（关于、留言板）
    dynamic/        # 微动态
  components/       # 组件（按功能域组织）
  pages/            # 页面路由
  i18n/             # 多语言翻译
```

## 部署
- 开发环境：本地 pnpm dev
- 生产部署：用户有 ESC 云服务器 + 腾讯云域名
- 构建产物：`dist/` 目录（纯静态文件）

## 当前阶段
初始化 — 克隆模板、安装依赖、配置个性化

## 工作流程
1. 克隆 Firefly 模板
2. 安装依赖（pnpm install）
3. 修改 src/config/ 下的配置文件进行个性化
4. 写博客文章到 src/content/posts/
5. 构建部署
