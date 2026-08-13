# 发布文章到线上

将本地改动推送到 GitHub，Vercel 会自动重新部署。

## 操作步骤

1. `git add -A`
2. `git status` 展示给用户看改了什么
3. 根据改动内容生成合适的 commit 信息（遵循 Conventional Commits）：
   - 改了配置 → `chore: 更新xxx配置`
   - 新增文章 → `feat: 发布文章《标题》`
   - 修改文章 → `docs: 更新文章《标题》`
   - 修了bug → `fix: 修复xxx问题`
4. `git commit -m "生成的信息"`
5. `git push origin main`
6. 告诉用户：已推送，Vercel 会在 2-3 分钟内自动部署完成

注意：GitHub 账号 4Llover 已认证（密钥环持久化），无需重新登录。
