# 写新博客文章

## 操作步骤

1. 询问用户：文章标题是什么？大致内容方向？
2. 创建文件 `src/content/posts/文件名.md`（文件名用英文短横线格式）
3. 写好 frontmatter：
   - title: 中文标题
   - published: 今天日期 YYYY-MM-DD
   - description: 一句话摘要
   - tags: 根据内容填写
   - category: 分类
   - draft: false（默认发布；如果用户想先存为草稿则设为 true）
4. 根据用户描述写正文（Markdown 格式）
5. 如果用户提供了图片，放到 `public/assets/images/` 下并在文章中引用
6. 告诉用户文章已创建，可以在 Obsidian 中继续编辑
7. 如果用户想立即发布，调用 /publish 流程
