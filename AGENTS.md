# AGENTS.md - Top Barks Dog Training Website

Guidelines for AI agents working on this Astro.js-based website project.

## Project Overview

**Stack**: Astro 5 + Tailwind CSS v4 + Preline UI + TypeScript
**Package Manager**: pnpm
**Site**: https://topbarks.co.uk

## Build Commands

```bash
# Development server with hot reload
pnpm dev

# Production build (typecheck + build + HTML minification)
pnpm build

# Preview production build locally
pnpm preview

# Astro CLI commands
pnpm astro check    # Type checking
pnpm astro build    # Build only
```

**No testing framework is currently configured.** If adding tests, use Vitest for unit tests and Playwright for E2E.

## Code Style Guidelines

### Imports & Path Aliases

**ALWAYS use path aliases** - never use relative paths like `../` or `./`:

| Alias | Maps to | Usage |
|-------|---------|-------|
| `@/*` | `src/*` | General source imports |
| `@components/*` | `src/components/*` | UI components, sections |
| `@data/*` | `src/data_files/*` | Constants, JSON data |
| `@images/*` | `src/images/*` | Image assets |
| `@scripts/*` | `src/assets/scripts/*` | JavaScript utilities |
| `@styles/*` | `src/assets/styles/*` | CSS files |
| `@utils/*` | `src/utils/*` | Helper functions |
| `@content/*` | `src/content/*` | Content collections |

**Examples**:
```typescript
// Good
import { SITE } from "@data/constants";
import HeroSection from "@components/sections/landing/HeroSection.astro";
import heroImage from "@images/front_pic.png";

// Bad - never do this
import { SITE } from "../../data_files/constants";
```

### TypeScript Conventions

- **Strict mode enabled** via `astro/tsconfigs/strict`
- Use explicit types for function parameters and returns
- Use interfaces for component props (see `MainLayout.astro` for pattern)
- Avoid `any` - use `unknown` if type is uncertain

**Example pattern from MainLayout.astro**:
```typescript
interface Props {
  title?: string;
  meta?: string;
  structuredData?: object;
  lang?: string;
  customDescription?: string | null;
}
```

### Formatting

- **Prettier** configured with `prettier-plugin-tailwindcss`
- 2-space indentation (default Prettier)
- No semicolons enforced by Prettier defaults
- Double quotes for strings
- Tailwind classes are auto-sorted by Prettier plugin

```bash
# Format all files (run from website/ directory)
npx prettier --write "src/**/*.{ts,astro,css}"
```

### Naming Conventions

| Type | Convention | Example |
|------|------------|---------|
| Components | PascalCase | `HeroSection.astro`, `CardBlog.astro` |
| Utilities | camelCase | `navigation.ts`, `utils.ts` |
| Constants | SCREAMING_SNAKE_CASE | `SITE`, `SEO`, `OG` |
| Props interfaces | PascalCase Props | `interface Props { ... }` |
| CSS classes | kebab-case | `scrollbar-hide`, `lenis-smooth` |
| File names | PascalCase for components | `MainLayout.astro` |

### Tailwind CSS v4 Specifics

This project uses **Tailwind v4** with the new configuration format:

```css
/* In global.css - NOT tailwind.config.js */
@import 'tailwindcss';
@theme {
  --color-forest-600: #3d6b3d;
  --color-earth-500: #b07f52;
}
```

**Key differences from v3**:
- Custom colors defined in `@theme` block in CSS, not JS config
- Use `@custom-variant dark` for dark mode
- Plugin imports: `@plugin '@tailwindcss/forms'`
- No `tailwind.config.js` file exists

### Component Patterns

**Astro components follow this structure**:
```astro
---
// 1. Imports at top
import MainLayout from "@/layouts/MainLayout.astro";
import { SITE } from "@data/constants";

// 2. Props interface (if accepting props)
interface Props {
  title: string;
  subTitle?: string;
}

// 3. Destructure props with defaults
const { title, subTitle = "" } = Astro.props;
---

<!-- 4. Template using props -->
<section>
  <h1>{title}</h1>
  {subTitle && <p>{subTitle}</p>}
</section>
```

### Content Collections

All content uses Zod schemas in `src/content.config.ts`:

```typescript
import { z, defineCollection } from 'astro:content';
import { glob } from 'astro/loaders';

const blogCollection = defineCollection({
  loader: glob({ pattern: '**/[^_]*.{md,mdx}', base: "./src/content/blog" }),
  schema: ({ image }) => z.object({
    title: z.string(),
    pubDate: z.date(),
    // ...more fields
  }),
});
```

### Error Handling

- Use Zod for runtime validation of content collections
- Content schemas must be strict - all fields explicitly typed
- Handle missing images gracefully with fallback patterns
- Use TypeScript strict null checks

### Preline UI Components

Preline is used for interactive components (modals, dropdowns, accordions):

```astro
<script>
  import "preline/preline.js";
</script>
```

- Preline script loaded in `MainLayout.astro`
- Preline CSS variants imported in `global.css`: `@import 'preline/variants.css'`
- Follow Preline documentation for component markup patterns

### Dark Mode

Implemented via CSS classes and localStorage:

```css
/* Always pair light and dark variants */
class="text-forest-800 dark:text-forest-200"
class="bg-beige-50 dark:bg-earth-950"
```

Color palette is defined in `global.css` using brand colors:
- `forest-*`: Primary brand greens
- `earth-*`: Warm browns/tans
- `sage-*`: Supporting accent greens
- `beige-*`: Background neutrals

### SEO & Meta

SEO is centralized in `src/data_files/constants.ts`:

```typescript
export const SITE = { title, description, url };
export const SEO = { title, description, structuredData };
export const OG = { title, description, image };
```

Override per-page via `MainLayout` props:
```astro
<MainLayout 
  title="Custom Page Title"
  customDescription="Page-specific description"
/>
```

## Project Structure Reference

```
website/
├── src/
│   ├── components/          # Reusable Astro components
│   │   ├── sections/        # Page sections (landing, features, etc.)
│   │   └── ui/              # UI primitives (buttons, cards, forms)
│   ├── layouts/             # Layout templates
│   ├── pages/               # File-based routes
│   ├── content/             # Markdown/MDX collections
│   ├── content.config.ts    # Collection schemas
│   ├── data_files/          # Constants, JSON data
│   ├── utils/               # Helper functions
│   ├── images/              # Image assets
│   └── assets/
│       ├── scripts/         # JS utilities
│       └── styles/          # Global CSS, Tailwind theme
├── public/                  # Static files
├── astro.config.mjs         # Astro configuration
├── tsconfig.json            # TypeScript config (path aliases)
└── .prettierrc              # Prettier config
```

## Common Tasks

**Add a new page**:
1. Create `.astro` file in `src/pages/`
2. Use `MainLayout` wrapper
3. Import sections from `@components/sections/`

**Add a new component**:
1. Create in `src/components/ui/` or `src/components/sections/`
2. Use PascalCase naming
3. Define Props interface if accepting props
4. Use path aliases for imports

**Add content**:
1. Add markdown to `src/content/blog/`, `products/`, etc.
2. Follow existing frontmatter patterns
3. Images go in `src/images/content/`

**Update navigation**:
1. Edit `src/utils/navigation.ts`
2. Update `navBarLinks` or `footerLinks` arrays

## Important Notes

- **Always use pnpm**, not npm or yarn
- **Always use path aliases** - relative imports break during refactoring
- **This is Tailwind v4** - syntax differs from v3
- **No tests exist yet** - add Vitest/Playwright if testing is needed
- HTML is minified in production via `process-html.mjs`
- Site uses Lenis for smooth scrolling
- Images are processed by Sharp via Astro

## Git Repository Structure (IMPORTANT)

This project uses **two separate git repositories**:

### 1. Website Repository (`website/`)
- **Location**: `/top_barks/website/`
- **Remote**: `https://github.com/simond3414/top-barks-website.git`
- **Purpose**: The live Astro.js website deployed to Cloudflare Pages
- **Commits**: Always work from the `website/` directory

```bash
cd website/
git status
git add .
git commit -m "feat: description"
git push
```

### 2. Materials Repository (parent directory)
- **Location**: `/top_barks/` (this directory)
- **Remote**: `https://github.com/simond3414/top-barks-materials.git`
- **Purpose**: Construction materials, content files, and resources
- **Commits**: Always work from the parent directory (`/top_barks/`)

```bash
# From /top_barks/ (NOT in website/)
git status
git add .
git commit -m "feat: description"
git push
```

### What's in Each Repository?

**Website repo (`website/`)**:
- Astro.js source code
- Components, pages, layouts
- Build configuration
- Deployed to https://topbarks.co.uk

**Materials repo (parent)**:
- `md_files/` - Content markdown and images
- `tb_resources/` - PDF training resources (password-protected)
- `ai_helper_materials/` - Screenshots and helper images
- `AGENTS.md` - This file
- `package.json` - Root dependencies
- `.gitignore` - Excludes nested repos

### Working with Both Repos

**When building the website:**
```bash
cd website/
pnpm build
# Commit from website/ directory
git add .
git commit -m "feat: changes"
git push
```

**When updating materials:**
```bash
# Stay in /top_barks/
git add md_files/
git commit -m "feat: new content"
git push
```

**Important**: The `.gitignore` in the parent directory excludes `website/` and `template_materials/` to prevent git from trying to track the nested repositories.
