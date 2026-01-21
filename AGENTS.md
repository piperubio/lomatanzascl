# AGENTS.md - Lomatanzas Website

This document provides guidance for AI coding agents working on this codebase.

## Project Overview

Lomatanzas Family Lodge website - a static marketing site for cabin rentals in Matanzas, Chile.

**Tech Stack:**
- **Framework:** Astro 5
- **Language:** TypeScript (strict mode)
- **CSS:** Tailwind CSS 4 (via Vite plugin)
- **Package Manager:** pnpm
- **Icons:** lucide-astro

## Build/Lint/Test Commands

```bash
# Development server (localhost:4321)
pnpm dev

# Production build (outputs to ./dist)
pnpm build

# Preview production build locally
pnpm preview

# Run Astro CLI commands
pnpm astro <command>

# Type checking (via Astro's TypeScript integration)
pnpm astro check
```

**Note:** No linting (ESLint) or testing framework is configured. TypeScript strict mode provides type safety.

## Code Style Guidelines

### Astro Component Structure

Follow this pattern for all `.astro` components:

```astro
---
/**
 * ComponentName
 * Brief description in Spanish
 */

// 1. Imports (lucide-astro icons, other components)
import { IconName } from 'lucide-astro';

// 2. TypeScript interfaces
interface Props {
  title: string;
  description?: string;
}

// 3. Data definitions (arrays, objects)
const items = [
  { key: "value" }
];

// 4. Destructure props with defaults
const { title, description = "default" } = Astro.props;
---

<!-- 5. HTML Template -->
<section class="section-padding">
  <div class="container-custom">
    {items.map((item) => (
      <div>{item.key}</div>
    ))}
  </div>
</section>

<style>
  /* 6. Component-scoped CSS (minimal, prefer Tailwind) */
</style>

<script>
  // 7. Client-side JavaScript (vanilla JS only)
</script>
```

### Naming Conventions

| Type | Convention | Example |
|------|------------|---------|
| Components | PascalCase | `SocialProof.astro` |
| Pages | kebab-case | `condiciones.astro` |
| CSS classes | Tailwind utilities + semantic | `btn-primary`, `card` |
| JS variables | camelCase | `faqSchema` |
| CSS properties | kebab-case | `--color-primary` |

### Import Order

1. Astro/framework imports
2. Third-party imports (lucide-astro)
3. Local components
4. Styles (in Layout only)

```astro
---
import Layout from '../layouts/Layout.astro';
import { Phone, Mail } from 'lucide-astro';
import Welcome from '../components/Welcome.astro';
---
```

### TypeScript

- Strict mode is enabled (extends `astro/tsconfigs/strict`)
- Always define `interface Props` for component props
- Use optional properties with `?` and provide defaults when destructuring
- Type cast DOM elements when needed: `as HTMLElement`

### CSS/Styling

- **Utility-first:** Use Tailwind classes directly in HTML
- **Custom classes:** Defined in `src/styles/global.css` using `@apply`
- **Design tokens:** Use CSS custom properties from `@theme` block
- **Responsive:** Mobile-first with `sm:`, `md:`, `lg:` prefixes

Key utility classes:
- `.container-custom` - Max-width container with padding
- `.section-padding` - Consistent vertical spacing
- `.btn-primary`, `.btn-secondary`, `.btn-whatsapp` - Button styles
- `.card`, `.card-warm` - Card containers
- `.section-title`, `.section-subtitle` - Typography

### Accessibility

- Use semantic HTML (`<section>`, `<nav>`, `<main>`)
- Include `aria-*` attributes on interactive elements
- Provide `alt` text for all images
- Support `prefers-reduced-motion` (already configured)
- Use `focus-visible` for keyboard navigation

### SEO Requirements

- Include Schema.org JSON-LD markup where appropriate
- Use semantic heading hierarchy (h1 > h2 > h3)
- Add meta descriptions and OpenGraph tags via Layout props
- External links: `target="_blank" rel="noopener noreferrer"`

### Language

- **Code comments:** Spanish (matches target audience)
- **Variable/function names:** English
- **Content/UI text:** Spanish (Chilean market)

## Design System

### Colors (from `global.css` @theme)

```css
--color-primary: #0891b2;      /* Cyan - ocean theme */
--color-primary-dark: #0e7490;
--color-secondary: #f59e0b;    /* Amber - sun/sand */
--color-accent: #10b981;       /* Emerald - nature */
--color-sand: #fef7ed;         /* Background */
--color-dark: #1c1917;         /* Text */
```

### Typography

- **Display font:** Plus Jakarta Sans (headings)
- **Body font:** DM Sans (paragraphs)
- Use `.font-display` and `.font-body` classes

### Spacing

- Sections: `py-16 md:py-24` (via `.section-padding`)
- Container: `max-w-7xl mx-auto px-4 sm:px-6 lg:px-8`

