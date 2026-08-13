# CLAUDE.md — 小黑的宝藏

个人博客项目，基于 Firefly (Astro 7) 模板。

## 快速参考

- **仓库**: https://github.com/4Llover/blog
- **部署**: Vercel（git push 自动上线）
- **GitHub**: 4Llover（已认证，密钥环持久化）
- **编辑器**: Obsidian（Vault = 项目根目录）

## 命令

```bash
pnpm dev          # 本地开发 localhost:4321
pnpm build        # 生产编译
pnpm new-post 名称 # 新建文章
```

## 发布

```bash
git add -A && git commit -m "feat: 描述" && git push
```

## 技能

- `/blog` — 加载完整上下文
- `/publish` — 推送发布
- `/new-post` — 创建文章
- `/config` — 改配置

详细说明见 [AGENTS.md](AGENTS.md) 和 [docs/使用指南.md](docs/使用指南.md)
