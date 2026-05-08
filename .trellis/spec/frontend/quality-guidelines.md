# Quality Guidelines

> Code quality standards for frontend development.

---

## Overview

<!--
Document your project's quality standards here.

Questions to answer:
- What patterns are forbidden?
- What linting rules do you enforce?
- What are your testing requirements?
- What code review standards apply?
-->

(To be filled by the team)

---

## Forbidden Patterns

### CSS: 禁止跨文件 `@apply` 自定义组件类

**禁止**在独立 CSS 文件中用 `@apply` 引用定义在其他文件里的自定义类（如 `@apply link`、`@apply card-base`）。

**原因**：Tailwind v3 在 Vite 分块编译时，每个 CSS 文件独立走 PostCSS 管道。没有 `@tailwind components` 指令的文件无法解析其他文件的 `@layer components` 内容。本地热更新（`pnpm dev`）可能因缓存不报错，但 CI 冷构建会失败。

**正确做法**：
- 将 CSS 内容合并到 `main.css` 的 `@layer components` 块内，或
- 内联使用 Tailwind 原子类替代自定义组件类

```css
/* ❌ 错误 */
a { @apply link font-medium; }

/* ✅ 正确：内联原子类 */
a { @apply transition rounded-md p-1 -m-1 font-medium; }
```

---

## Required Patterns

<!-- Patterns that must always be used -->

(To be filled by the team)

---

## Testing Requirements

<!-- What level of testing is expected -->

(To be filled by the team)

---

## Code Review Checklist

- [ ] CSS 文件中是否有跨文件 `@apply` 自定义类？（见 Forbidden Patterns）
- [ ] 新功能推送前是否执行过本地 `pnpm build` 冷构建验证（而非仅 `pnpm dev`）？
