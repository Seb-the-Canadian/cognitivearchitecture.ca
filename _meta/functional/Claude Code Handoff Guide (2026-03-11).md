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

# Claude Code Handoff Guide — Garden Migration

> **Project:** Garden Migration: Obsidian Publish → 11ty
> **Linear Project ID:** a116e7bc-43ad-44c2-b05a-ac8c69b31e24
> **Created:** 2026-03-11
> **Vault path:** `cognitivearchitecture_ca/`

---

## Purpose

This document maps the cross-context coordination between **Cowork** (design review, planning, vault-level decisions) and **Claude Code** (implementation, debugging, build pipeline) for the garden migration project. Each Linear issue contains a copy-pastable Claude Code prompt. This guide explains *when* and *how* to use them.

---

## Context Model

| Context | Tool | Best For |
|---------|------|----------|
| **Cowork** | Claude Desktop (Cowork mode) | Design review, visual QA, planning, vault governance decisions, document creation |
| **Claude Code** | Terminal (`claude` CLI) | Writing code, running builds, installing packages, debugging errors, file manipulation |

**Rule of thumb:** If it touches `eleventy.config.js`, `package.json`, CSS, JS, or Nunjucks templates — Claude Code. If it's about *what should it look like* or *should we publish this* — Cowork.

---

## Linear Issue Map

### Stage 1: Migrate & Stabilize

| Issue | Phase | Points | Context | Dependency |
|-------|-------|--------|---------|------------|
| COG-272 | 1A: Content Prep | 5 | Claude Code | — |
| COG-273 | 1B: 11ty Scaffolding | 5 | Claude Code | COG-272 |
| COG-274 | 1C: Wikilinks & Backlinks | 5 | Claude Code | COG-273 |
| COG-275 | 1D: Callout Rendering | 5 | Claude Code | COG-274 |
| COG-276 | 1E: Layout & Navigation | 8 | Claude Code + Cowork | COG-275 |
| COG-277 | 1F: Design Porting | 5 | Claude Code | COG-276 |
| COG-278 | 1G: Assets & Deployment | 3 | Claude Code + Manual | COG-277 |
| COG-279 | 1H: POSSE Pipeline & QA | 5 | Claude Code | COG-278 |

**Stage 1 total:** 41 points (~35–50 hours with AI pairing)

### Stage 2: Enhancement Pipeline

| Issue | Enhancement | Points | Context | Dependency |
|-------|-------------|--------|---------|------------|
| COG-281 | 2A: Pagefind Search | 3 | Claude Code | Stage 1 |
| COG-282 | 2B: Type-Driven Templates | 5 | Claude Code + Cowork | Stage 1 |
| COG-283 | 2C: Graph View (D3.js) | 8 | Claude Code | Stage 1 |
| COG-284 | 2D: Hover Previews | 3 | Claude Code | Stage 1 |
| COG-285 | 2E: OG Images | 3 | Claude Code | Stage 1 |
| COG-286 | 2F: Full Data Druid Aesthetic | 8 | Cowork + Claude Code | Stage 1, ideally 2B |

**Stage 2 total:** 30 points (~24–39 hours, independent workstreams)

---

## How to Use the Claude Code Prompts

Each Linear issue contains a fenced code block labeled **"Claude Code Handoff Prompt."** To use it:

### Starting a Phase

1. Open the Linear issue for the phase you're starting
2. Copy the Claude Code handoff prompt from the issue description
3. In your terminal, navigate to the vault root:
   ```bash
   cd ~/path/to/cognitivearchitecture_ca
   ```
4. Start Claude Code:
   ```bash
   claude
   ```
5. Paste the handoff prompt as your first message
6. Claude Code will have access to the CLAUDE.md governance file and the full vault

### During a Phase

- Claude Code will work through the tasks in the prompt
- For phases that suggest **sub-agent delegation**, Claude Code will spawn parallel workers for independent tasks
- If Claude Code needs a design decision (especially in 1E, 1F, 2B, 2F), it will ask — you can also bring the question to Cowork for a more considered review
- Run `npx eleventy --serve` frequently to verify changes visually

### Completing a Phase

1. Run the verification steps listed at the bottom of each handoff prompt
2. If all checks pass, commit:
   ```bash
   git add -A && git commit -m "Phase 1X: [description]"
   ```
3. Update the Linear issue status to Done
4. Move to the next phase

### If Something Breaks

- The handoff prompt gives Claude Code enough context to debug within the phase
- If a bug traces back to a *previous* phase, reference that phase's issue number for context
- For persistent build errors, the most common causes are: special characters in filenames (parentheses, colons), case-sensitivity mismatches in wikilink targets, and missing npm packages

---

## Step 0 Prompt — Full Project Orientation

Use this prompt to orient a **new Claude Code session** that has no prior context about the project. Paste this as the first message in any fresh session:

```
## Project: Garden Migration — cognitive-architecture.ca

You are working on migrating a digital garden from Obsidian Publish to a self-hosted 11ty static site.

### Architecture
- The vault root IS the 11ty project root (no symlinks, no submodules)
- Content: 138 markdown files with YAML frontmatter (status, type, tags, created, last_tended, up)
- Templates/CSS/JS: `_build/` directory
- Build output: `_site/`
- Hosting: Cloudflare Pages (auto-builds on push to main)

### Directory structure
```
cognitivearchitecture_ca/
├── eleventy.config.js
├── package.json
├── _build/
│   ├── layouts/    (base.njk, note.njk, gate.njk, archive.njk, claim.njk, etc.)
│   ├── includes/   (backlinks.njk, breadcrumbs.njk, local-graph.njk)
│   ├── css/        (main.css, callouts.css)
│   ├── js/         (dark-mode.js, hover-preview.js)
│   └── data/       (global data files)
├── _site/          (build output, gitignored)
├── .obsidian/      (excluded from build)
├── _meta/          (excluded from build)
├── Atlas/          (content)
├── Home.md         (content)
└── ...
```

### Key packages
- @11ty/eleventy (SSG)
- @photogabble/eleventy-plugin-interlinker (wikilinks + backlinks)
- markdown-it-obsidian-callouts (callout rendering)
- @11ty/eleventy-plugin-rss (RSS feed)
- pagefind (search, Stage 2)
- d3 (graph view, Stage 2)
- @floating-ui/dom (hover previews, Stage 2)

### Design system
- Accent color: #3f734a (forest green)
- Font: EB Garamond (serif, Google Fonts)
- Dark mode: CSS custom properties + localStorage toggle
- Status badges: seed (🌱 yellow), sprout (light green), sapling (green), evergreen (deep green)

### Governance
- Read CLAUDE.md in the vault root — it defines boundaries
- Human writes content; AI tends infrastructure
- Do not modify note content (definitions, arguments, connections)
- You CAN modify: templates, CSS, JS, config files, build scripts, metadata

### Current phase
Check Linear for the current active issue. The project tracks as:
- Linear project: "Garden Migration: Obsidian Publish → 11ty"
- Issues: COG-272 through COG-286
- Each issue has a detailed handoff prompt — read the active issue for your specific task

### What phase am I on?
Look at the git log and the state of the project:
- If no eleventy.config.js exists → Phase 1A or 1B
- If eleventy.config.js exists but no layouts → Phase 1B
- If layouts exist but wikilinks don't resolve → Phase 1C
- If wikilinks work but callouts are unstyled → Phase 1D
- If callouts work but layout is bare → Phase 1E
- If layout exists but no Data Druid styling → Phase 1F
- If styled but no deployment config → Phase 1G
- If deployable but no RSS/POSSE → Phase 1H
- If all Stage 1 complete → Stage 2 (check Linear for active enhancement)
```

---

## Sub-Agent Delegation Patterns

Several phases recommend sub-agent delegation within Claude Code. Here's the pattern:

### When to delegate
- Phase has 3+ independent tasks that don't share state
- Tasks are substantial enough to benefit from parallel execution
- Examples: 1E (layout + CSS + pagination), 1H (RSS + POSSE + link checker), 2C (graph data + local graph + interaction)

### How Claude Code delegates
Claude Code uses its built-in agent spawning to run parallel workers. The handoff prompts specify suggested agent splits. Claude Code will:
1. Read the delegation plan from the prompt
2. Spawn agents for independent workstreams
3. Coordinate results back into the main branch
4. Run verification after all agents complete

### When NOT to delegate
- Phase 1A (content prep) — sequential, each fix informs the next
- Phase 1F (design porting) — coherent aesthetic requires single-thread attention
- Phase 1G (deployment) — mostly config + manual steps

---

## Cross-Context Handoff Points

These are moments where work should move between Cowork and Claude Code:

### Cowork → Claude Code
1. **Phase start**: Copy the handoff prompt from Linear, paste into Claude Code
2. **Design decision made**: After reviewing options in Cowork, communicate the decision to Claude Code (e.g., "use EB Garamond, not Crimson Text")
3. **Content prep complete**: After Phase 1A vault cleanup in Obsidian, signal Claude Code to begin 1B

### Claude Code → Cowork
1. **Design review needed**: Claude Code builds the layout/templates, then bring screenshots to Cowork for review: "Does this match the Data Druid feel?"
2. **Visual QA**: After Phase 1F, do a full visual walkthrough in Cowork comparing against Obsidian Publish
3. **Launch readiness**: After Phase 1H, bring the launch checklist results to Cowork for final approval
4. **Vault governance questions**: If Claude Code encounters a question about content (should this note be published? should these be linked?), escalate to Cowork

---

## Monitoring Progress

### In Linear
- All issues are in the "Garden Migration: Obsidian Publish → 11ty" project
- Two milestones track Stage 1 and Stage 2
- Dependency chain: COG-272 → 273 → 274 → 275 → 276 → 277 → 278 → 279
- Stage 2 issues (COG-281–286) are independent of each other, all blocked by Stage 1

### In Git
- Each phase should produce 1-3 commits
- Commit message format: `Phase 1X: [description]` or `Phase 2X: [description]`
- Tag `v1.0` after Stage 1 launch checklist passes

### Build health
- After each phase, `npx eleventy` should succeed with 0 errors
- After Phase 1G, Cloudflare Pages builds on push
- After Phase 1H, RSS validates and POSSE pipeline produces correct output

---

## Timeline Reference

Assuming ~8–10h/week of focused work:

| Week | Phases | Milestone |
|------|--------|-----------|
| 1–2 | 1A + 1B | First successful build |
| 2–3 | 1C + 1D | Links resolve, callouts render |
| 3–4 | 1E + 1F | Site looks like a site |
| 4–5 | 1G + 1H | Deployed, POSSE working |
| 5 | DNS cutover | **Site live** (keep Publish as fallback 1 week) |
| 6+ | Stage 2 | Enhancements in any order |

---

## Reference Documents

| Document | Location |
|----------|----------|
| Migration Assessment | `_meta/functional/Migration Assessment - Obsidian Publish to Quartz 4 (2026-03-11).md` |
| Project Plan | `_meta/functional/11ty Migration Project Plan (2026-03-11).md` |
| This Handoff Guide | `_meta/functional/Claude Code Handoff Guide (2026-03-11).md` |
| Vault Governance | `CLAUDE.md` |
| Tag Taxonomy | `_meta/Tag Taxonomy.md` |
