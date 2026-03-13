---
created: 2026-03-11
last_tended: 2026-03-11
type: effort
tags:
  - migration
  - infrastructure
up:
  - "[[cognitivearchitecture_ca]]"
---

# Project Plan: Migrate cognitive-architecture.ca from Obsidian Publish to 11ty

## Context

You're moving your digital garden (cognitive-architecture.ca) from Obsidian Publish ($8/month, zero-ops, constrained DOM) to a self-hosted 11ty static site. The motivation is sovereignty and design freedom — not cost savings. You already run an 11ty site (sebthecanadian.ca), so the build system is familiar. The vault contains 138 markdown files with consistent frontmatter, 817 wikilinks, 73 callout blocks (~half using Nick Milo custom types), and a 4,627-line publish.css that won't transfer.

The strategy: **migrate first, enhance second.** Stage 1 gets the garden live with content parity. Stage 2 layers capabilities that Obsidian Publish can't offer (graph view, type-driven templates, Pagefind search, OG images).

All estimates assume **AI pairing** (Claude scaffolding code, debugging build issues). Without pairing, multiply by ~1.5x.

---

## Three Architecture Decisions

### 1. Source Model: Vault IS the 11ty Project

Add 11ty config directly to the vault repo. No symlinks, no submodules, no sync scripts.

```
cognitivearchitecture_ca/           ← Vault root AND 11ty project
├── eleventy.config.js              ← 11ty config
├── package.json                    ← Node dependencies
├── _build/                         ← Templates, CSS, JS (gitignored by Obsidian)
│   ├── layouts/
│   ├── includes/
│   ├── css/
│   ├── js/
│   └── data/
├── _site/                          ← Build output (gitignored)
├── .github/workflows/deploy.yml    ← CI/CD
├── .obsidian/                      ← Excluded from 11ty build
├── _meta/                          ← Excluded from 11ty build
├── publish.css                     ← Excluded from 11ty build
├── CLAUDE.md                       ← Excluded from 11ty build
├── Atlas/                          ← Content (11ty reads this)
├── Home.md                         ← Content
└── ...
```

**Why this over symlink/submodule:** One repo, one commit, one deploy. You edit in Obsidian, the `_build/` folder is invisible to your writing flow (underscore prefix hides it in Obsidian's explorer). No cross-repo coordination, no git submodule commands to remember. The vault *is* the project.

**Obsidian coexistence:** `eleventy.config.js`, `package.json`, and `_build/` show in Obsidian's file explorer but Obsidian ignores non-markdown files. You can exclude `_build/` and `_site/` from Obsidian's file explorer in Settings → Files & Links → Excluded files.

### 2. Hosting: Cloudflare Pages

You already use Cloudflare for DNS. Cloudflare Pages auto-detects 11ty projects — push to main, it builds and deploys. No GitHub Actions config needed. Faster builds (~1-2 min vs 5-10 min), global CDN included, edge functions available for future enhancements.

Setup: connect GitHub repo → set build command (`npm run build`) → set output dir (`_site`) → add custom domain. Done.

### 3. Publish Filtering: Folder-Based with Override

**Public by default:** Root gate pages + everything under `Atlas/The Almanac/`
**Private by default:** `Atlas/Seeds/`, `_meta/`, `.obsidian/`, `_build/`
**Override:** `publish: false` in frontmatter hides any individual note; `publish: true` forces inclusion of any note regardless of folder.

This matches your existing vault structure and requires minimal frontmatter changes.

---

## Stage 1: Migrate & Stabilize

**Goal:** Garden live on 11ty at cognitive-architecture.ca with content parity to Obsidian Publish.
**Estimated total: 35–50 hours** (with AI pairing)

### Phase 1A — Content Prep (4–6h)

**What:** Clean the vault for 11ty consumption. No code yet.

| Task | Hours | Details |
|------|-------|---------|
| Normalize `last_tended` field | 0.5h | Fix space-vs-underscore inconsistency across all files. Find & replace in Obsidian. |
| Standardize `status` field | 0.5h | Ensure string (not array) everywhere. |
| Define URL slugs | 1–2h | Document the mapping: `Greenhouse (index)/` → `/greenhouse/`, spaces → hyphens, strip parenthetical suffixes. Create a reference table in `_meta/url-structure.md`. |
| Audit broken wikilinks | 1–1.5h | Grep all `[[targets]]`, cross-reference against filenames. Fix any orphans. |
| Review publish surface | 1h | Walk Obsidian Publish's current live pages. Confirm the folder-based rules capture exactly the same set. |

**Deliverable:** Clean vault ready for 11ty. URL mapping documented.
**Risk:** Low. All work happens in Obsidian.

### Phase 1B — 11ty Scaffolding (3–5h)

**What:** Initialize the project, get a successful build with raw (unstyled) markdown output.

| Task | Hours | Details |
|------|-------|---------|
| Initialize project | 0.5h | `npm init`, install `@11ty/eleventy`, create `eleventy.config.js` with input/output dirs and ignore patterns for `.obsidian/`, `_meta/`, `_build/`, `publish.css`, `CLAUDE.md`, `README.md`, `node_modules/`, `_site/`. |
| Minimal layout | 1h | `_build/layouts/base.njk` — bare HTML5 document with `{{ content \| safe }}`. Just enough to render pages. |
| Configure collections | 1h | `allNotes` collection with publish filtering. `byType`, `byStatus` collections for future use. |
| First build test | 1–2h | Run `npx eleventy --serve`. Debug any path/filename issues (parentheses in folder names, colons in filenames, special chars). Budget time here — this is where edge cases surface. |

**Deliverable:** `npx eleventy` succeeds. All 138 files build. Pages render as raw HTML (no styling, no wikilink resolution).
**Risk:** Medium. Filenames with special chars (`(`, `.`, `:`) may cause build errors. Fix by renaming or configuring permalink overrides.
**Key file:** `eleventy.config.js`

### Phase 1C — Wikilinks & Backlinks (4–6h)

**What:** Internal links work. Backlinks display.

| Task | Hours | Details |
|------|-------|---------|
| Install eleventy-plugin-interlinker | 0.5h | `npm install @photogabble/eleventy-plugin-interlinker`. Configure in `eleventy.config.js`. |
| Build slug resolution map | 1–1.5h | The plugin needs a mapping of note titles → URLs. Configure the plugin's resolver to handle your folder structure and slugification rules. Handle case-insensitive matching (Obsidian is case-insensitive). |
| Handle aliased wikilinks | 0.5h | Plugin supports `[[Note\|Display]]` natively — verify with your 69 aliased links. |
| Handle `up:` field links | 1h | The `up:` frontmatter field contains wikilinks in YAML. These need a Nunjucks filter to resolve them in templates (not in markdown body). Write a `resolveWikilink` filter. |
| Backlinks template component | 1–1.5h | Plugin exposes backlinks data per page. Create `_build/includes/backlinks.njk` that renders the "Linked from" section. |
| Verify | 0.5h | Spot-check 10 notes for correct link resolution. Check backlinks on a well-linked note like `Cognitive Architecture`. |

**Deliverable:** All 817 wikilinks resolve. Backlinks display on every note.
**Risk:** Medium. Slug resolution edge cases (duplicate titles across folders, special characters). The plugin is actively maintained but may not handle every Obsidian edge case.
**Key packages:** `@photogabble/eleventy-plugin-interlinker`

### Phase 1D — Callout Rendering (3–5h)

**What:** All 73 callout blocks render as styled HTML, including Nick Milo custom types.

| Task | Hours | Details |
|------|-------|---------|
| Install markdown-it-obsidian-callouts | 0.5h | `npm install markdown-it-obsidian-callouts`. Configure with 11ty's `amendLibrary("md", ...)`. |
| Extract active callout types | 0.5h | From the vault audit: 15 custom types actually in use (milestone, connect, map, tldr, warning, info, quote, etc.). Document their intended colors and icons (extract from the Nick Milo section of `publish.css`). |
| Create callout CSS | 1.5–2.5h | Write CSS for all 15 types. Lucide icons via CDN (`https://unpkg.com/lucide-static/icons/`). Colors extracted from publish.css. Standard callouts (note, warning, info) get standard treatment. Custom types (milestone, connect, map) get their Nick Milo colors. |
| Handle Obsidian comments | 0.5h | Strip `%% ... %%` blocks in a markdown-it plugin or post-process step. These are Waypoint markers and hidden comments — they should not appear in output. |
| Verify | 0.5h | Check Home.md (heavy callout usage), a Shed page, and a Concept page. |

**Deliverable:** Callouts render with correct icons, colors, and structure.
**Risk:** Low-Medium. The npm package handles the syntax parsing. The main work is CSS.
**Key packages:** `markdown-it-obsidian-callouts`

### Phase 1E — Layout & Navigation (5–8h)

**What:** The site looks like a site. Base layout, note template, gate pages, index pages, breadcrumbs, responsive.

| Task | Hours | Details |
|------|-------|---------|
| Base layout | 1.5–2h | `base.njk`: HTML5 skeleton, CSS link, header (logo + dark mode toggle), sidebar nav (gates + maps), main content area, footer. Use CSS Grid. |
| Note template | 1–1.5h | `note.njk`: title, metadata bar (created, last_tended, status badge, type), content body, tags, `up:` parent links, backlinks section. |
| Gate/home template | 1–1.5h | `gate.njk`: for Home.md, The Grove.md, etc. Wider layout, hero area, preserves inline SVG icons (or replaces with emoji if SVGs are stripped). |
| Index/archive template | 1h | `archive.njk`: lists notes with title, excerpt, date, status badge. Used for `/atlas/`, `/concepts/`, `/tags/[tag]/`. |
| Tag pages | 0.5–1h | Auto-generate a page per tag using 11ty's tag pagination. |
| Breadcrumbs | 0.5h | Nunjucks include that derives path from URL segments. |
| Dark mode | 1h | CSS custom properties for light/dark palette. JS toggle that saves to localStorage. Forest green accent (`#3f734a`) in both modes. |
| Responsive | 0.5–1h | Collapse sidebar on mobile. Readable font sizes. Touch-friendly targets. |

**Deliverable:** Fully navigable site with consistent layout, dark mode, and responsive design.
**Risk:** Medium. This is the most creative phase — you'll iterate on visual decisions. Budget for "it doesn't look right yet" time.

### Phase 1F — Design Porting (3–5h)

**What:** Port the Data Druid aesthetic from publish.css. Not pixel-perfect parity — design *intent*.

| Task | Hours | Details |
|------|-------|---------|
| Extract palette from publish.css | 0.5h | Accent: `#3f734a`. Background, text, border, link colors for light and dark modes. |
| Font strategy | 1h | AppleMyungjo is macOS-only. Pick a cross-platform serif: EB Garamond (Google Fonts, free, similar weight) or Crimson Text. Set up `@font-face` or Google Fonts import. |
| CSS custom properties | 1–1.5h | Define `--color-accent`, `--color-bg`, `--color-text`, `--color-border`, `--font-body`, `--font-heading`, etc. All components reference these. |
| Status badges | 0.5–1h | Visual indicators for seed/sprout/sapling/evergreen. Small colored pills or icons next to note titles. |
| Polish pass | 0.5–1h | Spacing, link hover states, code block styling, table formatting. |

**Deliverable:** Site has the Data Druid feel — forest green, serif typography, garden metaphor in visual language.
**Risk:** Low. This is CSS work against a DOM you control. No fighting someone else's selectors.
**Note:** Vanilla CSS with custom properties, not SCSS. Avoids the SCSS learning curve. You can migrate to SCSS later if you want nesting/mixins.

### Phase 1G — Assets & Deployment (3–4h)

**What:** Images work, CI/CD works, site is deployed.

| Task | Hours | Details |
|------|-------|---------|
| Image passthrough | 0.5h | Configure `addPassthroughCopy` for `_meta/Site Attachments/`. Update image embed resolution (the wikilink plugin should handle `![[image.jpg]]` → `<img src="...">` paths). |
| Cloudflare Pages setup | 1h | Connect GitHub repo. Build command: `npm run build`. Output: `_site`. Add `cognitive-architecture.ca` as custom domain. |
| DNS configuration | 0.5h | Point `cognitive-architecture.ca` CNAME to Cloudflare Pages domain. Lower TTL 24h before cutover. |
| 404 page | 0.5h | Custom 404.md with garden-themed message and navigation links. |
| Staging verification | 1h | Full walkthrough on the Cloudflare Pages preview URL before DNS cutover. |

**Deliverable:** Site live at cognitive-architecture.ca (or staging URL).
**Risk:** Low. You've done this before with sebthecanadian.ca.

### Phase 1H — POSSE Pipeline & QA (4–6h)

**What:** RSS feed works. POSSE bridge to sebthecanadian.ca works. All links verified.

| Task | Hours | Details |
|------|-------|---------|
| RSS feed | 1h | Install `@11ty/eleventy-plugin-rss`. Create `feed.njk` template generating Atom feed at `/feed.xml`. |
| Vault JSON export | 1h | Create `_build/data/vault.11tydata.js` that exports all published note metadata as JSON at `_site/vault.json`. This replaces the Obsidian Publish cache manifest as the POSSE data source. |
| Rebuild garden-rss.js | 1–1.5h | Point it at `vault.json` instead of the Obsidian Publish API. Preserve `gardenPosts.json` output format for sebthecanadian.ca compatibility. |
| Link checker | 0.5–1h | Run a link checker against the built site. Fix any broken internal links. |
| End-to-end POSSE test | 0.5h | Build garden → generate vault.json → run garden-rss.js → verify gardenPosts.json → verify sebthecanadian.ca can consume it. |

**Deliverable:** POSSE pipeline working. RSS feed valid. All links verified.
**Risk:** Medium. The gardenPosts.json contract must match exactly what sebthecanadian.ca expects. Test carefully.

### Phase 1 — Launch Checklist

DNS cutover happens when all of these are green:

- [ ] All published notes render without build errors
- [ ] All wikilinks resolve (no dead links in output)
- [ ] Backlinks display on every note
- [ ] All 73 callouts render with correct styling
- [ ] Images load
- [ ] Dark mode works
- [ ] Mobile responsive
- [ ] RSS feed validates (feedvalidator.org)
- [ ] POSSE pipeline produces correct gardenPosts.json
- [ ] Cloudflare Pages builds succeed on push
- [ ] Obsidian Publish remains live as fallback for 1 week post-cutover

**Stage 1 total: 35–50 hours** (with AI pairing)

---

## Stage 2: Enhancement Pipeline

Once stable, these are independent workstreams. Prioritize by what creates the most value for readers and for your own gardening practice.

### Enhancement 1: Pagefind Search (2–3h)
- Install Pagefind, configure post-build indexing
- Add search UI component to sidebar or header
- **Why first:** High value, low effort. Better than Obsidian Publish's search.
- **Package:** `pagefind`

### Enhancement 2: Type-Driven Templates (4–6h)
- Distinct templates for Claims (proposition card), Questions (inquiry format with linked claims), Concepts (definition + connections layout), Seeds (minimal, clearly-unfinished)
- Status-driven visual treatment (seeds look sparse, evergreens look substantial)
- **Why second:** This is the capability that most differentiates 11ty from Publish. Your content types become first-class design elements.

### Enhancement 3: Graph View (8–12h)
- Build link graph JSON at build time (nodes from published notes, edges from wikilinks)
- D3.js force-directed visualization
- Nodes colored by status, sized by link count, clustered by thematic map
- Click to navigate, zoom/pan, highlight neighborhoods
- **Why this is worth building custom:** Your graph encodes semantic structure (claims → concepts → questions). A generic graph treats all links equally. Yours can visualize the garden's *architecture*.
- **Package:** `d3` (v7)

### Enhancement 4: Hover Previews (2–4h)
- On wikilink hover, show tooltip with note title + first paragraph
- Lightweight implementation: fetch target page excerpt at build time, embed as data attributes, render with JS on hover
- **Package:** `@floating-ui/dom` (lightweight Popper.js successor)

### Enhancement 5: OG Images (2–4h)
- Per-note social cards generated at build time
- Note title, status badge, garden branding, forest green background
- **Package:** `@11ty/eleventy-img` + `satori` or `@vercel/og`

### Enhancement 6: Full Data Druid Aesthetic (6–10h)
- Pixel-art borders or forest-themed ornamental elements
- Custom SVG flourishes for gate pages
- Micro-animations (e.g., seedling icon grows on hover)
- Typography refinement — OpenType features, proper small caps, ligatures
- This is the creative sprint where the site becomes unmistakably *yours*

**Stage 2 total: 24–39 hours** (independent workstreams, do in any order)

---

## Recommended Execution Order

```
Week 1-2:  Phase 1A (content prep) + Phase 1B (scaffolding)
Week 2-3:  Phase 1C (wikilinks) + Phase 1D (callouts)
Week 3-4:  Phase 1E (layout) + Phase 1F (design)
Week 4-5:  Phase 1G (deploy) + Phase 1H (POSSE + QA)
Week 5:    DNS cutover + 1 week monitoring
Week 6+:   Stage 2 enhancements (Pagefind first, then type templates, then graph)
```

This assumes ~8-10h/week of focused work. Faster if you sprint; slower if life happens. The phases are sequential within Stage 1 (each depends on the previous), but Stage 2 items are independent and can be done in any order.

---

## Key Packages

| Package | Purpose | Phase |
|---------|---------|-------|
| `@11ty/eleventy` | Static site generator | 1B |
| `@photogabble/eleventy-plugin-interlinker` | Wikilinks + backlinks | 1C |
| `markdown-it-obsidian-callouts` | Callout block rendering | 1D |
| `@11ty/eleventy-plugin-rss` | RSS/Atom feed | 1H |
| `pagefind` | Full-text search | 2.1 |
| `d3` | Graph visualization | 2.3 |
| `@floating-ui/dom` | Hover previews | 2.4 |

---

## Verification Plan

After each phase:
1. Run `npx eleventy --serve` and browse locally
2. Spot-check 10 notes (1 gate page, 2 concepts, 2 claims, 2 seeds, 1 question, 1 framework, 1 essay)
3. Check mobile view in browser dev tools
4. Run link checker before deployment phases

Before DNS cutover:
1. Full walkthrough on Cloudflare Pages preview URL
2. Compare every published page against Obsidian Publish version
3. Validate RSS feed at feedvalidator.org
4. Test POSSE pipeline end-to-end
5. Lighthouse audit (target >85)

---

## What This Plan Does NOT Include

- Obsidian-git plugin setup (you may want this for auto-committing vault changes — separate concern)
- Newsletter/Buttondown pipeline changes (this is external and doesn't change)
- Analytics setup (consider Plausible or Fathom if you want privacy-respecting analytics)
- Consolidation with sebthecanadian.ca (possible future project, not in scope)
