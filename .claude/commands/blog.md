# 小黑的宝藏 - 博客工作流技能

你正在管理「小黑的宝藏」个人博客项目。以下是完整的工作上下文和操作规范。

## 项目基本信息

- **项目路径**: C:\Users\blackboy\Desktop\ljt_4llover
- **GitHub 仓库**: https://github.com/4Llover/blog
- **部署平台**: Vercel（自动部署，推代码即上线）
- **线上域名**: https://www.blackboytreasure.cn
- **GitHub 账号**: 4Llover（gh auth 已持久化在系统密钥环，无需重新登录）
- **技术栈**: Astro 7 + Svelte 5 + Tailwind CSS 4 + @astrojs/vercel
- **内容编辑器**: Obsidian（Vault 路径即项目根目录）

## 技术架构

```
写文章(Markdown) → pnpm build 编译 → dist/ 纯静态文件 → Vercel 托管
       ↑                                              ↑
   Obsidian编辑                              git push 自动触发
```

- 静态博客：无数据库，所有内容编译为 HTML
- Astro 框架：Markdown 编译成网页
- Svelte：交互组件（搜索、设置面板等）
- Pagefind：客户端全文搜索

## 核心目录结构

```
src/
  config/                    ← 网站配置（改这里自定义网站）
    siteConfig.ts            站点名称、描述、语言、分页
    profileConfig.ts         头像、签名、社交链接
    navBarConfig.ts          导航栏菜单
    backgroundWallpaper.ts   壁纸、横幅文字
    sidebarConfig.ts         侧边栏布局
    fontConfig.ts            字体配置
    effectsConfig.ts         动画特效（樱花等）
    musicConfig.ts           音乐播放器
    commentConfig.ts         评论系统
    ...                      共 25 个配置模块
  content/
    posts/                   ← 博客文章（.md/.mdx）
    spec/                    ← 特殊页面（关于页等）
    dynamic/                 ← 微动态（类似朋友圈）
  components/                ← 页面组件
  pages/                     ← 路由
  i18n/                      ← 多语言翻译
public/
  assets/images/             ← 图片资源
  favicon/                   ← 网站图标
dist/                        ← 编译产物（git忽略）
.obsidian/                   ← Obsidian配置
  templates/                 ← 写作模板
docs/使用指南.md              ← 项目使用文档
```

## 博客文章规范

### 文件位置
`src/content/posts/你的文章名.md`

### Frontmatter 格式（必须）
```yaml
---
title: "文章标题"
published: 2026-08-12
description: "一句话描述，显示在文章列表"
tags: [标签1, 标签2]
category: 分类名
image: ./images/封面图.jpg   # 可选，显示在文章列表卡片
draft: false                 # true=草稿不发布, false=发布
pinned: false                # true=置顶
---
```

### 文章正文
标准 Markdown 语法，支持：
- 标题、列表、引用、代码块
- 图片：`![描述](图片路径)`（图片放同目录或 public/assets/images/）
- 提示框：`> [!note] 标题` / `> [!tip] 标题` / `> [!warning] 标题`
- 数学公式：`$行内公式$` / `$$块级公式$$`
- Mermaid 图表
- GitHub 卡片：`::github{repo="用户名/仓库名"}`

### 微动态
`src/content/dynamic/文件名.md`
```yaml
---
published: 2026-08-12
location: 所在地（可选）
---
内容正文
```

## 常用操作命令

### 本地开发预览
```bash
pnpm dev           # 启动开发服务器 localhost:4321
pnpm build         # 生产编译
pnpm preview       # 预览生产构建
```

### 新建文章
```bash
pnpm new-post 文章文件名    # 自动在 src/content/posts/ 创建模板
```

### 发布流程（推送到 GitHub → Vercel 自动部署）
```bash
# 配置变更时先本地验证
pnpm build

git add -A
git commit -m "feat: 描述你做了什么"
git push
```

推送后检查 Vercel Dashboard 确认部署状态为 Ready。

### Git 提交规范
- `feat:` 新功能/新文章
- `fix:` 修复问题
- `chore:` 配置/维护
- `docs:` 文档更新
- `style:` 样式调整

## 自动化发布流程

当用户要求发布/推送/上线时，执行：
1. `git add -A`
2. `git status` 检查变更
3. `git commit -m "合适的提交信息"`
4. `git push origin main`
5. 告诉用户：已推送，Vercel 会在 2-3 分钟内自动重新部署

## Obsidian 集成

- Vault 路径：项目根目录
- 模板位置：`.obsidian/templates/`
- 新建文章快捷键：Ctrl+P → Templater → 选择模板
- 图片附件目录：`public/assets/images/obsidian-attachments/`
- 文章管理面板：`src/content/spec/文章管理面板.md`（Dataview 查询）

## 网站个性化速查

| 想改什么 | 修改哪个文件 |
|---|---|
| 网站名称/描述 | src/config/siteConfig.ts |
| 头像/签名 | src/config/profileConfig.ts |
| 导航菜单 | src/config/navBarConfig.ts |
| 壁纸/横幅文字 | src/config/backgroundWallpaper.ts |
| 侧边栏布局 | src/config/sidebarConfig.ts |
| 主题色 | siteConfig.ts 的 themeColor.hue (0-360) |
| 字体 | src/config/fontConfig.ts |
| 动画特效 | src/config/effectsConfig.ts |
| 音乐播放器 | src/config/musicConfig.ts |
| 评论系统 | src/config/commentConfig.ts |

## 线上域名配置

- **主域名**: `www.blackboytreasure.cn`
- **根域名**: `blackboytreasure.cn`（跳转到 www）
- **site_url**: `src/config/siteConfig.ts` 必须与线上域名一致，否则所有链接和 SEO 标签失效
- Vercel Dashboard: 项目 → Settings → Domains 查看和管理域名

## 注意事项

- pnpm 是必须的包管理器（项目有 preinstall 检查）
- Node.js >= 22
- **push 前务必 `pnpm build` 验证构建**，否则 Vercel 构建失败线上会回滚到旧版本
- `site_url` 改动后必须同步更新，不一致会导致全站链接404
- dist/ 目录是编译产物，不需要提交到 Git
- 本地预览修改即时生效（热更新）
- Vercel 部署是自动的，每次 push 触发
- GitHub 认证已持久化，新会话无需重新登录
