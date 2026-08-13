# 改网站配置

根据用户需求修改 src/config/ 下的配置文件，然后重新编译验证。

## 常用配置对应关系

- 改名称/描述 → src/config/siteConfig.ts
- 改头像/签名/链接 → src/config/profileConfig.ts
- 改导航菜单 → src/config/navBarConfig.ts
- 改壁纸/横幅文字 → src/config/backgroundWallpaper.ts
- 改侧边栏 → src/config/sidebarConfig.ts
- 改主题色 → siteConfig.ts 的 themeColor.hue (0-360)
- 改字体 → src/config/fontConfig.ts
- 改动画 → src/config/effectsConfig.ts

## 操作步骤

1. 读取对应的配置文件
2. 修改用户要求的配置项
3. 告诉用户改了什么
4. 如果用户想看效果，建议运行 `pnpm dev` 本地预览
5. 如果用户满意，调用 /publish 推送到线上
