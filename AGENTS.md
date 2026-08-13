# AGENTS.md — 小黑的宝藏 博客项目

## 这是什么项目

「小黑的宝藏」是一个个人博客网站，基于 Firefly (Astro 7) 模板搭建。
- **GitHub 仓库**: https://github.com/4Llover/blog
- **部署平台**: Vercel（推代码自动部署，免费）
- **GitHub 账号**: 4Llover（gh auth 已持久化在 Windows 系统密钥环，新会话无需重新登录）
- **博客主人**: 小黑，签名：美满伴我

## 技术栈

| 技术 | 作用 |
|---|---|
| Astro 7 | 博客框架，把 Markdown 编译成网页 |
| Svelte 5 | 交互组件（搜索、设置面板等） |
| Tailwind CSS 4 | 样式系统 |
| Markdown/MDX | 写文章的格式 |
| Pagefind | 客户端全文搜索 |
| pnpm | 包管理器（项目强制要求，有 preinstall 检查） |
| Obsidian | 本地编辑器（Vault 就是项目根目录） |

## 项目结构

```
src/
  config/               ← 25 个配置模块（改这里自定义网站外观和功能）
    siteConfig.ts         站点名称、描述、语言、分页、主题色
    profileConfig.ts      头像、签名、社交链接
    navBarConfig.ts       导航栏菜单项
    backgroundWallpaper.ts 壁纸模式、横幅文字
    sidebarConfig.ts      侧边栏布局
    commentConfig.ts      评论系统
    effectsConfig.ts      动画特效
    musicConfig.ts        音乐播放器
    fontConfig.ts         字体选择
    ...                   其余 16 个模块见 src/config/index.ts
  content/
    posts/              ← 博客文章（.md/.mdx 文件）
    spec/               ← 特殊页面（关于页、文章管理面板）
    dynamic/            ← 微动态（类似朋友圈）
  components/           ← 页面组件
  pages/                ← 路由
  plugins/              ← Markdown/HTML 插件
  i18n/                 ← 多语言翻译
public/
  assets/images/        ← 图片资源
  favicon/              ← 网站图标
dist/                   ← 编译产物（git 忽略，不需要手动管）
.obsidian/              ← Obsidian 编辑器配置
  templates/            ← 写作模板（Templater）
docs/使用指南.md         ← 项目使用文档
```

## 常用命令

```bash
pnpm dev                # 启动本地开发服务器 localhost:4321
pnpm build              # 生产编译（生成 dist/）
pnpm preview            # 预览生产构建
pnpm check              # TypeScript 检查
pnpm new-post 文件名     # 新建文章模板
```

## 发布流程

所有发布操作通过 Git 推送到 GitHub，Vercel 自动检测并重新部署（2-3 分钟）：

```bash
# 配置变更时，先本地验证构建不会报错
pnpm build

git add -A
git commit -m "feat/fix/chore: 描述"
git push origin main
```

不需要手动操作 Vercel，推送即上线。推送后在 Vercel Dashboard 确认部署状态为 Ready。

## 文章 Frontmatter 规范

每篇文章必须以 YAML frontmatter 开头：

```yaml
---
title: "文章标题"
published: 2026-08-12
description: "一句话摘要"
tags: [标签1, 标签2]
category: 分类名
image: ./images/封面图.jpg   # 可选
draft: false                 # true=草稿不发布
pinned: false                # true=置顶
---
```

## 编码规范

- Biome 为格式化和 lint 工具，Tab 缩进，双引号
- 组件用 PascalCase（`PostCard.astro`），配置用 camelCase（`siteConfig.ts`）
- Git 提交遵循 Conventional Commits：`feat:` / `fix:` / `chore:` / `docs:` / `style:`
- 不要提交密钥、token 等敏感信息
- `dist/`、`node_modules/`、`.astro/` 已在 .gitignore 中

## Claude Code 技能命令

本项目配置了以下技能（新会话中可用斜杠命令调用）：

| 命令 | 文件 | 用途 |
|---|---|---|
| `/blog` | .claude/commands/blog.md | 加载完整博客上下文，通用操作入口 |
| `/publish` | .claude/commands/publish.md | 推送到 GitHub 发布上线 |
| `/new-post` | .claude/commands/new-post.md | 创建新文章 |
| `/config` | .claude/commands/config.md | 修改网站配置 |

## 权限配置

`.claude/settings.json` 已预授权以下操作（无需每次确认）：
- pnpm / git / gh / node / npx 命令
- 文件操作（ls, mkdir, cp, mv, rm, cat 等）
- 浏览器预览工具（preview_* 系列）

## Obsidian 集成

- Vault 路径 = 项目根目录
- 模板位置：`.obsidian/templates/`
- 新建文章：Ctrl+P → Templater → 选择模板
- 图片附件：`public/assets/images/obsidian-attachments/`
- 文章管理面板：`src/content/spec/文章管理面板.md`（Dataview 查询）
- 已安装插件：Dataview、Templater、Linter、Outliner、Admonition、Projects 等 11 个

## 部署架构

- **平台**: Vercel（静态站点托管，git push 自动部署，免费）
- **适配器**: `@astrojs/vercel`（astro.config.mjs 中配置）
- **线上域名**: `https://www.blackboytreasure.cn`
- **根域名**: `blackboytreasure.cn` → 308 跳转到 `www.blackboytreasure.cn`
- **site_url**: 必须与线上域名一致（`src/config/siteConfig.ts`），否则所有内部链接、og:url、sitemap 全部出错

## 部署隐患与防护

| 隐患 | 后果 | 防护措施 |
|---|---|---|
| `site_url` 与实际域名不一致 | 所有链接、SEO 标签、sitemap 失效 | 修改域名时同步更新 `siteConfig.ts` |
| push 前未本地 build | Vercel 构建失败，线上回滚到旧版本 | 每次配置变更后先 `pnpm build` 验证 |
| `@astrojs/vercel` 升级后导入路径变化 | 构建失败 | 升级后立即本地 `pnpm build` 测试 |
| Vercel 部署失败用户无感知 | 线上仍是旧版本，用户以为已上线 | push 后检查 Vercel Dashboard 部署状态 |
| 根域名 DNS 未同步 | 部分网络访问 404 或超时 | 确保腾讯云 A 记录和 CNAME 记录都已添加 |
| `trailingSlash: "always"` | URL 末尾不带 `/` 会 404 | 所有内部链接和配置中保持末尾 `/` |
| 大量图片未压缩 | 构建缓慢，Vercel 免费额度 bandwidth 耗尽 | 图片放 `public/assets/images/`，控制尺寸 |

## Vercel 部署失败排查

```bash
# 1. 检查最新部署状态（需 gh auth）
gh api repos/4Llover/blog/deployments --jq '.[0] | {state, environment, created_at}'
gh api repos/4Llover/blog/deployments/<id>/statuses --jq '.[0].state'

# 2. 本地复现构建
pnpm build

# 3. 若本地成功但 Vercel 失败，检查 @astrojs/vercel 版本兼容性
pnpm list @astrojs/vercel
```

## 重要注意事项

1. 包管理器必须用 pnpm（项目有 preinstall 脚本强制检查）
2. Node.js 版本要求 >= 22
3. 本地开发时 `pnpm dev` 启动后首次加载较慢（Astro 编译依赖），后续热更新很快
4. Vercel 免费额度对个人博客完全够用
5. GitHub 认证存储在 Windows Credential Manager，重装系统才需要重新登录
