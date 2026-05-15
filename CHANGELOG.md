# Changelog

All notable changes to `cowork-social` will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [0.1.0] — 2026-05-15 — "Initial Release: Social Content Engine for the Cowork AI OS"

### Added — Initial release

- **`/onboard-social` wizard** — 8-phase install flow (~15 min). Resumable via `state-social.md`. Includes prereq check for cowork-ai-os.
- **`/brand-brief` skill** — Auto-derives brand brief from `about-me/business-brain.md`. Asks delta questions only — never re-collects identity.
- **`/content-coach` skill** — 5 ranked post ideas tied to wedge, virality-mixed (a few safe bets, a few swings).
- **`/draft-linkedin` skill** — LinkedIn-tuned 12-step draft (500–1500 chars, comment-CTA bias, image-aware via asset-index).
- **`/draft-twitter` skill** — Native (Blotato doesn't cover X). 280-char per tweet + thread support.
- **`/draft-instagram` skill** — IG-tuned + image-mandatory awareness via asset-index.md + hashtag block.
- **`/draft-facebook` skill** — FB-tuned + link-preview-aware + reel-type guard.
- **`/draft-tiktok` skill** — NEW surface. Script (hook ≤ 3s structure) + caption + hashtags.
- **`/draft-threads` skill** — Native (Blotato doesn't cover Threads). 500-char + reply chains.
- **`/grade-post` skill** — 6-dimension hook=50% weighted rubric. Top 3 ranked fixes + estimated post-fix score.
- **`/weekly-content-session` skill** — Monday batch orchestrator. Calls draft skills + Blotato schedule. Falls back to drafts-only if Blotato disconnected.
- **`/generate-weekly-ideas` skill** — Saturday 8am cron. 10 ranked ideas with virality scoring. Headless variant — NEXT MOVE in file footer for cron contexts.
- **`/content-engine-review` skill** — Monthly retro. Calendar-log + memory + skill-improvements walkthrough. Platform-mix analysis + tuning proposals.
- **3 architectural foundations applied in every skill** — lazy-load context, self-improvement close, ⚡ NEXT MOVE actionable close.
- **7 onboarding templates** — `state-social.md`, `brand-brief.md`, `platform-voice.md`, `asset-index.md`, `scheduling-defaults.md`, `trend-sources.md`, `calendar-log.md`.
- **Shared 12-step draft-skill spec** (`_shared/draft-skill-spec.md`) — single source of truth for all 6 platform draft skills.
- **11 proven hook patterns** (`_shared/hook-patterns.md`) — Reframe, Parallel Contrast, Specific Number, Question, Vulnerable Story, Contrarian Take, Pain Point List, Behind-the-Scenes, Receipts, Most People Reverse, Stolen Lesson. Referenced by `/content-coach`, all 6 `/draft-*`, and `/grade-post`.
- **Connector catalog** (`connectors-social.md`) — Blotato (live-verified 2026-05-15) + 3 cross-cutting MCPs already verified in cowork-research v0.2 + skip-list.
- **6 personalization profiles** — one per business type (Solo coach, Agency owner, Creator, Course creator, Solopreneur/SMB, Sales-led B2B).

### Architectural decisions

- **Cowork-native rewrites of Blotato's 5 free Claude Skills** — `content-coach`, `brand-brief`, `post-writer` (split into 6 platform-specific drafts), `post-grader`, `post-scheduler` (folded into `/weekly-content-session`). Blotato's versions target Claude Code (filesystem-based, `~/.claude/skills/`); we rewrote them for Claude Cowork's runtime (ZIP upload via Customize → Skills, sandboxed FS, cowork-ai-os identity layer). Hook patterns + grader weights are spiritually descended from Blotato's originals; runtime is entirely ours.
- **2 native additions** — `/draft-twitter` and `/draft-threads` (Blotato's post-writer doesn't cover X or Threads).
- **3 native orchestrators** — `/weekly-content-session`, `/generate-weekly-ideas`, `/content-engine-review` (no Blotato analog).
- **Shared-spec architecture** — `_shared/foundations.md`, `_shared/draft-skill-spec.md`, `_shared/hook-patterns.md` are single sources of truth; each skill references them rather than duplicating logic.
- **Foundation C-headless variant** — `/generate-weekly-ideas` puts NEXT MOVE in file footer (cron context, no live user reading chat).

### Verified

- All 13 skills apply the 3 architectural foundations (lazy-load, self-improving, ⚡ NEXT MOVE).
- **Blotato MCP live-tested** in default Cowork environment on 2026-05-15: `mcp__claude_ai_Blotato__blotato_get_user` returned `{subscriptionStatus: "active"}`. Namespace confirmed: `mcp__claude_ai_Blotato__*` (single-prefix, NOT doubled-prefix like Context7 or Playwright).
- 4 cross-cutting MCPs (Perplexity, Firecrawl, Context7, Playwright) inherited as live-verified from cowork-research v0.2.0 (same 2026-05-15 smoke-test session).

### Notes

- Soft-depends on `cowork-ai-os >= 0.10` for identity files (`about-me/about-me.md`, `business-brain.md`, `connections.md`).
- `cowork-ai-os >= 0.10.2` recommended for live connector catalogs (Phase 2 delegates to `/browse-connectors`).
- Loose-coupled with `cowork-research >= 0.2` — both plugins share the Blotato MCP cleanly. If you've already wired Blotato for cowork-research, cowork-social detects it and skips Phase 4's OAuth step.
- Blotato MCP URL surfaced by the wizard. Affiliate link: `https://blotato.com/?ref=nuno`. Discount code `NUNO30` → 30% off first 3 months. Affiliate framing is gated to the "new user" branch only.
- **No course SOPs in this repo** — course material lives in the private course workspace per the modular-plugin rule (carried over from cowork-obsidian v0.5 and cowork-research v0.1+v0.2).

### Deferred to v0.2+

- `/create-visual` — Blotato visual templates (carousels, infographics, quote cards, manga, whiteboard) via `blotato_create_visual`
- `/remix-source` — YouTube / podcast / PDF / website scrape via `blotato_create_source` for content remix
- Mid-week tune-up skill — Wednesday refresh between Monday batch and weekend
- Custom Blotato schedules per ICP segment (different timings for different audience segments)
- Multi-account / multi-brand support
- Bluesky, Pinterest, YouTube publishing surfaces (Blotato supports them; we don't wire them in v0.1)
- Engagement-data feedback loop — `/grade-post` learning from `blotato_list_posts` published metrics
- Custom Cowork MCP server — `social_draft`, `social_grade`, `calendar_log` as first-class MCP tools
- Stop-hook auto-extract — fold session insights into `skill-improvements.md` automatically

[0.1.0]: https://github.com/AutomatedMarketer/cowork-social/releases/tag/v0.1.0
