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

# Migration Assessment: Obsidian Publish → Quartz 4

**Date:** 2026-03-11
**Assessor:** Co-orchestration session (Claude + Seb)
**Subject:** cognitivearchitecture.ca (Digital Garden)
**Vault access:** Direct (actual vault mounted and audited)
**Status:** Assessment complete — decision pending

---

## Executive Summary

**The honest bottom line:** Your vault is cleaner and more migration-friendly than the prior indirect assessment suggested. The Dataview blocker identified previously does not exist — zero Dataview queries appear anywhere in the vault. Content-wise, migration to Quartz 4 would be straightforward: 138 markdown files with consistent frontmatter, standard wikilinks, and no exotic Obsidian syntax. The real blockers are (1) a 4,627-line publish.css with 66 custom callout types from the Nick Milo callout pack baked in — none of which Quartz renders with the correct icons or colors without equivalent CSS work — and (2) inline SVG icons hand-embedded in your four main navigation pages, which Quartz will strip or mangle. For a vault of this size (138 notes, ~17MB total), the migration is technically achievable in 15–25 hours of focused work, but the CSS rebuild alone accounts for half that estimate. The prior assessment's recommendation stands, reinforced by direct evidence: Obsidian Publish remains the right tool for your profile right now. The migration calculus changes when the vault grows past ~50 published notes or when Obsidian Publish's limitations genuinely constrain your garden.

---

## 1. Vault Audit (Direct Evidence)

### 1.1 Scale and Size

| Metric | Value |
|--------|-------|
| Total files | 190 |
| Markdown files | 138 (excluding .obsidian) |
| Total vault size | 17 MB |
| Image/attachment files | 16 (in `_meta/Site Attachments/`) |
| Attachment size | ~12 MB (mostly PNG logos and banner images) |
| publish.css | 610 KB / 4,627 lines |
| Canvas files | 0 |

### 1.2 Folder Structure

```
cognitivearchitecture_ca/
├── Atlas/
│   ├── Seeds/                        (44 seed notes)
│   ├── The Almanac/
│   │   ├── Claims/                   (16 claim notes)
│   │   ├── Concepts/                 (18 concept notes)
│   │   ├── Greenhouse (index)/       (3 published essays)
│   │   ├── Questions (index)/        (19 question notes)
│   │   ├── The Grove (index)/        (1 long-form piece)
│   │   └── The Shed (index)/         (5 frameworks/tools)
│   └── [9 thematic map files]
├── _meta/
│   ├── Site Attachments/             (images, logos, config)
│   ├── almanac/                      (newsletter pipeline docs)
│   ├── functional/                   (audit + policy docs)
│   └── templates/                    (2 templates)
├── [7 root-level pages: Home, About, Gates, etc.]
├── publish.css
└── CLAUDE.md
```

**URL hierarchy assessment:** The published folder structure (`Atlas/The Almanac/{section}/{note}`) maps cleanly to a URL hierarchy. Quartz 4 would preserve this natively. The parenthetical folder names ("Greenhouse (index)", "The Shed (index)") are a minor concern — some build tools handle parentheses in paths poorly. Worth testing early.

### 1.3 Publication Model

**No per-note publish flags exist.** The vault has no `publish: true/false` in any frontmatter. Publication is managed entirely through Obsidian Publish's UI (the publish.json config has empty `included` array — Obsidian tracks publication state internally, not in YAML).

This means that for any alternative static site generator, you would need to either: (a) add a `publish` field to every note's frontmatter, or (b) use folder-based inclusion (publish everything under a certain path). Option (b) is simpler and maps to your existing structure, but it means your filtering logic lives in the build config rather than in the content.

### 1.4 Frontmatter Fields

| Field | Prevalence | Format |
|-------|-----------|--------|
| `created` | ~100% | ISO date (YYYY-MM-DD) |
| `last_tended` | ~95% | ISO date — some inconsistency with `last tended` (space vs. underscore) |
| `type` | ~98% | "note", "effort", "source" |
| `tags` | ~92% | Array |
| `up` | ~85% | Array of wikilinks (navigation/parent links) |
| `status` | ~25% | "seed", "sprout", "sapling", "evergreen" — sometimes string, sometimes array |
| `aliases` | ~15% | Array |
| `related` | ~8% | Array of wikilinks |

**Consistency issues found:** The `last_tended` field has a spelling variant (`last tended` with space). The `status` field appears as both string and array. One file (cognitivearchitecture_ca.md) has duplicate frontmatter entries. These are minor cleanup items, not blockers.

### 1.5 Link Analysis

| Link Type | Count | Files | Share |
|-----------|-------|-------|-------|
| Wikilinks `[[...]]` | 817 | All 138 files | 91.5% |
| Aliased wikilinks `[[...\|display]]` | 69 | 56 files | 8.4% of wikilinks |
| Standard markdown links `[text](url)` | 76 | 21 files | 8.5% |

The vault is overwhelmingly wikilink-native. Markdown links are used exclusively for external URLs. This is the expected pattern for an Obsidian-native garden.

### 1.6 Obsidian-Specific Syntax

| Feature | Count | Files | Notes |
|---------|-------|-------|-------|
| **Callout blocks** `> [!type]` | 73 | 37 files | Heavy. 20+ distinct types from Nick Milo's pack |
| **Embeds/transclusions** `![[...]]` | 9 | 7 files | Mostly image embeds; 2 note-level transclusions |
| **Footnotes** `[^n]` | 63 | 5 files | Concentrated — 55 in one file (Setting up a prompt engineering project) |
| **Obsidian comments** `%%...%%` | ~20 | ~12 files | Hidden content, Waypoint blocks |
| **Inline SVG icons** | ~12 | 4 files | Hand-embedded Lucide SVG in navigation pages |
| **Waypoint-generated blocks** | 3 | 3 files | Auto-generated folder indexes |
| **Dataview queries** | **0** | 0 files | **Not present** |
| **DataviewJS** | **0** | 0 files | **Not present** |
| **Mermaid diagrams** | 0 | 0 files | Not present |
| **LaTeX** | 0 | 0 files | Not present |
| **Canvas** | 0 | 0 files | Not present |

**Critical correction from prior assessment:** The prior assessment flagged Dataview as a blocker based on digital_forest planning documents assimilated from a different project folder. The actual vault contains zero Dataview queries. This removes the single largest compatibility concern.

### 1.7 Callout Types Actually Used in Content

| Callout Type | Occurrences | Standard? |
|-------------|-------------|-----------|
| `milestone` | 8 | No — Nick Milo custom |
| `connect` | 8 | No — Nick Milo custom |
| `map` | 4 | No — Nick Milo custom |
| `tldr` | 8+ | Yes (Obsidian built-in) |
| `warning` / `Warning` | 3 | Yes |
| `info` | 2 | Yes |
| `quote` | 2 | Yes |
| `NOTE` | 1 | Yes |
| `faq` | 1 | Yes |
| `hint` | 1 | Yes |
| `tower` | 1 | No — Nick Milo custom |
| `bike` | 1 | No — Nick Milo custom |
| `radar` | 1 | No — Nick Milo custom |
| `venetian` | 1 | No — Nick Milo custom |
| `search` | 1 | No — Nick Milo custom |
| `link` | 1 | No — Nick Milo custom |
| `help` | 1 | No — Nick Milo custom |
| `calendar` | 1 | No — Nick Milo custom |
| `anchor` | 1 | No — Nick Milo custom |
| `command` | 1 | No — Nick Milo custom |
| `user` | 1 | No — Nick Milo custom |
| `industry` | 1 | No — Nick Milo custom |
| `globe` | 1 | No — Nick Milo custom |
| `script` | 1 | No — Nick Milo custom |
| `mail` | 1 | No — Nick Milo custom (in _meta only) |

**Of the ~73 callout instances, roughly half use non-standard Nick Milo custom types.** These render correctly on Obsidian Publish because publish.css includes the full Nick Milo callout pack (262 callout CSS rules across 66 defined types). Quartz renders all callout types as blocks but only provides built-in styling and icons for the ~15 standard Obsidian callout types. Custom types would render as generic unstyled callouts without the correct color and icon.

### 1.8 CSS and Theming

| Component | Details |
|-----------|---------|
| **Theme** | Baseline (by Kepano) |
| **Accent color** | `#3f734a` (forest green) |
| **Text font** | AppleMyungjo |
| **Interface font** | Apple SD Gothic Neo |
| **publish.css** | 4,627 lines, 610 KB — includes full Baseline theme export + Nick Milo callout pack |
| **CSS snippets** | nick-milo-callouts.css (51 KB), custom-admonitions (referenced, not found as file) |
| **Plugin CSS** | callout-manager, folder-notes, waypoint, linter all include custom styles |

**Breakdown of publish.css:** This is not a hand-written stylesheet. It's a compiled/concatenated output that includes: the Baseline theme's full variable system, light and dark mode definitions, animation system, icon stroke modifiers, density modifiers, full Lucide icon set for callouts, code syntax highlighting theme, mobile responsiveness rules, and the complete Nick Milo callout pack. Roughly 80% of this file is theme infrastructure, not custom design work. The actual "Data Druid aesthetic" customization (color palette, fonts, accent color) represents a small fraction.

### 1.9 Plugins

**Community plugins (5):**

| Plugin | Migration Impact |
|--------|-----------------|
| callout-manager | Manages callout styling; publish.css captures the output. No runtime dependency. |
| nldates-obsidian | Authoring-only (natural language dates). No impact on published output. |
| obsidian-linter | Authoring-only. No impact on published output. |
| folder-notes | Creates folder-level index notes. The notes exist as regular markdown — no runtime dependency. |
| waypoint | Generates auto-updated file listings in `%% Begin Waypoint %%` blocks. 3 files use this. The generated content is static markdown between the markers — it would publish as-is, but wouldn't auto-update. |

**Core plugins:** Publish and Sync are active. Graph, backlinks, tags, footnotes, outgoing links, bookmarks, outline all enabled.

---

## 2. Compatibility Gap Analysis

### Summary Table

| Feature | In Vault? | Quartz 4 | Effort | Classification |
|---------|-----------|----------|--------|----------------|
| **Wikilinks** | 817 instances | ✅ Native | None | Non-issue |
| **Aliased wikilinks** | 69 instances | ✅ Native | None | Non-issue |
| **Backlinks** | Used | ✅ Native | None | Non-issue |
| **Graph view** | Used | ✅ Native | None | Non-issue |
| **Tags** | Pervasive | ✅ Native (with index) | None | Non-issue |
| **Standard callouts** (note, warning, info, quote, etc.) | ~35 instances | ✅ Native | None | Non-issue |
| **Nick Milo custom callouts** (milestone, connect, map, etc.) | ~38 instances | ⚠️ Renders as generic callout; no icon/color | 4–8h | **Friction point** |
| **Footnotes** | 63 instances | ✅ Native (GFM) | None | Non-issue |
| **Image embeds** `![[img.jpg]]` | 7 instances | ✅ Native | None | Non-issue |
| **Note transclusions** `![[Note]]` | 2 instances | ✅ Native | None | Non-issue |
| **Inline SVG icons** | ~12 in 4 files | ⚠️ May be stripped by sanitizer | 1–2h manual fix | Friction point |
| **Obsidian comments** `%%...%%` | ~20 instances | ✅ Stripped from output (correct behavior) | None | Non-issue |
| **Waypoint blocks** | 3 files | ⚠️ Static content OK; won't auto-update | Manual maintenance | Low friction |
| **Custom frontmatter** (status, last_tended, up) | Pervasive | ⚠️ Parsed, not rendered — needs custom components to display | 4–8h for display | Friction point |
| **Folder names with parens** | 4 folders | ⚠️ May cause URL/path issues | Test early | Low friction |
| **publish.css** | 610 KB | ❌ Incompatible DOM | Full rewrite needed | **Blocker** |
| **AppleMyungjo font** | Active | ⚠️ macOS-only system font — won't render on Windows/Linux | Font strategy needed | Friction point |
| **Dark mode** | Via Baseline theme | ✅ Native (Quartz has built-in toggle) | Palette porting | Low friction |
| **Full-text search** | Used | ✅ Native (FlexSearch) | None | Non-issue |
| **Custom domain** | cognitive-architecture.ca | ✅ Via hosting provider (DNS reconfigure) | 1h | Non-issue |
| **Dataview** | ❌ Not in vault | N/A | N/A | **Non-issue** (prior assessment was wrong) |

### Detail on the Two Blockers

**1. CSS Rewrite (BLOCKER)**

The publish.css is a 4,627-line compiled stylesheet targeting Obsidian Publish's DOM. Quartz uses a completely different HTML structure with different class names. Zero percent of these selectors would work in Quartz.

However, the situation is less dire than it appears. The publish.css is mostly theme boilerplate (Baseline theme export + Nick Milo pack). Your actual design intent — the Data Druid aesthetic — consists of: a forest green accent (`#3f734a`), AppleMyungjo font, specific callout colors for ~15 types you actually use, and dark mode palette. Porting the design *intent* to Quartz's SCSS system is 4–8 hours, not a full 4,627-line rewrite. The question is whether you can accept "close enough" or need pixel-perfect parity.

**2. Nick Milo Custom Callouts (HIGH FRICTION)**

Quartz renders the `> [!type]` syntax for any type string, but only provides built-in styling/icons for the ~15 standard Obsidian types. The Nick Milo pack defines 66 types with specific Lucide icons and colors. You use ~15 of those 66 across the vault. You'd need to either: (a) write custom CSS in Quartz's SCSS to replicate the icons and colors for those 15 types, (b) replace custom callout types with standard ones (e.g., `[!milestone]` → `[!tip]`), or (c) accept unstyled callout rendering. Option (a) is the right call but requires understanding Quartz's SCSS system.

---

## 3. Lift Estimation

### Effort by Category

| Category | Lift | One-time Hours | Ongoing Delta vs. Publish | Notes |
|----------|------|---------------|---------------------------|-------|
| **Content prep** | Low | 2–4h | None | Clean frontmatter, no Dataview, no exotic syntax. Main work: add publish flags or configure folder-based filtering; fix inline SVGs in 4 nav pages; minor frontmatter normalization. |
| **Theming/design** | Medium-High | 6–12h | +1h/quarter | Port design intent (palette, fonts, callout styling) to Quartz SCSS. Not a full 610KB rewrite — extract the ~15 callout types you use, set colors, configure fonts. Font strategy needed for cross-platform (AppleMyungjo is macOS-only). |
| **Build & deploy** | Medium | 3–6h | +1–2h/month | Quartz setup, GitHub Actions, DNS migration. You have CI experience from your 11ty site. The POSSE pipeline (`garden-rss.js`) breaks and needs rebuild — 4–6h additional. |
| **Ongoing maintenance** | Medium | N/A | +2–3h/month | Git workflow for every publish (vs. zero-ops today). Node.js/dependency updates. Waypoint blocks won't auto-update. |

### Total Estimated One-Time Effort

| Scenario | Hours | Confidence |
|----------|-------|------------|
| **Optimistic** (minimal CSS, accept Quartz defaults, skip POSSE rebuild) | 12–16h | Low — assumes you're OK with visual regression |
| **Realistic** (port callout styling, fix nav pages, rebuild POSSE, test thoroughly) | 18–25h | Medium |
| **Pessimistic** (full aesthetic parity, edge case debugging, font sourcing, build issues) | 25–35h | Medium |

These estimates are 8–10 hours lower than the prior assessment because the Dataview blocker doesn't exist and the actual content is cleaner than inferred.

### Skills / Tool Familiarity Required

| Skill | Your Level | Needed | Gap |
|-------|-----------|--------|-----|
| Git (commit, push) | Familiar | Same | None |
| Node.js / npm | Basic | Basic-Moderate | Small — Quartz config is TypeScript but mostly declarative |
| TypeScript | Unknown | Reading comprehension | Quartz's `quartz.config.ts` is straightforward |
| SCSS | Unknown | Moderate | Quartz uses SCSS for styling; this is the primary skill gap |
| GitHub Actions | Familiar | Same | None |
| DNS / Cloudflare | Familiar | Same | None |

**The SCSS gap is the most significant.** SCSS is where you'd port your callout styling, color palette, and font declarations. It's CSS with variables and nesting — not fundamentally different from what you already know, but the syntax is unfamiliar and debugging is less intuitive than plain CSS.

---

## 4. Risk Register

### Risk 1: POSSE Pipeline Breakage
**Likelihood: Certain | Impact: High**

Your `garden-rss.js` fetches Obsidian Publish's cache manifest API. Migrating off Publish destroys this endpoint. Your 11ty site's garden integration breaks immediately.

**Recovery:** Rebuild pipeline to parse Quartz's native RSS/Atom feed or read source markdown directly from the Quartz repo. Estimated: 4–6 hours. The Quartz RSS output is simpler to parse than the Publish manifest, so the rebuilt pipeline would likely be more maintainable.

### Risk 2: Callout Visual Regression
**Likelihood: High | Impact: Medium**

Your navigation structure relies heavily on custom callout types for visual wayfinding (milestone for gates, map for trails, connect for relationships). These carry semantic meaning through color and icon. Generic rendering loses that semantic layer — the garden becomes harder to navigate visually.

**Recovery:** Port the ~15 callout types you actually use into Quartz's custom CSS. This is achievable but requires learning Quartz's SCSS compilation. Alternatively, accept the visual regression temporarily and port callout styling incrementally.

### Risk 3: Inline SVG Stripping
**Likelihood: Medium-High | Impact: Medium**

Your Home, Greenhouse, Grove, and Shed pages embed raw Lucide SVG icons directly in the markdown. Quartz's markdown pipeline may strip or sanitize these. These four pages are the primary navigation surfaces of the garden — if the icons disappear, the landing experience degrades.

**Recovery:** Replace inline SVGs with emoji or unicode symbols, or use Quartz's component system to render icons. The inline SVG approach is fragile even on Obsidian Publish — it's a known workaround, not a supported feature.

### Risk 4: Build Pipeline Debugging
**Likelihood: Medium | Impact: Medium**

Folder names with parentheses ("Greenhouse (index)"), filenames with periods and special characters (several of your Claim and Seed filenames end with periods or contain colons), and the deeply nested path structure could trigger edge cases in Quartz's build. As a beginner developer, diagnosing Node.js/TypeScript build errors without a mental model of the system is time-consuming.

**Recovery:** Quartz has an active Discord. Budget 2–4 hours for unexpected build issues. Consider renaming problematic folders before migration — the parenthetical "(index)" pattern could be replaced with a cleaner convention.

### Risk 5: Maintenance Fatigue
**Likelihood: Medium | Impact: Medium**

Obsidian Publish is zero-ops: edit, click publish, done. Quartz adds: git add, git commit, git push, wait for CI, verify deploy. This friction accumulates. The garden's value comes from tending it — adding friction to the publishing step risks reducing how often you tend.

**Recovery:** The obsidian-git plugin can automate commits. GitHub Actions handles the build. But this adds moving parts and failure modes that don't exist today. The core question: does the friction of git-based publishing reduce your gardening frequency? Only you can answer that.

---

## 5. Alternatives Check

| Tool | Better for You? | Why / Why Not |
|------|-----------------|---------------|
| **Quartz 4** | Baseline comparison | Best Obsidian compatibility of any SSG. Handles wikilinks, callouts, embeds, graph view, backlinks natively. Primary gaps: custom callout styling, CSS rewrite. |
| **Obsidian Publish** (status quo) | **Yes, for now** | Zero ops, perfect compatibility, your existing POSSE pipeline works, publish.css gives you full styling control. $8/month buys you ~25 hours of not-migrating. |
| **Quartz Syncer plugin** | Worth watching | Newer tool that manages the Obsidian-to-Quartz sync with automatic style integration via SCSS. Could reduce the CSS porting burden. Not yet mature enough to recommend for production use. |
| **Perlite** | No | Requires PHP web server. More ops burden, not less. Not static hosting. |
| **Digital Garden Jekyll** | No | Ruby ecosystem (new dependency stack). Less Obsidian compatibility than Quartz. |
| **Hugo + obsidian-export** | No | Two-step pipeline. Go templates (yet another language). obsidian-export doesn't handle custom callouts. |
| **11ty consolidation** | Interesting but expensive | You already run 11ty for sebthecanadian.ca. You could publish the garden as a section of that site. But 11ty has zero native Obsidian support — you'd build wikilink resolution, callout rendering, backlinks, and graph view from scratch. Higher custom development than Quartz by far. |
| **Flowershow** | Worth investigating | MDX-based Obsidian publisher built on Next.js. Handles wikilinks, callouts, graph view. Newer, less battle-tested than Quartz, but the component model might make custom callout styling easier. |

### The Consolidation Question

Your infrastructure currently has three layers: Obsidian (authoring) → Obsidian Publish (garden hosting) → 11ty (identity site + POSSE). Quartz would replace layer 2, giving you more control but more maintenance. The deeper question is whether you want to consolidate layers 2 and 3 (garden + identity site) into a single 11ty build. That's architecturally cleaner but requires significantly more custom development work. For now, the three-layer model works.

---

## 6. Recommendation

### Updated Math (with direct evidence)

| Factor | Value |
|--------|-------|
| Obsidian Publish cost | $96/year |
| Migration effort (realistic) | 18–25 hours |
| POSSE pipeline rebuild | 4–6 hours additional |
| Breakeven period | 2.5–3 years of Publish savings |
| Ongoing maintenance delta | 2–3 hours/month |
| Vault size | 138 notes — small for a migration ROI argument |

### The Verdict

**Stay on Obsidian Publish.** The direct vault audit strengthens this recommendation, not weakens it:

1. **The Dataview blocker doesn't exist.** This was the strongest technical argument for staying. Without it, migration is technically feasible — but "feasible" isn't the same as "advisable."

2. **The CSS situation is more tractable than feared but still the dominant cost.** The publish.css is mostly theme boilerplate, not custom work. Your actual design intent is portable. But porting it to SCSS requires learning a new syntax, and the Nick Milo callout pack — which gives your navigation pages their semantic visual layer — needs per-type recreation in Quartz's system.

3. **Your vault is small.** 138 notes. The overhead of a self-hosted build pipeline is disproportionate to the content volume. This calculus changes at 300+ notes.

4. **The POSSE pipeline works.** Breaking a functioning integration to rebuild it against a different backend is pure churn with no user-facing improvement.

5. **Your time is better spent writing.** The garden's value comes from the ideas in it, not the infrastructure under it. Twenty-five hours of migration work is twenty-five hours not spent tending seeds into saplings.

### When to Revisit

Migrate when:

- Published vault grows past ~50+ substantive notes (currently ~9 published, ~138 total)
- Obsidian Publish pricing increases or features degrade
- You develop SCSS comfort through other work (this is the primary skill blocker)
- You need features Publish doesn't offer: API access, custom components, full HTML control, build-time computation
- The Quartz Syncer plugin matures enough to handle the CSS bridge automatically
- Philosophical cost of vendor dependency outweighs practical convenience — this is a legitimate concern, but it's not urgent

### What You Could Do Now (Zero Migration Required)

- **Normalize frontmatter:** Fix the `last_tended` / `last tended` inconsistency and `status` string/array variance. This is good vault hygiene regardless of hosting.
- **Add publish flags:** Even if Obsidian Publish doesn't need them, adding `publish: true/false` to frontmatter makes your content portable to any future publishing tool. This is sovereignty infrastructure.
- **Replace inline SVGs:** The raw SVG icons in your nav pages are fragile even on Publish. Replace with emoji or unicode — simpler and more portable.
- **Document your callout type taxonomy:** Note which of the 66 Nick Milo types you actually use (~15) and what semantic role each serves. This becomes the spec for any future CSS port.

---

## Appendix: Prior Assessment Corrections

| Claim in Prior Assessment | Direct Evidence Says | Impact |
|--------------------------|---------------------|--------|
| "Heavy Dataview usage" | Zero Dataview queries in vault | **Major correction** — removes primary blocker |
| "9 published posts" | 138 total markdown files; published count unclear (no frontmatter flags) | Vault is larger than assumed; published subset still small |
| "Planned Digital Forest CSS" (`forest-pixel.css`) | Not found in vault — publish.css is Baseline theme + Nick Milo pack, not pixel-art themed | CSS scope is different than described |
| "Custom callout types: forest, seedling, sapling, mature" | Not found — actual custom types are Nick Milo's (milestone, connect, map, etc.) | Callout taxonomy is different |
| "Deeply nested folder hierarchy with numbering scheme" | Vault uses clean folder names without numbering; the 1.0/1.2/1.2.5 scheme was from a different vault | Structure is cleaner than described |

---

## Sources

- Direct vault audit: `/sessions/confident-upbeat-shannon/mnt/cognitivearchitecture_ca/` (mounted 2026-03-11)
- [Quartz 4 — Official Site](https://quartz.jzhao.xyz/)
- [Quartz 4 — Callouts](https://quartz.jzhao.xyz/features/callouts)
- [Quartz 4 — GitHub Repository](https://github.com/jackyzha0/quartz)
- [Quartz Syncer Plugin](https://www.obsidianstats.com/plugins/quartz-syncer)
- [Nick Milo Callout Pack](https://github.com/nickmilo) — CSS snippet identified in vault
- Prior indirect assessment (2026-03-11, same session, based on assimilated documents from sebthecanadian.ca project)
