# AI Agent Instructions for Hugo Blox Academic CV Site

**Project**: Academic CV website built with Hugo Blox + Tailwind CSS v4 + Pagefind  
**Language**: Japanese (日本語 — `defaultContentLanguage: ja`)  
**Build System**: Hugo + pnpm + Netlify  
**Agent Permissions**: Full workspace access | Auto-run operations | Auto-recover module issues

---

## 🚀 Quick Command Reference

### Build & Serve
```bash
pnpm install              # Install dependencies (auto-run if needed)
pnpm dev                  # Start dev server (http://localhost:1313)
pnpm build                # Production build (hugo --minify + pagefind)
pnpm run pagefind         # Regenerate search index only
```

### Hugo Module Recovery
```bash
hugo mod clean            # Clear module cache
hugo mod get -u           # Update modules
hugo mod tidy             # Clean unused modules
```

**When to use**: Module errors, import failures, or after git conflicts in `go.mod`/`go.sum`.

---

## 📁 Architecture & Edit Zones

### Primary Edit Zones
- **Content**: `content/` (markdown pages, newsfeed, blog, publications)
- **Site Config**: `config/_default/hugo.yaml`, `languages.yaml`, `params.yaml`
- **Author Data**: `data/authors/me.yaml` (main profile)
- **Custom Styles**: `assets/css/custom.css`
- **Layout Overrides**: `layouts/_partials/` (custom display logic)

### Generated (Never Edit)
- `public/` — Build output (regenerated every deploy)
- `resources/_gen/` — Hugo cache (regenerated on build)

### Database-like Files
- `hugo_stats.json` — Update after CSS class changes
- `.github/workflows/import-publications.yml` — References `content/publication/` (see Pitfalls)

---

## 📝 Content Conventions

### Frontmatter Format (YAML)
```yaml
---
title: "ページタイトル [日本語優先]"
date: 2026-04-01  # ISO 8601 format (YYYY-MM-DD)
authors:
  - me           # Always use 'me' for author
tags: []         # Optional tags
---
```

### File Naming Patterns
- **News articles**: `content/news/YYYYMMDD-XX.md` (e.g., `20260401-01.md`)
- **Blog posts**: `content/blog/<slug>/index.md`
- **Events/Presentations**: `content/events/<slug>/index.md`
- **Projects**: `content/projects/<slug>/index.md`
- **Publications (bulk)**: `content/publications/<descriptive-name>.md`

### Content Organization
```
content/
  _index.md                    # Home page (sections config)
  contact.md
  experience.md
  news/                        # Daily news/updates
  blog/                        # Long-form posts
  events/                      # Talks, workshops
  projects/                    # Research/side projects
  publications/                # Papers (plural!)
  courses/                     # Courses taught
  slides/                      # Slide decks
```

**Important**: Publications directory is `publications/` (plural), not `publication/`.

---

## 🔧 Common Operations

### Add News Item
1. Create `content/news/YYYYMMDD-XX.md` with frontmatter
2. Add date (today), authors: [me], title
3. Write markdown body
4. Rebuild: `pnpm build` (auto-indexing included)

### Update Home Page Sections
1. Edit `content/_index.md`
2. Modify `sections:` array to add/remove sections
3. Reference section files by their `_index.md` paths
4. Rebuild to verify

### Fix Hugo Module Issues
If you see errors like `failed to resolve output format` or `module not found`:
```bash
hugo mod clean
hugo mod get -u
hugo mod tidy
pnpm build
```

### Verify Build Locally
```bash
pnpm build
# Then inspect public/ folder for errors
```

Netlify build command (auto-runs on deploy):
```
hugo --gc --minify -b $URL --logLevel debug && pnpm run pagefind
```

---

## ⚠️ Known Pitfalls

### 1. **Publications Directory Mismatch**
- ✅ **Correct**: `content/publications/` (plural)
- ❌ **Wrong**: `content/publication/` (singular)
- ⚠️ **Issue**: `.github/workflows/import-publications.yml` references `content/publication/`, which doesn't exist. This is a known discrepancy.
- **Action**: Manually edit this workflow if auto-importing publications; or keep manual publication files in `publications/`.

### 2. **Public Folder Overwritten on Build**
- Do NOT edit files in `public/` — they regenerate with every build
- Always edit source files in `content/`, `config/`, or `layouts/`

### 3. **Language Default Won't Revert**
- If you change `defaultContentLanguage` from `ja` to anything else, existing ja-language pages may become orphaned
- Always keep `ja` as primary unless intentionally migrating the whole site

### 4. **Search Index Not Auto-Updated**
- `pnpm run pagefind` must run AFTER `hugo build` generates `public/`
- If using `pnpm build`, pagefind is already included; but verify `public/pagefind/` exists

### 5. **CSS Class Changes Not Recognized**
- After adding new Tailwind CSS classes to markdown or layouts:
  - Delete `resources/_gen/` folder and rebuild, OR
  - Let `hugo server` detect and recompile (usually automatic)
  - Verify updated `hugo_stats.json`

### 6. **Git Module Lock Issues**
- If `go.mod` or `go.sum` has merge conflicts:
  ```bash
  hugo mod tidy
  hugo mod get -u
  ```
  This resolves most SHA mismatches.

### 7. **Netlify vs Local Differences**
- Netlify uses: `hugo --gc --minify`
- Local dev: `hugo server --disableFastRender`
- If build works locally but fails in Netlify, check: `pnpm build` output with gc/minify flags

---

## 🎯 Agent Decision Tree

**When asked to edit content:**
1. Check if file exists in `content/` → Create with YAML frontmatter
2. Add `date: YYYY-MM-DD`, `authors: [me]`, `title: "..."`
3. After significant changes → Run `pnpm build` to validate
4. If module errors appear → Auto-run `hugo mod clean && hugo mod get -u && hugo mod tidy`

**When asked to modify config:**
1. Edit target file in `config/_default/`
2. Restart `pnpm dev` to see changes
3. Run `pnpm build` if major config changes (language, menu, etc.)

**When asked to add styling:**
1. Edit `assets/css/custom.css`
2. Use Tailwind v4 syntax (if new classes, rebuild)
3. Verify `hugo_stats.json` is updated

**When encountering build errors:**
1. Check if error mentions "module" → Run recovery sequence
2. Check if error mentions "css / styles" → Rebuild, clear cache
3. Check if error mentions "parse error" → Validate YAML frontmatter
4. Otherwise → Report with full error output

---

## 🌍 Language & Localization

- **Default**: Japanese (ja)
- **Config location**: `config/_default/languages.yaml` (languageCode: ja-JP)
- **Content**: Create lang-specific folders if adding non-ja content:
  - `content/news/index.ja.md` (Japanese)
  - `content/news/index.en.md` (English, if needed)

For now, **assume all content is Japanese** unless explicitly told otherwise.

---

## 📊 Automation Rules for This Workspace

- ✅ **Automatically execute**: Build, serve, pagefind, module recovery
- ✅ **Automatically fix**: YAML frontmatter mistakes, missing date fields
- ✅ **Ask first (optional)**: For large refactors (renaming multiple files, restructuring directories)
- ❌ **Never execute**: Workflow file edits (`.github/workflows/`) should be reviewed first

---

## 🔗 Reference Files

| File | Purpose |
|------|---------|
| [AGENTS.md](../../AGENTS.md) | Project-wide guidelines (build, architecture) — Source of truth |
| [config/_default/hugo.yaml](../../config/_default/hugo.yaml) | Hugo main config |
| [config/_default/languages.yaml](../../config/_default/languages.yaml) | Language settings |
| [data/authors/me.yaml](../../data/authors/me.yaml) | Author profile (used in all posts) |
| [netlify.toml](../../netlify.toml) | Netlify build config (parity check: use `--gc --minify`) |
| [package.json](../../package.json) | pnpm scripts (dev, build, pagefind) |
| [.github/workflows/](../../.github/workflows/) | CI/CD automation |

---

## ✨ Pro Tips

1. **Linking between content**:
   - Use relative paths in markdown: `[Link](../other-page/)`
   - Hugo will resolve them correctly

2. **Front matter helpers**:
   - Always run `date: $(date +"%Y-%m-%d")` locally to get today's date
   - Copy `authors: [me]` template from existing files

3. **Before committing**:
   - Run `pnpm build` to catch errors early
   - Verify `public/` doesn't have stale content

4. **Debugging search issues**:
   - Search index lives in `public/pagefind/`
   - If search broken → delete `public/` and rebuild
   - Verify metadata (`title`, `date`) in frontmatter (Pagefind indexes these)

---

## 🚨 Emergency Recovery

**If "nothing works" and all rebuilds fail:**
```bash
hugo mod clean              # Clear module cache
rm -r resources/_gen        # Clear Hugo build cache
rm -r public                # Clear output
pnpm install                # Reinstall dependencies
pnpm build                  # Full rebuild
```

Then verify:
- [x] `public/index.html` exists and has content
- [x] `public/pagefind/` directory exists
- [x] No TypeScript/YAML parsing errors in output

---

**Last Updated**: 2026-04-01  
**For Agents**: Follow this document + AGENTS.md as your north star. When in doubt, prioritize content safety and verify builds.
