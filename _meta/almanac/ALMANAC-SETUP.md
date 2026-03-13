---
created: 2026-02-06
last_tended: 2026-02-06
type: effort
tags:
  - stub
up:
  - "[[cognitivearchitecture_ca]]"
---
# The Almanac Monthly — Setup Reference

> **Purpose:** Configuration reference for the Buttondown newsletter. Copy-paste sections into Buttondown's settings as needed. Not published.
> **Created:** 2026-02-05

---

## 1. Buttondown Profile Configuration

### Newsletter Name
```
The Almanac Monthly — Cognitive Architecture
```

### Username (URL slug)
```
cognitive.architecture
```
→ Produces: `buttondown.com/cognitive.architecture`

### Display Name / From Name
```
Seb — Cognitive Architecture
```

### Reply-to
Use whatever email you want replies going to. Buttondown free tier uses their sending domain, so the "from" address won't be your custom domain — but the reply-to can be.

---

## 2. Landing Page Copy (Subscribe Page)

This is what people see at your Buttondown URL. Paste into Buttondown's "Description" or landing page field. Markdown supported.

```markdown
A periodic dispatch from [Cognitive Architecture](https://cognitive-architecture.ca) — a digital garden exploring knowledge work, technology, philosophy, and what it means to keep humanity at the centre of increasingly complex systems.

The Almanac Monthly is a curated digest, not a feed. Each issue highlights new plantings, recently tended notes, and fragments still taking shape. It arrives monthly, sometimes less. No automation, no algorithmic urgency — just a human pointing at what's growing.

If technology conversations feel like they move too fast or skip important human considerations, this is designed with your perspective in mind.
```

### Shorter variant (if Buttondown's description field has a character limit):

```markdown
Monthly dispatch from a digital garden at the intersection of knowledge work, technology, and human-centred design. New notes, revised thinking, and seeds not yet planted.
```

---

## 3. Welcome Email (First Email After Subscribe)

Buttondown lets you configure an automatic welcome email. Paste this into the welcome email content field.

```markdown
Thanks for subscribing to The Almanac Monthly.

This is a periodic digest from [Cognitive Architecture](https://cognitive-architecture.ca) — a digital garden where I work through questions about knowledge, technology, and what it looks like to design systems that amplify human thinking rather than replace it.

Each issue follows a simple structure: new notes I've published, existing notes I've meaningfully revised, and sometimes a handful of fragments that don't have their own page yet.

It arrives monthly. There's no algorithm deciding what you see — I compose each issue by hand from what's actually growing in the garden.

In the meantime, you're welcome to explore: [cognitive-architecture.ca](https://cognitive-architecture.ca)

— Seb
```

---

## 4. Subscribe Page Metadata

### Meta description (SEO / social share)
```
Subscribe to The Almanac Monthly — a digest from Cognitive Architecture, a digital garden exploring knowledge work, technology, and human-centred design.
```

### Social share image
If Buttondown lets you set an OG image, use the same banner image from your site (`banner-w-borders.jpg`). You'd need to host it at a public URL — your Obsidian Publish site serves it, so the URL would be something like:
```
https://cognitive-architecture.ca/banner-w-borders.jpg
```
Test whether that resolves before using it.

---

## 5. Buttondown Settings Checklist

- [ ] Set newsletter name: "The Almanac Monthly — Cognitive Architecture"
- [ ] Set username/slug
- [ ] Paste landing page copy into description
- [ ] Configure welcome email
- [ ] Set reply-to address
- [ ] Set meta description if available
- [ ] Test subscribe flow end-to-end (subscribe yourself with a secondary email)
- [ ] Confirm welcome email arrives and renders correctly
- [ ] Confirm unsubscribe link works

---

## 6. Obsidian Publish — Subscribe Integration

Obsidian Publish doesn't support custom widgets, embeds, or JavaScript injection. Your options for surfacing the subscribe link are:

### Option A: Add to Home.md (Recommended)

Add a subscribe callout to your Home page, in the navigation section. Fits naturally with your existing callout structure.

Suggested placement: After the "Garden Gates + Maps" section, before "Search & Tags."

```markdown
> [!mail] The Almanac Monthly
> _A monthly dispatch highlighting new plantings, recently tended notes, and seeds still taking shape._
>
> [Subscribe →](https://buttondown.com/cognitive.architecture)
```

Callout type `[!mail]` may not have a built-in icon in your publish theme — test it. Alternatives: `[!info]`, `[!abstract]`, or a custom callout type via your publish.css.

### Option B: Dedicated Subscribe Note

Create a standalone note that's published and linked from navigation:

**File:** `Subscribe.md` (at vault root, alongside Home, About, etc.)

```markdown
---
created: 2026-02-05
last_tended: 2026-02-05
status: evergreen
tags: [meta]
aliases: [subscribe, newsletter]
up: ["[[Home]]"]
---

# The Almanac Monthly

A periodic dispatch from this garden — curated, not automated. Each issue highlights what's been planted, what's been tended, and what's still germinating.

Monthly. Composed by hand. No tracking beyond what Buttondown's free tier provides by default.

**[Subscribe via Buttondown →](https://buttondown.com/cognitive.architecture)**

Past issues are archived in the garden but not published here — The Almanac Monthly is for subscribers.
```

Then add a link in Home.md's navigation:
```markdown
> #### [[Subscribe|The Almanac Monthly]] ✉
> ##### _Monthly dispatch. New plantings, tended notes, and seeds._
```

### Option C: Add to About the Site

Less prominent but zero friction — just append to the bottom of `About the site.md`:

```markdown
> [!mail] The Almanac Monthly
> _Monthly digest of what's growing here. [Subscribe →](https://buttondown.com/cognitive.architecture)_
```

### Recommendation

**Do both A and B.** Create the Subscribe note for anyone who lands on it directly or via search, and add the callout to Home.md for visibility. Option C is optional — good for discoverability but not essential.

---

## 7. Almanac Archive Template

For archiving sent issues in `_meta/almanac/`. Each issue gets a file:

**Filename pattern:** `almanac-001.md`, `almanac-002.md`, etc.

```markdown
---
type: almanac-archive
issue: 1
subject: "Almanac Monthly #1 — {thematic hook}"
sent: YYYY-MM-DD
subscriber-count: 0
---

# Almanac Monthly #1 — {thematic hook}

{Paste the full markdown content of the sent email here.}

---

## Pipeline Notes

**Candidates considered:**
- [[Note A]] — included as New Planting
- [[Note B]] — included as Recently Tended
- [[Note C]] — skipped (not ready)

**Post-send:**
- Set `almanac-status: featured` and `almanac-issue: 1` on all featured notes
- Moved skipped candidates back to `almanac-status: candidate` or `skip`
```

---

## 8. Pipeline Quick Reference

### Throughout the Month
Tend notes. The linter stamps `last tended`. When something feels newsletter-worthy, add it to `_meta/almanac/next.md` with a one-line annotation.

### Almanac Day
1. Open `next.md` — your composition plan is there
2. Quick triage: search `[almanac-status:candidate]` or sort by modification date to catch anything missed
3. Compose in Buttondown: Opening → New Plantings → Recently Tended → From the Grove (optional) → Field Notes → Closing
4. Subject line: `Almanac Monthly #{issue} — {brief thematic hook}`
5. Send

### After Sending
1. Archive: copy sent markdown to `_meta/almanac/almanac-{NNN}.md`
2. Update frontmatter: set `almanac-status: featured` and `almanac-issue: {N}` on featured notes
3. Clear `next.md` for next cycle

---

## Open Questions

- [x] **Buttondown username:** Confirmed: `cognitive.architecture`
- [x] **Naming:** Resolved. Vault section stays "The Almanac." Newsletter is "The Almanac Monthly."
- [ ] **Callout icon:** Test `[!mail]` callout type in your publish theme; may need CSS
- [ ] **OG image:** Test whether `https://cognitive-architecture.ca/banner-w-borders.jpg` resolves publicly
- [ ] **Subscribe note placement:** Root level alongside Home/About, or nested?
