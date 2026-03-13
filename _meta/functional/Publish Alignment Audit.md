---
created: 2025-11-13
last_tended: 2026-01-22
type: effort
tags:
  - stub
up:
  - "[[cognitivearchitecture_ca]]"
---
# Obsidian Publish Alignment Audit

This document captures the current state of the Cognitive Architecture vault relative to recommended Obsidian Publish practices. Sources reference guidance from the official documentation: [Obsidian Publish › Publish sites](https://help.obsidian.md/Obsidian+Publish/Publish+sites) and [Obsidian Publish › Customize your site](https://help.obsidian.md/Obsidian+Publish/Customize+your+site).

---
## Snapshot

| Area | Current State | Alignment Assessment | Notes |
| --- | --- | --- | --- |
| Content scope (`.obsidian/publish.json`) | `included: []`, `excluded: ["Drafts", "01_Admin/Meta/Templates"]` | **At risk** | Empty `included` list means anything manually selected can ship; doc recommends explicit folder inclusion to prevent accidental publishes.
| Root structure | Mix of publishable pages and support directories in vault root | **At risk** | Docs encourage clear separation of public content from back-office material to simplify navigation controls.
| Navigation visibility | `Meta/` shows structural assets (tag glossary, archives) | **Partial** | Hidden folders need either exclusion or explicit unpublish so they do not surface in Publish sidebar.
| Page slugs | Filenames with spaces (e.g., `About me.md`) | **Partial** | Use `permalink` frontmatter or rename files to keep clean URLs as suggested in customization guide.
| Theme customization | `publish.css` contains full Minimal theme copy | **Misaligned** | Docs advise using built-in theme selection and keeping `publish.css` to small overrides to ease maintenance.
| Attachment handling | Assets consolidated under `Meta/Site Attachments/` | **Aligned** | Matches recommendation to store media in a predictable folder and keep it excluded unless directly published.

---
## Priority Actions

1. **Restrict published scope** (Publish sites › Manage your site):
   - Populate `included` with the handful of public folders (e.g., `Home.md`, `The Grove/`, `The Greenhouse/`, `The Shed/`).
   - Keep drafts, templates, and archives in `excluded` to protect them from manual selection mistakes.

2. **Restructure top-level content** (Publish sites › Organize your vault):
   - Create a parent folder (e.g., `Garden/`) for all public-facing notes.
   - Move administrative folders (`Meta/`, `Drafts/`, archives) out of the published tree or mark them excluded.

3. **Tighten navigation** (Publish sites › Manage your site navigation):
   - For support folders that must remain in the vault, mark them Hidden or Excluded in Publish so they do not appear in the sidebar.
   - Curate the default navigation links to match the “Gates” and “Paths” taxonomy described on `Home.md`.

4. **Stabilize URLs** (Customize your site › Page settings):
   - Add a `permalink` value to any note whose filename contains spaces or capitalization you may want to change later.
   - Optionally rename files to slugified versions (e.g., `about-me.md`) to reduce reliance on redirects.

5. **Streamline custom CSS** (Customize your site › Theme and styling):
   - Install the Minimal theme through Publish settings instead of embedding the full CSS in `publish.css`.
   - Retain only bespoke overrides in `publish.css` so future theme updates do not require manual merges.

---
## Supporting Details

- **Attachment policy**: Publish automatically bundles files stored alongside published notes. Keeping media in a dedicated directory aligns with the documentation; just confirm the folder stays hidden or excluded unless assets should surface publicly.
- **Metadata hygiene**: Frontmatter already uses `status`, `tags`, and `last tended`. When adding `permalink`, follow the same YAML block for consistency.
- **Testing workflow**: After restructuring `publish.json`, use the Publish preview modal to confirm only intended notes appear in the queue before pushing updates.

---
## Next Review

Revisit this alignment check after the folder restructure and CSS cleanup, or sooner if new sections (e.g., additional "Gates" or "Paths") are published.
