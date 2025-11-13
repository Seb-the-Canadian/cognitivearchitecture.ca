# Obsidian Publish Alignment Plan

Use this checklist to bring the vault in line with Obsidian Publish best practices. Update the status line at the top and tick checkboxes as each task is completed.

---
## Status
- [ ] Plan not started
- [ ] Plan in progress
- [ ] Plan complete

---
## 1. Content Inventory & Metadata
- [x] Export a note list (title, path, publish status) for reference
- [x] Confirm all published notes have frontmatter `status`, `tags`, `created`, `last tended`
- [x] Flag notes that should remain private or need redaction before publishing
- [x] Standardize tag taxonomy (e.g. `#evergreen`, `#greenhouse`, `#grove`, `#shed`)
- [x] Ensure headings and file names are slug-friendly and human-readable

### Note inventory (2025-11-12)
| Title | Path | Publish status |
| --- | --- | --- |
| Home | Home.md | Public |
| About me | About me.md | Public |
| About the site | About the site.md | Public |
| The Greenhouse | The Greenhouse.md | Public |
| The Grove | The Grove.md | Public |
| The Shed | The Shed.md | Public |
| Publish Alignment Plan | Meta/Operations/Publish Alignment Plan.md | Private |
| Tag Glossary | Meta/Tag Glossary.md | Private |
| The Workshop | Meta/99_Archive/The Workshop.md | Private |

## 2. Site Structure & Navigation
- [x] Document the intended role of top-level sections (Home, Greenhouse, Grove, Shed, Meta)
- [x] Verify each published note belongs to a section or hub index
- [x] Create or update navigation blocks (tables of contents, link hubs, callouts) where missing
- [x] Resolve broken or missing internal links using Obsidian's graph and backlink panes
- [x] Review embedded content (transclusions) for publish readiness

### Structure review (2025-11-12)
- Documented section purposes in [[Site Structure Overview|Meta/Operations/Site Structure Overview]].
- Confirmed coverage for published pages:
  - `Home.md` serves as landing hub with "Gates" and "Paths" navigation.
  - `The Greenhouse.md`, `The Grove.md`, `The Shed.md`, `About me.md`, and `About the site.md` now include navigation footers linking across core sections.
- No additional navigation gaps identified during manual review; follow-up tasks captured below.
- Created placeholder notes for previously-unresolved links (`digital garden`, `Digital Gardens Index`, `Cognitive Architecture`, and `Lightweight Tools for Knowledge Architecture — Business Case Study`) to avoid broken references.
- Verified the only embed (`![[Tag Glossary]]`) renders correctly on the Home page.

## 3. Media & Attachments
- [x] Move published media into `Meta/Site Attachments/` with descriptive names
- [~] Compress or resize large images for web delivery (< 500 KB where possible)
- [x] Confirm all image embeds use relative vault paths
- [x] Remove unused attachments or archive them outside the publish tree

### Media review (2025-11-12)
- Identified `Meta/Site Attachments/logo.png` as the only asset used by published notes.
- Resized the logo to 800 × 800 to reduce footprint (now ~1.1 MB); still above the 500 KB target—consider further compression if needed.
- Verified that all notes reference media via vault-relative paths and no unused attachments are present.
- Exception: retain current logo quality despite size > 500 KB; revisit if additional images are introduced or performance issues emerge.

## 4. Visual Styling & UX
- [x] Catalogue existing theme changes and CSS snippets
- [x] Define the callout palette (name, purpose, icon) and document usage guidelines
- [ ] Test published pages on mobile, tablet, and desktop for layout issues
- [ ] Note typography or spacing tweaks to implement in `publish.css`
- [ ] Plan accessibility checks (contrast, heading hierarchy, link clarity)

### Styling review (2025-11-12)
- Confirmed `publish.css` as the sole custom styling touchpoint; no additional snippets are active while `.obsidian` remains ignored from version control.
- Documented active callouts (info, warning, tldr, gate) with icon assignments and usage notes in [[Callout Palette|Meta/Operations/Callout Palette]].
- Pending responsive spot checks across breakpoints and deeper typography/accessibility tuning during subsequent passes.

## 5. SEO & Social Sharing
- [ ] Set site-wide title, description, and custom domain (if applicable)
- [ ] Draft reusable meta description or abstract for key notes
- [ ] Configure Open Graph / Twitter card defaults via `publish.css` or frontmatter
- [ ] Verify canonical URLs and sitemap generation inside Publish dashboard
- [ ] Identify cornerstone content to feature on Home page or navigation hubs

## 6. Workflow & Maintenance
- [ ] Define the draft → review → publish workflow (tools, roles, cadence)
- [ ] Create a pre-publish checklist (links, callouts, metadata, images)
- [ ] Schedule regular tending (e.g. monthly review of `last tended` notes)
- [ ] Track changes or release notes for public transparency
- [ ] Document how to sync desktop snippets with Publish `publish.css`

---
## Next Actions Log
Use this section to record immediate follow-ups.

- [ ] 
- [ ] 
- [ ] 
