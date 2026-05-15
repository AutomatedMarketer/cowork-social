# v0.1.0 — Initial Release: Social Media Content Engine for Cowork

## The big idea

Most content creators get the biggest single win out of this project. Sabrina Ramonov framed the Cowork + Blotato workflow in her [60-minute Cowork masterclass](https://youtu.be/-q_wgmmD0e0) like this:

> "It eliminated four steps you'd normally have to do. You can just be like, 'just upload this photo I took', and then it'll work and you don't have to worry about anything else."
>
> "This is your entire social media content calendar within co-work. Think about how powerful this is."

`cowork-social` is the plugin that operationalizes that workflow on a **weekly cadence**:

- **Hour 1** — Saturday 8am, `/generate-weekly-ideas` drops 10 ranked ideas in your workspace. Monday morning, `/weekly-content-session` walks you from those ideas → on-brand drafts → graded posts.
- **Hour 2** — your drafts get scheduled into Blotato (or saved to `outputs/` if you skip Blotato). Visuals, hashtags, line breaks per platform — handled.
- **Close the laptop.** Your week of content is queued. You move on to the work that pays you.

That's the project. Run it once, get a rhythm. Run it weekly, build a flywheel.

## What's new

- **13 skills** — wizard + brand-brief + content-coach + 6 platform draft skills (LinkedIn, X/Twitter, Instagram, Facebook, TikTok, Threads) + hook-weighted grader + 3 orchestrators (weekly session, weekly ideas, monthly review).
- **3 architectural foundations applied in every skill** — lazy-load context (no auto-loading business-brain), self-improving close (every skill ends with "anything to bake in for next time?"), ⚡ NEXT MOVE actionable close (specific next action + timing, never "let me know if you need anything else").
- **Cowork-native rewrite of Blotato's 5 official Claude Skills** — Blotato ships free Claude Skills for Claude Code; we rewrote them for Cowork's runtime (ZIP upload, sandboxed FS, cowork-ai-os identity layer). Plus 2 native additions (X, Threads) + 3 native orchestrators.
- **8-phase resumable wizard** — `/onboard-social` writes `state-social.md` on every phase transition. Stop any time, pick up where you left off.
- **Shared 12-step draft-skill spec** — `_shared/draft-skill-spec.md` is the single source of truth for all 6 platform drafts. Fix step 7 once, fix it everywhere.
- **11 proven hook patterns** — `_shared/hook-patterns.md` referenced by 8 skills. Reframe, Parallel Contrast, Specific Number, Question, Vulnerable Story, Contrarian Take, Pain Point List, Behind-the-Scenes, Receipts, Most People Reverse, Stolen Lesson.
- **Blotato MCP live-verified** in default Cowork environment on 2026-05-15. Namespace: `mcp__claude_ai_Blotato__*`. 16 tools wired in v0.1 (4 of them used directly by skills; 12 available for natural-language operations).
- **Foundation C-headless variant** — `/generate-weekly-ideas` runs Saturday 8am as a cron, so it can't surface a NEXT MOVE block in chat. It puts the NEXT MOVE in the **file footer** instead, where you find it Monday morning when you open the ideas file.

## About Blotato

**cowork-social is built for Blotato.** We chose it because of our experience — it works best with everything else in the Cowork stack (direct local-file upload, 16 MCP tools, OAuth-friendly, up to 20 social accounts on one seat).

- **If you already have a Blotato account:** ignore the affiliate link below. Just OAuth-connect during the wizard's Phase 4.
- **If you're new to Blotato:** sign up at [blotato.com/?ref=nuno](https://blotato.com/?ref=nuno) and use code `NUNO30` at checkout for **30% off your first 3 months** ($29/mo → $20.30/mo).
- **If you don't want Blotato at all:** the wizard skips Phase 4 cleanly. Drafts still save to `outputs/social-media-content/` — you'll schedule manually inside each platform. About 80% of cowork-social's value retained.

### How to wire Blotato in Cowork (3 clicks)

1. Settings → Connectors → **Add Custom Connector**
2. Paste the Blotato MCP URL the wizard surfaces
3. Click **Connect** → approve OAuth in the browser → done

No JSON. No CLI. No API-key juggling. The wizard's Phase 4 walks you through it and detects the active subscription via `blotato_get_user` before letting you proceed.

## What's still deferred

These move to v0.2+ to keep v0.1 tight:

- **`/create-visual`** — Blotato visual templates (carousels, infographics, quote cards, manga, whiteboard) via `blotato_create_visual` + `blotato_list_visual_templates`. Pairs with `/weekly-content-session` to auto-attach visuals.
- **`/remix-source`** — YouTube / podcast / PDF / website scrape via `blotato_create_source` → platform-specific posts + auto-visual. Sabrina's "Hormozi YouTube → LinkedIn post + whiteboard infographic" workflow.
- **Mid-week tune-up skill** — Wednesday refresh between Monday batch and weekend ideation.
- **Custom Blotato schedules per ICP segment** — different cadences for different audience segments.
- **Multi-account / multi-brand support** — one brand per workspace in v0.1.
- **Engagement-data feedback loop** — `/grade-post` learns from `blotato_list_posts` published metrics.
- **Bluesky, Pinterest, YouTube publishing** — Blotato supports them; we don't wire them in v0.1.
- **Custom Cowork MCP server** — `social_draft`, `social_grade`, `calendar_log` as first-class MCP tools. Ships once we've watched 20+ users hit specific friction.

## Install

New install:

```
/plugin marketplace add AutomatedMarketer/cowork-social
/plugin install cowork-social@cowork-social
/onboard-social
```

**Prereqs:** `cowork-ai-os >= 0.10` for identity files (`about-me/about-me.md`, `business-brain.md`, `connections.md`). `cowork-ai-os >= 0.10.2` recommended for live connector catalogs. Loose-couples with `cowork-research >= 0.2` (shared Blotato MCP).

## Breaking changes

**None.** This is the initial release.

## What's next

- **v0.2 — visual generation pipeline.** `/create-visual` (Blotato visual templates) + `/remix-source` (YouTube/podcast/PDF scrape → platform posts + auto-visual). The Hormozi-YouTube-to-LinkedIn-post-plus-whiteboard workflow Sabrina demoed becomes a one-prompt operation.
- **v0.3 — engagement feedback loop.** `/grade-post` learns from published-engagement metrics. Mid-week tune-up skill. Multi-account scheduling.
- **v0.4+ — custom Cowork MCP server.** Once we've watched 20+ users hit specific friction, we ship `social_draft`, `social_grade`, `calendar_log` as first-class MCP tools.
- **The modular-plugin roadmap is unchanged.** `cowork-ai-os` (identity) → `cowork-obsidian` (vault) → `cowork-research` (research engine) → `cowork-social` (THIS) → `cowork-financial` (P&L + cashflow briefs) → `cowork-highlevel` (GoHighLevel CRM ops). Each ships independently. None require the others, but they compose well when stacked.

## Credits

Built by Nuno Tavares of [Automated Marketer](https://automatedmarketer.net) for the [VCInc](https://vcinc.com) cohort.

- **Sabrina Ramonov** — her [60-minute Cowork masterclass](https://youtu.be/-q_wgmmD0e0) is the framing source for the "Hour 1 / Hour 2 / close laptop" pattern this plugin operationalizes. The "it eliminated four steps you'd normally have to do" framing for Blotato's local-upload superpower is hers verbatim.
- **Blotato team** — for the 5 free Claude Skills we used as inspiration + reference for the Cowork-native rewrites. Hook patterns and grader weights are spiritually descended from their originals; runtime is entirely ours.
- **VCInc cohort students** — the cohort whose weekly-content friction shaped which 13 skills shipped first.
- **Karpathy's [LLM Wiki gist](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)** — the original "Obsidian is the IDE, the LLM is the programmer, the wiki is the codebase" framing carried over from sibling cowork plugins.
- **Memory architecture pattern** — carried over from `cowork-obsidian v0.5` and `cowork-research v0.2`.

v0.1 specifically: the "Hour 1 / Hour 2 / close laptop" framing came from watching cohort users say "I know I should post weekly but Mondays always get away from me" — the Monday-blank-page friction is what gates compounding, and the orchestrators (`/weekly-content-session` + `/generate-weekly-ideas`) are designed to remove it.
