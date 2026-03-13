---
created: 2026-03-13
last_tended: 2026-03-13
type: effort
tags:
  - migration
  - infrastructure
up:
  - "[[cognitivearchitecture_ca]]"
---

# URL Structure Reference

Generated: 2026-03-13
Scope: Publishable files only. Excludes: `_meta/`, `Atlas/Seeds/`, `.obsidian/`, `_build/`, `node_modules/`, `CLAUDE.md`, `README.md`, `cognitivearchitecture_ca.md`

---

## Slug Rules

The following rules are applied in order when converting a filename to a URL slug:

### Rule 1 — Strip trailing periods from filenames
Many filenames end with a period (common in claim-style note titles). The trailing period is removed before any other transformation.

Examples:
- `Digital gardening is more sustainable than fast production..md` → `digital-gardening-is-more-sustainable-than-fast-production`
- `Capital cognitive capture is more novel threat than traditional automation..md` → `capital-cognitive-capture-is-more-novel-threat-than-traditional-automation`
- `in the absence of clarity, LLMs create complexity..md` → `in-the-absence-of-clarity-llms-create-complexity`

### Rule 2 — Lowercase everything
All characters are lowercased.

Examples:
- `Cognitive Architecture.md` → `cognitive-architecture`
- `The Cognitive Conservatory.md` → `the-cognitive-conservatory`

### Rule 3 — Spaces → hyphens
All spaces become hyphens.

Examples:
- `Data Fluency.md` → `data-fluency`
- `About me.md` → `about-me`

### Rule 4 — Ampersand → `and`
`&` is replaced with `and`.

Examples:
- `Atlas/Cognitive Architecture & Knowledge Work.md` → `/atlas/cognitive-architecture-and-knowledge-work/`
- `Atlas/Cultural & Philosophical Grounding.md` → `/atlas/cultural-and-philosophical-grounding/`

### Rule 5 — Semicolons → hyphens
Semicolons in filenames are converted to hyphens (after applying the semicolon as a separator within the slug).

Examples:
- `Data fluency is developmental, not binary; it cannot be mandated..md` → `data-fluency-is-developmental-not-binary-it-cannot-be-mandated`
- `Systems are not neutral; every technical choice shapes what can be expressed..md` → `systems-are-not-neutral-every-technical-choice-shapes-what-can-be-expressed`

### Rule 6 — Em-dashes and en-dashes → hyphens
Em-dashes (—) and en-dashes (–) are replaced with hyphens.

Examples:
- `Partnership Compact — Core Values for AI Collaboration.md` → `partnership-compact-core-values-for-ai-collaboration`

### Rule 7 — Apostrophes → stripped
Apostrophes (straight `'` and curly `'`) are removed.

Examples:
- `Default Decisions - LinkedIn's 2025 AI Policy Update.md` → `default-decisions-linkedins-2025-ai-policy-update`
- `Marginalized populations' experiences offer a crucial lens (on technology adoption)..md` → `marginalized-populations-experiences-offer-a-crucial-lens-on-technology-adoption`

### Rule 8 — Quotation marks → stripped
Straight and curly double quotes (`"`, `"`, `"`) are removed.

Examples:
- `In AI mediated work, employability becomes "legibility to the system plus proprietary context access".md` → `in-ai-mediated-work-employability-becomes-legibility-to-the-system-plus-proprietary-context-access`
- `What does it mean to speak truth to power; and how can critique become a form of healing, renewal, and "rehumanization"?.md` → `what-does-it-mean-to-speak-truth-to-power-and-how-can-critique-become-a-form-of-healing-renewal-and-rehumanization`

### Rule 9 — Question marks → stripped
Trailing question marks (common in question-index filenames) are removed.

Examples:
- `What becomes scarce when AI can copy at scale?.md` → `what-becomes-scarce-when-ai-can-copy-at-scale`
- `How do we build civic social digital infrastructure alternatives?.md` → `how-do-we-build-civic-social-digital-infrastructure-alternatives`

### Rule 10 — Commas → stripped
Commas are removed. See Ambiguous Cases for discussion of whether to preserve or strip.

Examples:
- `How do imagined societies, crises, and futures reveal hidden truths...?.md` → `how-do-imagined-societies-crises-and-futures-reveal-hidden-truths...`
- `Technology should amplify human capacity for wisdom, connection, and flourishing..md` → `technology-should-amplify-human-capacity-for-wisdom-connection-and-flourishing`

### Rule 11 — Double spaces → single hyphen
Consecutive spaces are collapsed before space-to-hyphen conversion.

Examples:
- `The most powerful questions in (digital) transformation  are "should we" and "why", not "can we"..md` → `the-most-powerful-questions-in-digital-transformation-are-should-we-and-why-not-can-we` (double space between `transformation` and `are` collapsed)

### Rule 12 — Collapse multiple hyphens
After all substitutions, consecutive hyphens (`--`, `---`) are collapsed to a single hyphen.

### Rule 13 — Directory path mapping (parenthetical suffixes stripped)
Directory names with parenthetical suffixes are mapped as follows:

| Directory | URL prefix |
|-----------|------------|
| `Atlas/The Almanac/Concepts/` | `/concepts/` |
| `Atlas/The Almanac/Claims/` | `/claims/` |
| `Atlas/The Almanac/Questions (index)/` | `/questions/` |
| `Atlas/The Almanac/Greenhouse (index)/` | `/greenhouse/` |
| `Atlas/The Almanac/The Grove (index)/` | `/the-grove/` |
| `Atlas/The Almanac/The Shed (index)/` | `/the-shed/` |
| `Atlas/The Almanac/` (direct children) | `/` |
| `Atlas/` (thematic maps) | `/atlas/` |
| Root files | `/` |

---

## Ambiguous Cases Requiring Human Decision

### A1 — Parentheses within filenames

Several filenames contain parenthetical qualifiers. Two options exist:

**Option A — Preserve parentheses in slug:**
- `Human wisdom cannot be replaced by (Artificial) intelligence..md` → `/claims/human-wisdom-cannot-be-replaced-by-(artificial)-intelligence/`
- `Marginalized populations' experiences offer a crucial lens (on technology adoption)..md` → `/claims/marginalized-populations-experiences-offer-a-crucial-lens-(on-technology-adoption)/`
- `The most powerful questions in (digital) transformation...` → `/claims/the-most-powerful-questions-in-(digital)-transformation-are.../`
- `Digital Gardens of the interwebs (a very narrow cross-section)..md` → `/digital-gardens-of-the-interwebs-(a-very-narrow-cross-section)/`

**Option B — Strip parentheses and their contents from slug:**
- `Human wisdom cannot be replaced by (Artificial) intelligence..md` → `/claims/human-wisdom-cannot-be-replaced-by-artificial-intelligence/`
- `Marginalized populations' experiences offer a crucial lens (on technology adoption)..md` → `/claims/marginalized-populations-experiences-offer-a-crucial-lens/`
- `The most powerful questions in (digital) transformation...` → `/claims/the-most-powerful-questions-in-transformation-are.../`
- `Digital Gardens of the interwebs (a very narrow cross-section)..md` → `/digital-gardens-of-the-interwebs/`

**Option C — Strip parentheses but keep contents:**
- `Human wisdom cannot be replaced by (Artificial) intelligence..md` → `/claims/human-wisdom-cannot-be-replaced-by-artificial-intelligence/`
- `Marginalized populations' experiences offer a crucial lens (on technology adoption)..md` → `/claims/marginalized-populations-experiences-offer-a-crucial-lens-on-technology-adoption/`

**Recommendation:** Option C is the cleanest for URL semantics — parenthetical content is meaningful but parentheses themselves are not valid in URLs without encoding. The table below uses Option C.

Files affected:
- `Atlas/The Almanac/Claims/Human wisdom cannot be replaced by (Artificial) intelligence..md`
- `Atlas/The Almanac/Claims/Marginalized populations' experiences offer a crucial lens (on technology adoption)..md`
- `Atlas/The Almanac/Claims/The most powerful questions in (digital) transformation  are "should we" and "why", not "can we"..md`
- `Atlas/The Almanac/Digital Gardens of the interwebs (a very narrow cross-section)..md`

**Decision needed:** Which option to apply? This affects 4 files.

---

### A2 — Commas in filenames

Many question and claim filenames include commas for readability. The proposed rule strips them (producing cleaner slugs). No URL-encoding issue, but worth confirming.

**Option A — Strip commas:**
- `How do imagined societies, crises, and futures reveal hidden truths about power, freedom, and moral responsibility in our own world?.md` → `how-do-imagined-societies-crises-and-futures-reveal-hidden-truths-about-power-freedom-and-moral-responsibility-in-our-own-world`

**Option B — Replace commas with hyphens:**
- → `how-do-imagined-societies-crises-and-futures-reveal-hidden-truths-about-power-freedom-and-moral-responsibility-in-our-own-world` (same result, as comma+space → hyphen after space-replacement)

In practice, both options produce identical results since commas in these filenames are always followed by a space. Stripping is cleaner.

**Decision needed:** Confirm stripping commas is acceptable. Affects approximately 12 files.

---

### A3 — Apostrophes in possessives

Stripping apostrophes changes `LinkedIn's` to `linkedins`. This is standard web practice but worth flagging.

Examples:
- `Default Decisions - LinkedIn's 2025 AI Policy Update.md` → `/greenhouse/default-decisions-linkedins-2025-ai-policy-update/`
- `Marginalized populations' experiences...` → `marginalized-populations-experiences...`

**Decision needed:** Confirm stripping apostrophes is acceptable. Two files affected.

---

### A4 — Very long URLs (question filenames)

Several question filenames produce extremely long URLs. This is SEO-suboptimal but preserves the full meaning. Consider whether shorter aliases are desirable.

Examples of long slugs:
- `/questions/what-broader-historical-and-structural-narratives-help-situate-political-philosophy-within-the-evolution-of-civilization-governance-and-design/` (148 chars)
- `/questions/how-do-imagined-societies-crises-and-futures-reveal-hidden-truths-about-power-freedom-and-moral-responsibility-in-our-own-world/` (134 chars)
- `/questions/how-do-individuals-form-moral-judgement-and-identity-within-and-sometimes-against-social-and-historical-structures/` (119 chars)

**Decision needed:** Accept long question URLs, or define a maximum length with truncation rules?

---

### A5 — Root gate pages vs. section index pages

The site has two layers:
1. Root gate pages (`The Greenhouse.md`, `The Grove.md`, `The Shed.md`) → proposed as `/the-greenhouse/`, `/the-grove/`, `/the-shed/`
2. Section index content lives in `Atlas/The Almanac/The Shed (index)/`, `Atlas/The Almanac/The Grove (index)/`, etc. → also proposed as `/the-shed/[slug]`, `/the-grove/[slug]`

The root gate pages and section index content share the same URL namespace. This is intentional if the root gate page IS the index (e.g., `The Shed.md` renders at `/the-shed/` and the shed articles live under `/the-shed/[slug]`). Confirm this is the intended architecture.

---

### A6 — `Digital Gardens of the interwebs (a very narrow cross-section)..md`

This file sits directly in `Atlas/The Almanac/` (not in a subdirectory). Per the mapping rules, direct children of `Atlas/The Almanac/` get a `/` prefix (top-level). This means the URL would be:

`/digital-gardens-of-the-interwebs-a-very-narrow-cross-section/`

Confirm this top-level placement is correct, or assign it to a section (e.g., `/the-grove/`).

---

## Complete URL Mapping

The table below uses Option C for parentheses (strip parens, keep contents), commas stripped, apostrophes stripped, quotation marks stripped.

| Source Path | Proposed URL | Notes |
|------------|--------------|-------|
| `Home.md` | `/` | |
| `About me.md` | `/about-me/` | |
| `About the site.md` | `/about-the-site/` | |
| `Havelian Tenants.md` | `/havelian-tenants/` | |
| `Illichian Design Ethics.md` | `/illichian-design-ethics/` | |
| `The Greenhouse.md` | `/the-greenhouse/` | Root gate page |
| `The Grove.md` | `/the-grove/` | Root gate page |
| `The Shed.md` | `/the-shed/` | Root gate page |
| `Atlas/Capability Development.md` | `/atlas/capability-development/` | Thematic map |
| `Atlas/Cognitive Architecture & Knowledge Work.md` | `/atlas/cognitive-architecture-and-knowledge-work/` | Thematic map; `&` → `and` |
| `Atlas/Core Claims & Positions.md` | `/atlas/core-claims-and-positions/` | Thematic map; `&` → `and` |
| `Atlas/Cultural & Philosophical Grounding.md` | `/atlas/cultural-and-philosophical-grounding/` | Thematic map; `&` → `and` |
| `Atlas/Digital Sovereignty & Infrastructure.md` | `/atlas/digital-sovereignty-and-infrastructure/` | Thematic map; `&` → `and` |
| `Atlas/Governance & Power Dynamics.md` | `/atlas/governance-and-power-dynamics/` | Thematic map; `&` → `and` |
| `Atlas/Human Judgement & Wisdom.md` | `/atlas/human-judgement-and-wisdom/` | Thematic map; `&` → `and` |
| `Atlas/Organizational Knowledge Systems.md` | `/atlas/organizational-knowledge-systems/` | Thematic map |
| `Atlas/Questions & Queries.md` | `/atlas/questions-and-queries/` | Thematic map; `&` → `and` |
| `Atlas/Technology Adoption & Change.md` | `/atlas/technology-adoption-and-change/` | Thematic map; `&` → `and` |
| `Atlas/The Almanac/Digital Gardens of the interwebs (a very narrow cross-section)..md` | `/digital-gardens-of-the-interwebs-a-very-narrow-cross-section/` | Top-level; trailing period stripped; parens stripped (see A1, A6) |
| `Atlas/The Almanac/Concepts/AI.md` | `/concepts/ai/` | |
| `Atlas/The Almanac/Concepts/Cognitive Architecture.md` | `/concepts/cognitive-architecture/` | |
| `Atlas/The Almanac/Concepts/Concepts.md` | `/concepts/concepts/` | |
| `Atlas/The Almanac/Concepts/Conservatory Roles.md` | `/concepts/conservatory-roles/` | |
| `Atlas/The Almanac/Concepts/Data Fluency.md` | `/concepts/data-fluency/` | |
| `Atlas/The Almanac/Concepts/Default Decisions - Architecture Shapes Behaviour.md` | `/concepts/default-decisions-architecture-shapes-behaviour/` | Hyphen in filename treated as literal |
| `Atlas/The Almanac/Concepts/Digital Sovereignty.md` | `/concepts/digital-sovereignty/` | |
| `Atlas/The Almanac/Concepts/Dual-mode Knowledge Fluency.md` | `/concepts/dual-mode-knowledge-fluency/` | |
| `Atlas/The Almanac/Concepts/Hesitation as Data.md` | `/concepts/hesitation-as-data/` | |
| `Atlas/The Almanac/Concepts/Intelligence vs. wisdom.md` | `/concepts/intelligence-vs-wisdom/` | Period in `vs.` stripped |
| `Atlas/The Almanac/Concepts/Philosophy of Enablement.md` | `/concepts/philosophy-of-enablement/` | |
| `Atlas/The Almanac/Concepts/Socratic Prototyping.md` | `/concepts/socratic-prototyping/` | |
| `Atlas/The Almanac/Concepts/The Cognitive Conservatory.md` | `/concepts/the-cognitive-conservatory/` | |
| `Atlas/The Almanac/Concepts/Tool Congruence.md` | `/concepts/tool-congruence/` | |
| `Atlas/The Almanac/Concepts/capital cognitive capture.md` | `/concepts/capital-cognitive-capture/` | |
| `Atlas/The Almanac/Concepts/digital garden.md` | `/concepts/digital-garden/` | |
| `Atlas/The Almanac/Concepts/in the absence of clarity, LLMs create complexity..md` | `/concepts/in-the-absence-of-clarity-llms-create-complexity/` | Trailing period stripped; comma stripped |
| `Atlas/The Almanac/Concepts/social infrastructure.md` | `/concepts/social-infrastructure/` | |
| `Atlas/The Almanac/Claims/Capital cognitive capture is more novel threat than traditional automation..md` | `/claims/capital-cognitive-capture-is-more-novel-threat-than-traditional-automation/` | Trailing period stripped |
| `Atlas/The Almanac/Claims/Data fluency is developmental, not binary; it cannot be mandated..md` | `/claims/data-fluency-is-developmental-not-binary-it-cannot-be-mandated/` | Trailing period stripped; comma stripped; semicolon → hyphen |
| `Atlas/The Almanac/Claims/Default decisions shape platform behaviour; most users never change defaults..md` | `/claims/default-decisions-shape-platform-behaviour-most-users-never-change-defaults/` | Trailing period stripped; semicolon → hyphen |
| `Atlas/The Almanac/Claims/Digital gardening is more sustainable than fast production..md` | `/claims/digital-gardening-is-more-sustainable-than-fast-production/` | Trailing period stripped |
| `Atlas/The Almanac/Claims/Hesitation is often valuable signal, not resistance to overcome..md` | `/claims/hesitation-is-often-valuable-signal-not-resistance-to-overcome/` | Trailing period stripped; comma stripped |
| `Atlas/The Almanac/Claims/Human wisdom cannot be replaced by (Artificial) intelligence..md` | `/claims/human-wisdom-cannot-be-replaced-by-artificial-intelligence/` | Trailing period stripped; parens stripped (see A1) |
| `Atlas/The Almanac/Claims/In AI mediated work, employability becomes "legibility to the system plus proprietary context access".md` | `/claims/in-ai-mediated-work-employability-becomes-legibility-to-the-system-plus-proprietary-context-access/` | Comma stripped; quotation marks stripped |
| `Atlas/The Almanac/Claims/Knowledge fragmentation is solved by semantic bridges, not just tool consolidation or acquisition..md` | `/claims/knowledge-fragmentation-is-solved-by-semantic-bridges-not-just-tool-consolidation-or-acquisition/` | Trailing period stripped; comma stripped |
| `Atlas/The Almanac/Claims/Knowledge is personal and political; there is no objective enablement..md` | `/claims/knowledge-is-personal-and-political-there-is-no-objective-enablement/` | Trailing period stripped; semicolon → hyphen |
| `Atlas/The Almanac/Claims/Marginalized populations' experiences offer a crucial lens (on technology adoption)..md` | `/claims/marginalized-populations-experiences-offer-a-crucial-lens-on-technology-adoption/` | Trailing period stripped; apostrophe stripped; parens stripped (see A1) |
| `Atlas/The Almanac/Claims/Metadata enables discovery; natural language enables understanding; both required..md` | `/claims/metadata-enables-discovery-natural-language-enables-understanding-both-required/` | Trailing period stripped; semicolons → hyphens |
| `Atlas/The Almanac/Claims/Organizations fail when they build technical capability before semantic clarity..md` | `/claims/organizations-fail-when-they-build-technical-capability-before-semantic-clarity/` | Trailing period stripped |
| `Atlas/The Almanac/Claims/Social opinion operates as enforcement mechanism of digital conformity..md` | `/claims/social-opinion-operates-as-enforcement-mechanism-of-digital-conformity/` | Trailing period stripped |
| `Atlas/The Almanac/Claims/Systems are not neutral; every technical choice shapes what can be expressed..md` | `/claims/systems-are-not-neutral-every-technical-choice-shapes-what-can-be-expressed/` | Trailing period stripped; semicolon → hyphen |
| `Atlas/The Almanac/Claims/Technology should amplify human capacity for wisdom, connection, and flourishing..md` | `/claims/technology-should-amplify-human-capacity-for-wisdom-connection-and-flourishing/` | Trailing period stripped; commas stripped |
| `Atlas/The Almanac/Claims/The most powerful questions in (digital) transformation  are "should we" and "why", not "can we"..md` | `/claims/the-most-powerful-questions-in-digital-transformation-are-should-we-and-why-not-can-we/` | Trailing period stripped; parens stripped; double space collapsed; quotation marks stripped; commas stripped (see A1) |
| `Atlas/The Almanac/Greenhouse (index)/Beyond the binary - data fluency over data literacy..md` | `/greenhouse/beyond-the-binary-data-fluency-over-data-literacy/` | Trailing period stripped |
| `Atlas/The Almanac/Greenhouse (index)/Default Decisions - LinkedIn's 2025 AI Policy Update.md` | `/greenhouse/default-decisions-linkedins-2025-ai-policy-update/` | Apostrophe stripped (see A3) |
| `Atlas/The Almanac/Greenhouse (index)/When Hesitation is Data - Rethinking AI Adoption Competency.md` | `/greenhouse/when-hesitation-is-data-rethinking-ai-adoption-competency/` | |
| `Atlas/The Almanac/Questions (index)/How can individuals or small orgs protect IP from cognitive capture?.md` | `/questions/how-can-individuals-or-small-orgs-protect-ip-from-cognitive-capture/` | Question mark stripped |
| `Atlas/The Almanac/Questions (index)/How can metadata and human-readable documentation work together?.md` | `/questions/how-can-metadata-and-human-readable-documentation-work-together/` | Question mark stripped |
| `Atlas/The Almanac/Questions (index)/How do imagined societies, crises, and futures reveal hidden truths about power, freedom, and moral responsibility in our own world?.md` | `/questions/how-do-imagined-societies-crises-and-futures-reveal-hidden-truths-about-power-freedom-and-moral-responsibility-in-our-own-world/` | Long URL (see A4); commas stripped; question mark stripped |
| `Atlas/The Almanac/Questions (index)/How do individuals form moral judgement, and identity, within and sometimes against, social and historical structures?.md` | `/questions/how-do-individuals-form-moral-judgement-and-identity-within-and-sometimes-against-social-and-historical-structures/` | Long URL (see A4); commas stripped; question mark stripped |
| `Atlas/The Almanac/Questions (index)/How do modern systems of capital, technology, and ideology capture power; and how might they be resisted, redirected, or reimagined?.md` | `/questions/how-do-modern-systems-of-capital-technology-and-ideology-capture-power-and-how-might-they-be-resisted-redirected-or-reimagined/` | Long URL (see A4); commas stripped; semicolon → hyphen; question mark stripped |
| `Atlas/The Almanac/Questions (index)/How do we build civic social digital infrastructure alternatives?.md` | `/questions/how-do-we-build-civic-social-digital-infrastructure-alternatives/` | Question mark stripped |
| `Atlas/The Almanac/Questions (index)/How do we design systems that amplify human wisdom rather than replace it?.md` | `/questions/how-do-we-design-systems-that-amplify-human-wisdom-rather-than-replace-it/` | Question mark stripped |
| `Atlas/The Almanac/Questions (index)/How do we distinguish valuable hesitation from fear based resistance?.md` | `/questions/how-do-we-distinguish-valuable-hesitation-from-fear-based-resistance/` | Question mark stripped |
| `Atlas/The Almanac/Questions (index)/How do we move organizations from extractive to stewardship models?.md` | `/questions/how-do-we-move-organizations-from-extractive-to-stewardship-models/` | Question mark stripped |
| `Atlas/The Almanac/Questions (index)/How do we structure work to preserve wisdom while leveraging intelligence?.md` | `/questions/how-do-we-structure-work-to-preserve-wisdom-while-leveraging-intelligence/` | Question mark stripped |
| `Atlas/The Almanac/Questions (index)/How does architecture encode values and what alternative architectures exist?.md` | `/questions/how-does-architecture-encode-values-and-what-alternative-architectures-exist/` | Question mark stripped |
| `Atlas/The Almanac/Questions (index)/How to design systems that amplify rather than replace?.md` | `/questions/how-to-design-systems-that-amplify-rather-than-replace/` | Question mark stripped |
| `Atlas/The Almanac/Questions (index)/What becomes scarce when AI can copy at scale?.md` | `/questions/what-becomes-scarce-when-ai-can-copy-at-scale/` | Question mark stripped |
| `Atlas/The Almanac/Questions (index)/What broader historical and structural narratives help situate political philosophy within the evolution of civilization, governance, and design?.md` | `/questions/what-broader-historical-and-structural-narratives-help-situate-political-philosophy-within-the-evolution-of-civilization-governance-and-design/` | Long URL (see A4); commas stripped; question mark stripped |
| `Atlas/The Almanac/Questions (index)/What cultural, communicative, and systemic infrastructures sustain a truthful, cooperative, and self-correcting society?.md` | `/questions/what-cultural-communicative-and-systemic-infrastructures-sustain-a-truthful-cooperative-and-self-correcting-society/` | Long URL (see A4); commas stripped; question mark stripped |
| `Atlas/The Almanac/Questions (index)/What does it mean to speak truth to power; and how can critique become a form of healing, renewal, and "rehumanization"?.md` | `/questions/what-does-it-mean-to-speak-truth-to-power-and-how-can-critique-become-a-form-of-healing-renewal-and-rehumanization/` | Semicolon → hyphen; commas stripped; quotation marks stripped; question mark stripped |
| `Atlas/The Almanac/Questions (index)/What does sustainable innovation look like?.md` | `/questions/what-does-sustainable-innovation-look-like/` | Question mark stripped |
| `Atlas/The Almanac/Questions (index)/What would professional data governance look like if designed for user sovereignty?.md` | `/questions/what-would-professional-data-governance-look-like-if-designed-for-user-sovereignty/` | Question mark stripped |
| `Atlas/The Almanac/Questions (index)/When do we build fluency capacity?.md` | `/questions/when-do-we-build-fluency-capacity/` | Question mark stripped |
| `Atlas/The Almanac/The Grove (index)/Concerning Capital Cognitive Capture.md` | `/the-grove/concerning-capital-cognitive-capture/` | |
| `Atlas/The Almanac/The Shed (index)/Architecture-Behaviour-Outcomes Model.md` | `/the-shed/architecture-behaviour-outcomes-model/` | |
| `Atlas/The Almanac/The Shed (index)/Dual-Mode Knowledge Model.md` | `/the-shed/dual-mode-knowledge-model/` | |
| `Atlas/The Almanac/The Shed (index)/Partnership Compact — Core Values for AI Collaboration.md` | `/the-shed/partnership-compact-core-values-for-ai-collaboration/` | Em-dash → hyphen |
| `Atlas/The Almanac/The Shed (index)/Setting up a prompt engineering project..md` | `/the-shed/setting-up-a-prompt-engineering-project/` | Trailing period stripped |
| `Atlas/The Almanac/The Shed (index)/The Socratic Prototyping Method.md` | `/the-shed/the-socratic-prototyping-method/` | |

---

## Section Summary

| Section | URL prefix | File count |
|---------|------------|------------|
| Home | `/` | 1 |
| Root content pages | `/about-me/`, `/about-the-site/`, etc. | 4 |
| Root gate pages | `/the-greenhouse/`, `/the-grove/`, `/the-shed/` | 3 |
| Atlas thematic maps | `/atlas/` | 10 |
| Concepts | `/concepts/` | 18 |
| Claims | `/claims/` | 16 |
| Questions | `/questions/` | 18 |
| Greenhouse | `/greenhouse/` | 3 |
| The Grove | `/the-grove/` | 1 |
| The Shed | `/the-shed/` | 5 |
| Top-level (direct Almanac children) | `/` | 1 |
| **Total** | | **80** |
