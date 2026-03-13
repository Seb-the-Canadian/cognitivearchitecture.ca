---
created: 2026-02-16
last_tended: 2026-02-16
type: project
tags:
  - stub
up:
  - "[[cognitivearchitecture_ca]]"
---

# Almanac Monthly — Reference

---

## Workflow

### Throughout the Month

Tend notes. The linter stamps `last tended`. When something feels newsletter-worthy, add it to [[next]] with a one-line annotation.

### Almanac Day

1. Open [[next]] — your composition plan is there
2. Triage: search `[almanac-status:candidate]` to catch anything tagged but not listed, or sort file explorer by modification date to jog memory
3. Compose in [Buttondown](https://buttondown.com/emails/new) using the skeleton below
4. Send

### Post-Send

- [ ] Update this file: `last-issue-sent`, `last-issue-number`, `next-issue-number`
- [ ] Archive sent markdown to `_meta/almanac/almanac-{NNN}.md`
- [ ] Set `almanac-status: featured` and `almanac-issue: {N}` on featured notes
- [ ] Review remaining candidates in [[next]]: move to next issue or remove
- [ ] Clear [[next]] for next cycle (increment `issue` in its frontmatter)

---

## Email Skeleton

Subject: `Almanac Monthly #{N} — {thematic hook}`

```markdown
{Opening: 2-4 sentences. Personal, tonal. What season the garden is in.}

---

## New Plantings

- **[Note Title](url)** — {annotation}
- **[Note Title](url)** — {annotation}

## Recently Tended

- **[Note Title](url)** — {what changed and why}

## From the Grove

{Only when something has reached maturity. Full paragraph. Omit if nothing qualifies.}

## Field Notes

- {Fragment. A seed not yet planted.}
- {Fragment.}

---

{Closing: One sentence. Clean exit. No calls to action.}
```

### Link Format

```
https://cognitive-architecture.ca/{Note+Name}
https://cognitive-architecture.ca/Atlas/Seeds/{Note+Name}
```

Spaces become `+`. Verify against live site.

---

## Frontmatter Properties

Set on notes after featuring:

```yaml
almanac-status: candidate | featured | skip
almanac-issue: 1
almanac-note: "Why it matters now"
```

### Lifecycle

```
absent → candidate → featured
            ↑   ╲        │
            │    → skip   │ (major revision)
            └─────────────┘
```

---

## How It Works

The **linter** maintains `created` and `last tended` on every note automatically. This is the discovery mechanism — every note you touch gets stamped.

The **running list** (`next.md`) captures curation: which notes matter for this issue and why. You add to it while tending.

The **frontmatter properties** are the archival layer: after sending, mark what appeared where so you don't repeat and can track coverage.

No Bases. No Dataview. No plugins beyond what's already installed.

---

## One-Time Setup

- [ ] Run linter across all seed packets to standardize `created` field (linter adds it from filesystem date where missing)

---

## Changelog

### Pipeline v3.0 — 2026-02-05
- Simplified to running list + linter + core search
- Removed Bases dependency (pipeline.base)
- Removed Dataview dependency (v1.0)
- Discovery via linter-maintained `last tended`, not database queries

### Pipeline v2.0 — 2026-02-05
- Bases rebuild (superseded)

### Pipeline v1.0 — 2026-02-05
- Dataview build (superseded)
