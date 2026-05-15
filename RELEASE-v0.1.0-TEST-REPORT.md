# cowork-social v0.1.0 — Verification Matrix

**Date:** 2026-05-15
**Status:** GREEN — 55/55

## Summary

- Foundation B per skill: 13/13
- Foundation C per skill: 13/13
- Slash-name consistency: 13/13
- Affiliate surfaces: 6/6
- Structural checks: 10/10
- **TOTAL: 55/55**

Manifest version-consistency check (G.1) and release zip build (G.2) also PASS.

### G.1 — Manifest version consistency

- `cowork-social/.claude-plugin/plugin.json` → `"version": "0.1.0"` ✅
- `.claude-plugin/marketplace.json` → `"version": "0.1.0"` ✅
- All 13 SKILL.md `version:` frontmatter fields → `0.1.0` ✅
- `CHANGELOG.md` first entry → `## [0.1.0] — 2026-05-15` ✅
- `RELEASE-v0.1.0.md` title references v0.1.0 ✅
- Other `0.2.x` / `0.10.x` matches are legitimate dependency-version refs for cowork-ai-os / cowork-research / future v0.2 features — not version drift.

### G.2 — Release zip

- Path: `d:/dev/cowork-social/release/cowork-social-v0.1.0.zip`
- Size: 107,490 bytes
- Total files: 38 (>30 threshold ✅)
- 13 SKILL.md files (one per declared skill) ✅
- `.claude-plugin/plugin.json` present in zip ✅
- plugin.json inside zip declares 13 skills, version 0.1.0 ✅
- ZERO SOP-shaped filenames (`sop`, `06-social-media-content`, `01b-wizard`, `why-hire`, `setting-up`) ✅
- All 9 onboard-social/phases/ files (00-welcome through 08-cadence-and-calibration) ✅

---

## Detailed test results

### Foundation B per skill (13/13)

For each SKILL.md: contains canonical `"What would've made this 10% better?"` (or scoped variant), references `_shared/foundations.md`, appends to `projects/social-media-content/memory.md`, and has 60%-overlap + 3+ recurrence → `skill-improvements.md` staging (either inline or via foundations.md reference).

| # | Skill | Canonical question | foundations.md ref | memory.md append | Recurrence staging | Result |
|---|---|---|---|---|---|---|
| 1 | onboard-social | "What would've made this onboarding 10% better?" (line 74, 106) | Yes (line 88-90, 106) | Yes (line 74, 106) | Inline reference to foundations.md Foundation B (line 89) | ✅ |
| 2 | brand-brief | "What would've made this 10% better?" (line 126) | Yes (line 124) | Yes (line 92, 107, 128) | Inline 60%-overlap + 3+ recurrence (line 128); `skill-improvements.md` named (line 128) | ✅ |
| 3 | content-coach | "What would've made this 10% better?" (line 137) | Yes (line 135) | Yes (line 102, 116, 139) | Inline 60%-overlap + 3+ recurrence (line 139); `skill-improvements.md` named | ✅ |
| 4 | draft-linkedin | "What would've made this 10% better?" (line 99) | Yes (line 99) | Yes (line 99) | Via foundations.md reference (line 99); recurrence rule canonicalized there | ✅ |
| 5 | draft-twitter | "What would've made this 10% better?" (line 136) | Yes (line 136, 146) | Yes (line 136) | "Run recurrence check" (line 142) + foundations.md ref | ✅ |
| 6 | draft-instagram | "What would've made this 10% better?" (line 116) | Yes (line 116, 126) | Yes (line 116) | Via foundations.md reference; recurrence rule canonicalized there | ✅ |
| 7 | draft-facebook | "What would've made this 10% better?" (line 105) | Yes (line 105, 115) | Yes (line 105) | Via foundations.md reference; recurrence rule canonicalized there | ✅ |
| 8 | draft-tiktok | "What would've made this 10% better?" (line 149) | Yes (line 149, 159) | Yes (line 149) | Via foundations.md reference; recurrence rule canonicalized there | ✅ |
| 9 | draft-threads | "What would've made this 10% better?" (line 134) | Yes (line 134, 144) | Yes (line 134) | Via foundations.md reference; recurrence rule canonicalized there | ✅ |
| 10 | grade-post | "What would've made this 10% better?" (line 143) | Yes (line 141, 162) | Yes (line 147) | Inline 60%-overlap + 3+ recurrence; `skill-improvements.md` named | ✅ |
| 11 | weekly-content-session | "What would've made this 10% better?" (line 199) | Yes (line 33, 197, 218, 248, 261) | Yes (line 201) | Inline recurrence-check + `skill-improvements.md` named | ✅ |
| 12 | generate-weekly-ideas | Headless variant — Foundation B adapted to file-write log (line 187-204); canonical question skipped per headless exception (line 189) | Yes (line 35, 187, 204, 212, 238) | Yes (line 190) — appends per-run log; `skill-improvements.md` referenced (line 204) | Headless adaptation: file-row append + recurrence check on next manual run; foundations.md ref | ✅ |
| 13 | content-engine-review | "What would've made this review 10% better?" (line 222) | Yes (line 37, 220, 243, 273, 286) | Yes (line 32, 224) | Inline recurrence-check + `skill-improvements.md` review surface (this skill IS the monthly retro that processes the queue) | ✅ |

**Foundation B subtotal: 13/13 PASS**

### Foundation C per skill (13/13)

For each SKILL.md: contains canonical `⚡ NEXT MOVE:` block (correct emoji + caps + colon), `Why:` line in canonical position, validation regex `⚡ NEXT MOVE: .+ .+ .+\n   Why: .+` (or D.12's file-footer variant), picking rule appropriate to skill.

| # | Skill | NEXT MOVE block | Why: line | Validation regex | Picking rule | Result |
|---|---|---|---|---|---|---|
| 1 | onboard-social | Yes (line 71, 73, 90) — wrap-up emits canonical block | Yes — "platform-aware, picks one specific action" (line 71) | Yes — regex named at line 71 | Platform-aware (LinkedIn → engage on last post, etc.) | ✅ |
| 2 | brand-brief | Yes (line 135 regex, examples lines 142-144) | Yes (line 135 regex includes `Why:`) | Yes (line 135) | Onboarding/setup post-brief → "Run /draft-* or /content-coach" | ✅ |
| 3 | content-coach | Yes (line 146 regex, examples lines 153-155) | Yes (line 146 regex includes `Why:`) | Yes (line 146) | "Pick idea #N and run /draft-<platform>" within hour | ✅ |
| 4 | draft-linkedin | Yes (line 109 ref, examples lines 121-131) | Yes — all examples include `Why:` line | Yes — references foundations.md regex | Blotato connected → Schedule; skipped → Post manually; live → Reply check | ✅ |
| 5 | draft-twitter | Yes (line 146 ref, examples lines 158-168) | Yes — all examples include `Why:` line | Yes — references foundations.md regex | Per Twitter NEXT MOVE priority list (line 148-153) | ✅ |
| 6 | draft-instagram | Yes (line 126 ref, examples lines 138-148) | Yes — all examples include `Why:` line | Yes — references foundations.md regex | Schedule via Blotato / Fix asset / Reply to comments | ✅ |
| 7 | draft-facebook | Yes (line 115 ref, examples lines 127-137) | Yes — all examples include `Why:` line | Yes — references foundations.md regex | Schedule on page / Re-run Phase 6 / Check shares | ✅ |
| 8 | draft-tiktok | Yes (line 159 ref, examples lines 171-181) | Yes — all examples include `Why:` line | Yes — references foundations.md regex | Record TikTok / Add reel asset / Check 3s watch-through | ✅ |
| 9 | draft-threads | Yes (line 144 ref, examples lines 156-166) | Yes — all examples include `Why:` line | Yes — references foundations.md regex | Schedule / Post manual + seed reply / Reply rate check | ✅ |
| 10 | grade-post | Yes (line 162 ref, regex line 165, examples lines 172-191) | Yes — regex includes `Why:` | Yes (line 165 + line 191) | Score-aware: ≥80 schedule / <80 rewrite hook / <60 re-run draft | ✅ |
| 11 | weekly-content-session | Yes (line 216 H2, examples lines 223-244) | Yes — all examples include `Why:` line | Yes (line 248) | Session-state-aware: scheduled / drafts-only / paused / Blotato skipped | ✅ |
| 12 | generate-weekly-ideas | **File-footer variant** (line 19, 53, 177, 210, 233) — NOT chat output | Yes — examples lines 220-221 include `Why:` line | Yes (line 216) | Headless adaptation — points to next Monday's /weekly-content-session run with top idea | ✅ |
| 13 | content-engine-review | Yes (line 241 H2 — verdict-aware, 3 variants, lines 248-262) | Yes — all 3 variants include `Why:` line | Yes (line 273) | Verdict-aware: red / yellow / green branches | ✅ |

**Foundation C subtotal: 13/13 PASS**

### Slash-name consistency (13/13)

For each SKILL.md: frontmatter `slug:` matches folder name.

| # | Folder | Slug in frontmatter | Result |
|---|---|---|---|
| 1 | onboard-social | `slug: /onboard-social` | ✅ |
| 2 | brand-brief | `slug: /brand-brief` | ✅ |
| 3 | content-coach | `slug: /content-coach` | ✅ |
| 4 | draft-linkedin | `slug: /draft-linkedin` | ✅ |
| 5 | draft-twitter | `slug: /draft-twitter` | ✅ |
| 6 | draft-instagram | `slug: /draft-instagram` | ✅ |
| 7 | draft-facebook | `slug: /draft-facebook` | ✅ |
| 8 | draft-tiktok | `slug: /draft-tiktok` | ✅ |
| 9 | draft-threads | `slug: /draft-threads` | ✅ |
| 10 | grade-post | `slug: /grade-post` | ✅ |
| 11 | weekly-content-session | `slug: /weekly-content-session` | ✅ |
| 12 | generate-weekly-ideas | `slug: /generate-weekly-ideas` | ✅ |
| 13 | content-engine-review | `slug: /content-engine-review` | ✅ |

**Slash consistency subtotal: 13/13 PASS**

(Note: 6 secondary `slug: <kebab-case-3-5-words>` matches inside draft-* SKILL.md files are output-format scaffolding for the generated draft files, not skill slugs — correct.)

### Affiliate surfaces (6/6)

Both `https://blotato.com/?ref=nuno` AND `NUNO30` present in:

| # | Surface | Path | ref=nuno | NUNO30 | Result |
|---|---|---|---|---|---|
| 1 | Wizard phase | `cowork-social/skills/onboard-social/phases/04-blotato-setup.md` | ✅ | ✅ | ✅ |
| 2 | Catalog | `cowork-social/skills/onboard-social/catalogs/connectors-social.md` | ✅ | ✅ | ✅ |
| 3 | Public README | `d:/dev/cowork-social/README.md` | ✅ | ✅ | ✅ |
| 4 | Public release notes | `d:/dev/cowork-social/RELEASE-v0.1.0.md` | ✅ | ✅ | ✅ |
| 5 | Workspace SOP | `d:/dev/Claude Code - Second Brain/Claude Co-Work/SOPs/06-social-media-content/04-blotato-setup.md` | ✅ | ✅ | ✅ |
| 6 | Workspace install guide | `d:/dev/Claude Code - Second Brain/Claude Co-Work/install-guides/06-social-media-content.md` | ✅ | ✅ | ✅ |

**Affiliate surfaces subtotal: 6/6 PASS**

### Structural checks (10/10)

| # | Check | Expected | Actual | Result |
|---|---|---|---|---|
| 1 | plugin.json declares 13 skills | 13 | 13 (verified via Python json.load) | ✅ |
| 2 | marketplace.json version matches plugin.json | 0.1.0 = 0.1.0 | Both at 0.1.0 | ✅ |
| 3 | Zero stale `Project 05` refs in `SOPs/06-social-media-content/` | 0 stale | Only hit is the legitimate wikilink to actual Project 05 — Research (in `07-verification-and-iteration.md` line 261), which IS the correct reference | ✅ |
| 4 | Build zip excludes SOP filenames | 0 matches | 0 matches (verified via zip namelist scan for `sop`, `06-social-media-content`, `01b-wizard`, `why-hire`, `setting-up`) | ✅ |
| 5 | `_shared/foundations.md` exists | Present | Present (143 lines, canonical Foundation B + C definitions) | ✅ |
| 6 | `_shared/draft-skill-spec.md` exists | Present | Present | ✅ |
| 7 | `_shared/hook-patterns.md` exists | Present | Present (11 proven hook patterns) | ✅ |
| 8 | `connectors-social.md` exists at `onboard-social/catalogs/` | Present | Present | ✅ |
| 9 | `grade-post/templates/grading-rubric.md` exists with hook=50% | Present + hook=50% | Present; hook=50% documented at line 27 ("**Hook quality** \| **50%**") + load-bearing note at line 34 | ✅ |
| 10 | All 9 `/onboard-social/phases/` files exist (00-08) | 9 files | 9 files: 00-welcome, 01-auto-derive-brand-brief, 02-platform-selection, 03-platform-voice-capture, 04-blotato-setup, 05-asset-index, 06-scheduling-defaults, 07-first-live-draft, 08-cadence-and-calibration | ✅ |

**Structural subtotal: 10/10 PASS**

---

## Fixes applied during verification

None. All 55 checks passed on first sweep. Phase A-F commits are correct as-shipped.

---

## Concerns / BLOCKED items for Nuno

None.

### Notes on Foundation B for the 6 platform-draft skills

The 6 `/draft-*` skills (LinkedIn, Twitter, Instagram, Facebook, TikTok, Threads) reference `_shared/foundations.md → Foundation B` rather than inlining the 60%-overlap + 3+ recurrence logic. This is by design (DRY — foundations.md is the canonical source). Each draft skill names the canonical question + memory.md append format + "Run recurrence check" pointer. Compliant via reference.

If you'd prefer inline copies in each draft skill (for self-contained reading), say the word — it's a small append to each file. Current design intentionally keeps the rule in one place per the spec note "References `_shared/foundations.md` for B + C. Don't duplicate the rules inline."

### Note on `/generate-weekly-ideas` (D.12)

Headless variant — Foundation B's "ask user 10% better question" can't run (no live user on Saturday 8am cron). The skill adapts by:

1. Skipping the live question (line 189)
2. Logging the run to `memory.md` per file-row format (line 190)
3. Recurrence check runs on the NEXT manual `/weekly-content-session` Monday morning when a user IS present (line 191-204)
4. Foundation C `⚡ NEXT MOVE` lives in the FILE FOOTER (line 19, 53, 177, 210, 233), not chat — the user reads it Monday when they open the file. Validation regex applies to the file footer text (line 216).

This is explicitly documented in `_shared/foundations.md` as the "headless exception" pattern. Compliant.

---

## Live-Cowork tests pending (non-blocking for GitHub push)

These require Nuno to run them in a clean Cowork session post-install to confirm runtime behavior matches the static design. They are NOT blockers for G.4 publish gate.

| Test | How Nuno runs it live |
|---|---|
| Wizard end-to-end | Run `/onboard-social` clean → walk all 8 phases → confirm `state-social.md` writes `install_complete: true` as final step + Phase 8 wrap-up message lists all 13 skills + canonical NEXT MOVE renders |
| Brand brief auto-derive | Run `/brand-brief` with populated `business-brain.md` → confirm it auto-derives 80% of fields + asks delta questions only — never re-collects identity |
| Draft skill canonical close | Run `/draft-linkedin` (or any draft-* skill) → confirm output ends with canonical NEXT MOVE block + "What would've made this 10% better?" prompt fires |
| Grade canonical fix output | Run `/grade-post` on a known-weak post → confirm Top 3 fixes ranked + estimated post-fix score + verdict-aware NEXT MOVE |
| Weekly session orchestrator | Run `/weekly-content-session` end-to-end → confirm it chains: ideas → drafts → grade → schedule via Blotato → calendar-log append; gracefully falls back to drafts-only if Blotato disconnected |
| Saturday cron behavior | Trigger `/generate-weekly-ideas` headless → confirm output file lands at `projects/social-media-content/weekly-ideas-<date>.md` + file footer contains canonical NEXT MOVE block + memory.md gets the run row |
| Monthly retro | Run `/content-engine-review` after a month of data → confirm 3 verdict branches (red/yellow/green) work + skill-improvements.md staged changes are surfaced for review |
| Recurrence flag | Run any skill 3+ times with similar feedback ("hook was weak", "voice felt off", etc.) → confirm recurrence detection fires + `skill-improvements.md` row gets staged |
| Blotato MCP wiring | After Phase 4 of onboarding completes → confirm `blotato_list_accounts` resolves + scheduling actually posts to the chosen platforms |
| Affiliate visibility | Open README on GitHub post-publish → confirm Blotato affiliate link + NUNO30 code render in browser without manual scroll |

---

## Conclusion

**GREEN — clear to push, tag, and publish to GitHub** (after explicit Nuno confirmation per the G.4 human gate).

- Static + inspection: 55/55 PASS
- Manifest version consistency: PASS
- Release zip build: PASS (38 files, 107 KB, zero SOP leakage, 13 SKILL.md, plugin.json present)
- Dynamic in-Cowork verification: procedure documented above
- Recommendation: GO for G.4 sign-off, then proceed with G.5 (tag) → G.6 (push) → G.7 (release) → G.8 (Downloads sync + memory update)
