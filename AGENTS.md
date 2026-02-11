# AGENTS.md - Project Guide for AI Coding Agents

## Project Overview

This is an **Academic CV/Portfolio Website** built with [Hugo Blox](https://hugoblox.com) (formerly Hugo Academic) for MIYAKOSHI Yuki (宮腰悠希), a doctoral student in Engineering at Tokyo Denki University. The website serves as a personal academic portfolio showcasing research work, publications, events/talks, projects, and blog posts.

**Live Site**: https://www.miyakoshiyuki.jp/

The primary language is Japanese (ja-JP), with support for multilingual content structure.

---

## Technology Stack

| Component | Version | Purpose |
|-----------|---------|---------|
| [Hugo](https://gohugo.io/) | 0.154.5 | Static site generator |
| [Go](https://golang.org/) | 1.19+ | Hugo modules support |
| [Node.js](https://nodejs.org/) | 22 | Build tooling |
| [pnpm](https://pnpm.io/) | 10.14.0 | Package manager |
| [Tailwind CSS](https://tailwindcss.com/) | 4.1.12 | CSS framework |
| [Pagefind](https://pagefind.app/) | 1.4.0 | Static site search |
| [Hugo Blox](https://hugoblox.com/) | v2 | Website builder framework |

### Hugo Modules Used
- `github.com/HugoBlox/kit/modules/integrations/netlify` - Netlify integration
- `github.com/HugoBlox/kit/modules/blox` - Core blox system
- `github.com/HugoBlox/kit/modules/slides` - Reveal.js slides support

---

## Project Structure

```
├── config/_default/        # Hugo configuration files
│   ├── hugo.yaml          # Core Hugo settings (language, pagination, imaging)
│   ├── params.yaml        # Hugo Blox parameters (theme, SEO, analytics)
│   ├── menus.yaml         # Navigation menu configuration
│   ├── languages.yaml     # Language configuration (ja-JP primary)
│   └── module.yaml        # Hugo modules imports and mounts
├── content/               # Website content (Markdown files)
│   ├── _index.md          # Homepage landing sections (blocks configuration)
│   ├── authors.backup/    # Legacy author data (deprecated)
│   ├── blog/              # Blog posts with images in subfolders
│   ├── contact.md         # Contact page with embedded Google Form
│   ├── courses/           # Course/tutorial content (Hugo Blox guide)
│   ├── events/            # Talks/presentations with date ranges
│   ├── experience.md      # Experience/CV page using resume blocks
│   ├── news/              # Short news items (YYYYMMDDX-XX.md format)
│   ├── projects/          # Project showcases
│   ├── publications/      # Academic publications
│   └── slides/            # Reveal.js presentations
├── data/                  # Data files
│   └── authors/
│       └── me.yaml        # Author profile (schema: hugoblox/author/v1)
├── assets/                # Static assets processed by Hugo
│   ├── css/
│   │   └── custom.css     # Custom CSS (bio-text class for paragraph spacing)
│   ├── media/             # Images, icons, author avatar
│   └── jsconfig.json      # JavaScript configuration
├── layouts/               # Custom HTML templates
│   └── _partials/         # Partial templates
│       ├── hooks/head-end/# Custom head injections
│       └── views/         # Custom view templates (news.html)
├── static/                # Static files copied as-is
│   └── uploads/           # Downloadable files (resume.pdf)
├── hugo-blox/             # Local blox overrides (community/all-access)
├── .github/workflows/     # GitHub Actions
│   ├── deploy.yml         # Deploy to GitHub Pages
│   ├── import-publications.yml  # BibTeX to Markdown conversion
│   └── upgrade.yml        # Auto-upgrade Hugo Blox modules
├── go.mod & go.sum        # Go module dependencies
├── package.json           # Node.js dependencies
├── pnpm-lock.yaml         # pnpm lockfile
├── hugoblox.yaml          # Hugo Blox version metadata
├── netlify.toml           # Netlify deployment configuration
└── .devcontainer/         # DevContainer configuration
    └── devcontainer.json  # VS Code DevContainer setup
```

---

## Build and Development Commands

All commands use `pnpm` (preferred):

```bash
# Development server (with live reload)
pnpm dev
# Equivalent: hugo server --disableFastRender
# Accessible at http://localhost:1313

# Production build
pnpm build
# Equivalent: hugo --minify && pnpm run pagefind

# Generate search index only
pnpm run pagefind
# Equivalent: pagefind --site public
```

### Hugo Commands

```bash
# Start development server with full rebuild
hugo server --disableFastRender

# Production build with minification
hugo --minify --baseURL "https://www.miyakoshiyuki.jp/"

# Build with garbage collection
hugo --gc --minify

# Clean module cache
hugo mod clean
hugo mod get -u
hugo mod tidy
```

---

## Content Management

### Homepage Configuration (`content/_index.md`)

The homepage uses Hugo Blox "blocks" system:

```yaml
sections:
  - block: resume-biography-3    # Hero section with avatar and bio
  - block: markdown              # Custom research description text
  - block: collection            # Publications list (view: citation)
  - block: collection            # Events/talks grid (view: article-grid)
  - block: collection            # News items (view: news)
```

### Content Types

| Type | Location | Description |
|------|----------|-------------|
| News | `content/news/` | Short news updates (format: `YYYYMMDD-X.md`) |
| Blog | `content/blog/` | Long-form articles with images in subfolders |
| Publications | `content/publications/` | Academic papers (can be auto-imported from BibTeX) |
| Events | `content/events/` | Talks, presentations with event dates |
| Projects | `content/projects/` | Project showcases with featured images |
| Courses | `content/courses/` | Educational/tutorial content |
| Slides | `content/slides/` | Reveal.js presentations |

### Author Profile (`data/authors/me.yaml`)

Schema: `hugoblox/author/v1`

Contains:
- Personal details (name in Japanese/English, role, bio)
- Affiliations with URLs
- Education history with dates
- Experience entries
- Social links (GitHub, etc.)

### Frontmatter Convention

```yaml
---
title: 'ページタイトル'
date: 2024-01-15
authors:
  - me           # References data/authors/me.yaml
featured: false  # For featuring content
tags: []
---
```

---

## Code Style Guidelines

### Markdown Content

1. **Frontmatter**: Use YAML format with `---` delimiters
2. **Filenames**: Use lowercase with hyphens (kebab-case)
3. **Dates**: Use ISO 8601 format (`2024-01-15`)
4. **Images**: Store in content folders alongside index.md
5. **News format**: `YYYYMMDD-X.md` where X is a sequence number

### Hugo Templates

1. **Partials**: Place in `layouts/_partials/`
2. **Custom views**: Place in `layouts/_partials/views/`
3. **Hook files**: Add custom HTML to `layouts/_partials/hooks/head-end/`
4. **Custom CSS**: Add to `assets/css/custom.css`

### CSS Conventions

- Uses Tailwind CSS v4 utility classes
- Custom CSS in `assets/css/custom.css` for specific overrides
- Example: `.bio-text` class for paragraph spacing in biography

---

## Deployment

### Primary: Netlify

Configuration in `netlify.toml`:
- Build command: `pnpm install && hugo --gc --minify && pnpm run pagefind`
- Publish directory: `public`
- Hugo version: 0.154.5
- Node version: 22
- Uses `netlify-plugin-hugo-cache-resources` for caching

### Alternative: GitHub Pages

Workflow in `.github/workflows/deploy.yml`:
- Triggers on push to `main`
- Uses `actions/deploy-pages@v4`
- Requires `HUGO_BLOX_LICENSE` secret for Pro features

---

## Automated Workflows

### 1. Publication Import (`.github/workflows/import-publications.yml`)

Automatically converts BibTeX to Markdown:
- **Trigger**: Push to `publications.bib` file
- **Tool**: `academic` Python package (>=0.10.0)
- **Command**: `academic import publications.bib content/publication/ --compact --verbose`
- **Output**: Creates a Pull Request with imported publications

### 2. Hugo Blox Upgrade (`.github/workflows/upgrade.yml`)

Automatically updates Hugo Blox modules:
- **Schedule**: Mondays at 05:00 UTC
- **Manual trigger**: Available with version choice (Stable/Beta)
- **Command**: `pnpm dlx hugoblox@latest upgrade --yes --ci`
- **Output**: Creates a PR with module updates

---

## Development Environment

### Using DevContainer (Recommended)

File: `.devcontainer/devcontainer.json`

- Image: `ghcr.io/HugoBlox/hugo-blox-dev:hugo0.154.5`
- Pre-configured with Hugo 0.154.5
- Includes Lore Studio VS Code extension
- Port 1313 forwarded for Hugo dev server
- Post-create command: `pnpm --version && hugo version`

### VS Code Extensions

Recommended extension: `lore.lore-studio` (Lore Studio visual editor)

### Local Setup Requirements

- Hugo Extended 0.154.5
- Go 1.19+
- Node.js 22
- pnpm 10.14.0

```bash
# Install dependencies
pnpm install

# Start dev server
pnpm dev
```

---

## Configuration Reference

### Hugo Configuration (`config/_default/hugo.yaml`)

Key settings:
- `defaultContentLanguage: ja` - Primary language is Japanese
- `hasCJKLanguage: true` - CJK language support
- `enableRobotsTXT: true` - Generate robots.txt
- `pagination.pagerSize: 10` - Items per page
- `imaging.quality: 90` - Image quality setting
- `imaging.resampleFilter: lanczos` - Image resampling

### Hugo Blox Parameters (`config/_default/params.yaml`)

Key sections:
- `identity` - Site branding, SEO metadata, social accounts
- `theme.mode: system` - Color scheme follows OS preference
- `header` - Navigation settings (search, theme toggle, language switcher)
- `footer.style: minimal` - Footer style
- `analytics.google.measurement_id` - Google Analytics 4 (G-SDLX266KE1)
- `search.enable: true` - Site search enabled
- `content.citations.style: apa` - Citation format
- `copyright.license.type: cc` - Creative Commons license
- `locale.date_format: "2006/01/02"` - Japanese date format

### Navigation Menu (`config/_default/menus.yaml`)

Items: Bio, Publications, Talks, News, Posts, Experience, Projects, Contact

---

## Security Considerations

1. **Environment Variables**: 
   - `HUGO_BLOX_LICENSE` - Stored in GitHub Secrets for Pro features
   
2. **Analytics**: 
   - Google Analytics 4 uses measurement ID (public)
   
3. **Forms**: 
   - Contact form uses embedded Google Forms (external iframe)
   
4. **CSP**: 
   - Content Security Policy configurable in `params.yaml` under `security.csp`
   
5. **AI Crawlers**:
   - `llms.txt` guidance configured in `params.yaml` under `seo.ai`

---

## Troubleshooting

### Common Issues

1. **Build fails with module errors**:
   ```bash
   hugo mod clean
   hugo mod get -u
   hugo mod tidy
   ```

2. **Pagefind search not working**:
   - Ensure `pnpm run pagefind` runs after build
   - Check `public` directory exists

3. **Style issues**:
   - Tailwind CSS v4 uses `@tailwindcss/cli`
   - Check `package.json` dependencies

4. **Image processing errors**:
   - Hugo Extended version required for image processing
   - Check `imaging.timeout` setting (default: 600000ms)

### Cache Locations

- Hugo cache: `/tmp/hugo_cache_runner/`
- Resources: `resources/` (committed to git)
- Pagefind index: `public/pagefind/`
- pnpm store: Mounted as volume in DevContainer

---

## External Resources

- [Hugo Blox Documentation](https://docs.hugoblox.com/)
- [Hugo Documentation](https://gohugo.io/documentation/)
- [Tailwind CSS v4 Docs](https://tailwindcss.com/docs)
- [Pagefind Documentation](https://pagefind.app/docs/)
- [Lore Studio Extension](https://marketplace.visualstudio.com/items?itemName=lore.lore-studio)

---

## License

- Hugo Blox Template: MIT © 2016-Present [George Cushen](https://georgecushen.com)
- Content and personal modifications: © MIYAKOSHI Yuki
