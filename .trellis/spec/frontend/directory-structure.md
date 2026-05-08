# Directory Structure

> Fuwari (Astro) 博客项目的目录结构与文件职责。

---

## Directory Layout

```
blog/
├── src/
│   ├── assets/
│   │   └── images/
│   │       └── demo-avatar.png   # 侧边栏头像（替换此文件更换头像）
│   ├── components/               # Astro/Svelte UI 组件（勿随意修改）
│   ├── config.ts                 # 博客核心配置（名称、导航、个人信息）
│   ├── content/
│   │   ├── posts/                # 📝 所有博客文章（.md / .mdx）
│   │   ├── spec/
│   │   │   └── about.md          # About 页面内容
│   │   └── config.ts             # Content Collection schema 定义
│   ├── pages/                    # Astro 路由页面（勿随意修改）
│   └── styles/
│       ├── main.css              # Tailwind 组件类定义（@layer components）
│       └── markdown.css          # 文章正文样式（注意 @apply 限制）
├── public/
│   └── favicon/                  # 网站图标
├── astro.config.mjs              # Astro 构建配置（含站点 URL）
├── tailwind.config.cjs           # Tailwind 配置
└── package.json                  # 使用 pnpm，不要用 npm/yarn
```

---

## 关键文件说明

### `src/config.ts` — 博客配置入口

所有个性化设置都在这里：

```typescript
export const siteConfig: SiteConfig = {
  title: "博客名",
  subtitle: "副标题",
  lang: "zh_CN",     // 语言
  themeColor: { hue: 250, fixed: false },
  banner: { enable: false, src: "..." },
};

export const profileConfig: ProfileConfig = {
  avatar: "assets/images/demo-avatar.png",
  name: "显示名",
  bio: "个人简介",
  links: [{ name: "GitHub", icon: "fa6-brands:github", url: "..." }],
};
```

### `src/content/posts/` — 文章目录

文章 frontmatter schema（来自 `src/content/config.ts`）：

```markdown
---
title: 文章标题         # 必填
published: 2026-05-08  # 必填，日期格式 YYYY-MM-DD
updated: 2026-05-08    # 可选，最后更新日期
description: 摘要       # 可选，显示在文章卡片
image: ''              # 可选，封面图 URL
tags: [生活, 技术]      # 可选，数组
category: 技术          # 可选，单个分类
draft: false           # true = 草稿不公开
---
```

### `astro.config.mjs` — 站点 URL

部署后必须更新 `site` 字段，否则 sitemap / RSS 地址错误：

```javascript
export default defineConfig({
  site: "https://blog-5pn.pages.dev",  // 改为实际域名
  ...
});
```

---

## 发布文章流程

**本地**：在 `src/content/posts/` 新建 `.md` 文件，`pnpm dev` 热更新预览。

**在线（GitHub 网页）**：
1. 进入 `src/content/posts/` 目录
2. Add file → Create new file
3. 文件名填 `文章slug.md`（英文，用连字符）
4. 填写 frontmatter + 正文 → Commit changes
5. Cloudflare Pages 自动触发构建，约 1-2 分钟上线

---

## Naming Conventions

| 对象 | 规范 | 示例 |
|------|------|------|
| 文章文件名 | 小写英文 + 连字符 | `my-first-post.md` |
| 图片资源 | 小写英文 + 连字符 | `project-cover.png` |
| 分类/标签 | 中文或英文均可 | `技术`、`Life` |

---

## Deployment

- **平台**：Cloudflare Pages
- **构建命令**：`pnpm run build`
- **输出目录**：`dist`
- **触发方式**：推送到 `main` 分支自动部署
- **注意**：推送前在本地跑 `pnpm build` 验证，不要只靠 `pnpm dev`
