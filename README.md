# Top Barks Materials

**Construction materials and content repository for Top Barks Dog Training**

This repository contains all the content, training resources, and construction materials used to build the Top Barks Dog Training website and business materials.

---

## Repository Overview

This repository works alongside the [website repository](https://github.com/simond3414/top-barks-website) which contains the live Astro.js website deployed to [topbarks.co.uk](https://topbarks.co.uk).

### What's in This Repository

| Directory | Contents |
|-----------|----------|
| `md_files/` | Content markdown files and images for the website |
| `tb_resources/` | Password-protected PDF training resources for clients |
| `ai_helper_materials/` | Screenshots and helper images |
| `website/` | (separate repo) - The live website |
| `template_materials/` | (separate repo) - Template materials |

---

## Git Repository Structure

This project uses **two separate git repositories**:

### 1. Website Repository (`website/`)
- **Location**: `/website/` (nested git repository)
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

### 2. Materials Repository (this directory)
- **Location**: `/top_barks/` (current directory)
- **Remote**: `https://github.com/simond3414/top-barks-materials.git`
- **Purpose**: Construction materials, content files, and resources
- **Commits**: Always work from the parent directory (`/top_barks/`)

```bash
# Stay in /top_barks/ (NOT in website/)
git status
git add .
git commit -m "feat: description"
git push
```

---

## Directory Contents

### `md_files/` - Website Content
Contains all the markdown content and images that populate the website:

**Content Files:**
- `home.md` - Homepage content
- `about.md` - About Mark Sanderson
- `dog_training.md` - Dog training service content
- `puppy_training.md` - Puppy training service content
- `behaviour_problems.md` - Behaviour consultation content
- `gun_dog_training.md` - Gundog training content
- `show_training.md` - Show training content
- `training_walks.md` - Training walks content
- `contact.md` - Contact page content
- `resources.md` - Client resources page
- `reviews.md` - Reviews/testimonials content
- `cancellations.md` - Cancellation policy
- `sitemap.md` - Sitemap structure

**Images (`md_files/images/`):**
- 47 images including:
  - Logo files (PNG and SVG formats)
  - Training photos
  - Breed images (clumber, field spaniel, spinone, cocker, bracco)
  - About page photos
  - Award images
  - Accreditations (APDT, ABTC, UKDOG Charter)

### `tb_resources/` - Training Resources
38 password-protected PDF training resources for clients, including:

**Behaviour Guides:**
- Cognitive Dysfunction
- Resource Guarding
- Scared Dogs
- Dogs scared of people
- Ladder of aggression
- Modifying behaviour problems
- Helping nervous and shy dogs

**Training Guides:**
- Clicker training basics
- Loose lead walking
- Whistle recall
- Gundog handling
- The stop whistle
- Good dog handling
- Parallel walking
- Automatic check-in

**Puppy Resources:**
- Puppy essentials
- Puppies and older dogs together
- Car sick puppies
- Puppy weekly social chart
- Kong stuffing recipes
- The Name Game

**Medication Information:**
- Fluoxetine for Dogs
- Zylkene

### `ai_helper_materials/` - Helper Screenshots
13 screenshot images used for AI assistance and reference during development:
- `screenshot_2026_01.png` through `screenshot_2026_14.png` (excluding 11)

---

## Working with This Repository

### When to Commit to This Repository

Commit to **this repository** when working with:
- ✅ Markdown content files
- ✅ Website images and assets
- ✅ PDF training resources
- ✅ Screenshot documentation
- ✅ Configuration files (AGENTS.md, .gitignore, etc.)

**Always commit from the `/top_barks/` directory:**
```bash
# From /home/simond3414/projects/top_barks/
git add md_files/new-content.md
git commit -m "feat: Add new training article"
git push
```

### When to Commit to the Website Repository

Commit to the **website repository** when working with:
- ✅ Astro.js components and pages
- ✅ Layout files
- ✅ JavaScript/TypeScript code
- ✅ CSS and styling
- ✅ Build configuration
- ✅ npm dependencies

**Always change to the website directory first:**
```bash
cd website/
pnpm build
git add .
git commit -m "feat: Add new component"
git push
```

---

## Business Information

**Top Barks Dog Training**
- **Owner:** Mark Sanderson
- **Location:** 11 Redthorn Drive, Huntington, York Y031 9DW
- **Website:** https://topbarks.co.uk
- **Email:** mark@topbarks.co.uk
- **Phone:** 07932 632855
- **Hours:** Monday-Friday, 9:30am-4:00pm
- **Service Area:** York, Huntington, Haxby, Wigginton, North Yorkshire

---

## Technical Details

- **Website Stack:** Astro 5 + Tailwind CSS v4 + Preline UI + TypeScript
- **Package Manager:** pnpm (not npm)
- **Deployment:** Cloudflare Pages
- **Hosting:** Static site with some serverless functions
- **Image Processing:** Sharp via Astro

---

## Quick Reference

| Task | Command Location |
|------|------------------|
| Update website content | `/top_barks/` (this repo) |
| Update website code | `/top_barks/website/` (website repo) |
| Build website | `cd website/ && pnpm build` |
| Deploy website | `cd website/ && git push` |
| Add new resources | `/top_barks/` (this repo) |
| Run dev server | `cd website/ && pnpm dev` |

---

## Important Notes

1. **Never mix commits** - Always be clear about which repository you're committing to
2. **Use pnpm**, not npm - The website uses pnpm exclusively
3. **Always use path aliases** in the website code (see AGENTS.md)
4. **This is Tailwind v4** - Configuration differs from v3
5. **The `.gitignore`** in this repo excludes the nested `website/` and `template_materials/` directories to prevent tracking conflicts

---

## License & Copyright

© 2006-2025 Top Barks Dog Training. All rights reserved.

The training resources (PDFs) are password-protected and intended for client use only.

---

## Contact

For questions about this repository or the website:
- **Website:** https://topbarks.co.uk
- **Email:** mark@topbarks.co.uk
