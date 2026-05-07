# brainstorm: 搭建个人博客

## Goal

搭建一个个人开发者博客，用于发布技术文章、记录学习心得，具备良好的 SEO、快速加载和舒适的写作体验。

## What I already know

* 项目目录为空（`/Desktop/blog`），尚无任何代码
* 开发者为 AZUR3B0NES，使用 Windows + PowerShell 环境
* 当前无框架偏好已确定

## Research Notes

### 主流个人博客技术方案对比（2026）

**Astro** — 现代静态站点生成器
- Island 架构：仅在需要时注水 JS，默认零 JS
- 支持 MDX、Markdown 写作
- npm 下载量快速增长，社区最活跃
- 原生支持 React/Vue/Svelte 组件混用
- Netlify/Vercel/GitHub Pages 均可免费托管

**Hugo** — 极速静态生成器（Go）
- 构建速度最快（万级页面毫秒级）
- 模板语法学习曲线略陡
- 不依赖 Node.js，环境简单
- 丰富的主题生态

**Next.js** — 全栈 React 框架
- 支持静态导出 + 服务端渲染
- 适合需要动态功能（评论、搜索后端）的博客
- 配置复杂度较高，对纯内容博客偏重

### 托管平台推荐

* **GitHub Pages** — 免费，与 Git 工作流无缝集成
* **Vercel** — 免费层充足，Next.js/Astro 首选
* **Cloudflare Pages** — 全球 CDN，免费，构建速度快

## Theme Research Notes

### 极简风（Minimal）

| 主题 | GitHub | 特点 |
|------|--------|------|
| **AstroPaper** | satnaing/astro-paper | ⭐ 最流行，极简黑白，SEO 优化，模糊搜索，深浅色切换 |
| **Astro Ink** | one-aalam/astro-ink | 清爽极简，适合技术写作 |
| **Stablo** | Web3Templates/stablo | Tailwind + MDX，快速上手 |

### 优雅/日系风

| 主题 | GitHub | 特点 |
|------|--------|------|
| **Fuwari** | saicaca/fuwari | ⭐ 中文社区最流行，卡片式布局，深浅色，View Transitions |
| **Frosti** | EveSunMaple/Frosti | 国内开发者作品，干净优雅，功能完善 |
| **Firefly（流萤）** | CuteLeaf/Firefly | 基于 Fuwari 二次开发，清新美观 |
| **Mizuki** | matsuzaka-yuki/Mizuki | Material Design 3 风格，现代感强 |

### 全功能型

| 主题 | GitHub | 特点 |
|------|--------|------|
| **AstroWind** | onwidget/astrowind | GitHub 最多 ⭐，完整落地页+博客，适合作品集+博客合一 |
| **Bookworm Light** | 多作者支持，内容分类丰富 | 内容型网站首选 |

## Decision (ADR-lite)

**Context**: 需要选择个人博客框架和主题，用于生活记录、技术分享、项目经历展示。
**Decision**: Astro + AstroWind 主题，部署到 Vercel
**Consequences**: 开箱即用的落地页+博客+作品集结构，GitHub 星数最多，维护活跃；需要一定 Tailwind 基础来自定义样式。

## Requirements

* 使用 AstroWind 模板（Astro 5 + Tailwind CSS）
* 博客栏目：生活、技术、项目经历（通过标签/分类区分）
* Projects 页面展示项目经历
* About 页面介绍个人信息
* 深色/浅色主题切换
* SEO 优化（meta、OG 图）
* 部署到 Vercel（免费）

## Acceptance Criteria (evolving)

* [ ] 能在本地预览博客
* [ ] 支持新建文章并实时热更新
* [ ] 构建后可部署到静态托管平台
* [ ] 首屏加载 < 1s（Lighthouse 评分 > 90）

## Definition of Done

* 项目可本地运行
* 至少一篇示例文章
* 部署到托管平台并可公开访问
* README 说明如何新增文章

## Out of Scope

* 评论系统（可后续集成 Giscus/Utterances）
* 付费托管方案
* 后台管理 CMS（纯文件写作）

## Technical Notes

* 参考：https://eastondev.com/blog/en/posts/dev/20251123-blog-framework-guide/
* 参考：https://thesoftwarescout.com/best-static-site-generators-2026-astro-next-js-hugo-more/
* 参考：https://criztec.com/hugo-vs-astro/
