# 发布文章到线上

将本地改动推送到 GitHub，Vercel 会自动重新部署到 `www.blackboytreasure.cn`。

## 操作步骤

1. 如果本次改动涉及配置文件（siteConfig.ts、astro.config.mjs 等），**先运行 `pnpm build` 验证构建无报错**
2. `git add -A`
3. `git status` 展示给用户看改了什么
4. 根据改动内容生成合适的 commit 信息（遵循 Conventional Commits）：
   - 改了配置 → `chore: 更新xxx配置`
   - 新增文章 → `feat: 发布文章《标题》`
   - 修改文章 → `docs: 更新文章《标题》`
   - 修了bug → `fix: 修复xxx问题`
5. `git commit -m "生成的信息"`
6. `git push origin main`
7. 告诉用户：已推送，Vercel 会在 2-3 分钟内自动部署完成

## 部署失败时

如果 Vercel 构建失败，线上会保持旧版本不中断：
1. 本地运行 `pnpm build` 复现错误
2. 修复后重新 commit + push
3. 确认 Vercel Dashboard 部署状态为 Ready

注意：GitHub 账号 4Llover 已认证（密钥环持久化），无需重新登录。
