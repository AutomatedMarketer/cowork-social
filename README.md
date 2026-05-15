# cowork-social

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square)](./LICENSE)
[![Version](https://img.shields.io/badge/version-0.1.0-brightgreen.svg?style=flat-square)](./CHANGELOG.md)
[![Platform: Mac · Windows · Linux](https://img.shields.io/badge/platform-Mac%20%C2%B7%20Windows%20%C2%B7%20Linux-blue.svg?style=flat-square)](#install)
[![Built for Claude Cowork](https://img.shields.io/badge/built%20for-Claude%20Cowork-7C3AED.svg?style=flat-square)](https://claude.com/product/cowork)

A [Claude Cowork](https://claude.com/product/cowork) plugin (also runs in [Claude Code](https://claude.com/product/claude-code)) that turns your assistant into a **full-time social media content engine** — ideas, on-brand drafts across 6 platforms, hook-weighted grading, and scheduled posting that compounds week over week.

> **Stop staring at the blank post box every Monday. Your assistant already knows your business, your voice, and your ICP. Give it the right skills and Blotato — and your content engine runs itself.**

Built by [Nuno Tavares](https://nunomtavares.com) for [VCInc](https://vcinc.com) cohort students and anyone who wants a content rhythm that survives a busy week.

---

## The big idea (read this first)

Most content creators get the biggest single win out of this project. Sabrina Ramonov framed the Cowork + Blotato workflow in her [60-minute Cowork masterclass](https://youtu.be/-q_wgmmD0e0) like this:

> "It eliminated four steps you'd normally have to do. You can just be like, 'just upload this photo I took', and then it'll work and you don't have to worry about anything else."
>
> "This is your entire social media content calendar within co-work. Think about how powerful this is."

`cowork-social` is the install + scaffold + wiring that makes that practical on a **weekly cadence**:

- **Hour 1** — `/generate-weekly-ideas` runs Saturday 8am. Monday morning, `/weekly-content-session` walks you from those ideas → drafts → graded posts.
- **Hour 2** — your drafts get scheduled into Blotato (or saved to `outputs/` if you skip Blotato). Visuals, hashtags, line breaks per platform — handled.
- **Close the laptop.** Your week of content is queued. You move on to the work that actually pays you.

That's the project. Run it once, get a rhythm. Run it weekly, build a flywheel.

---

## What it ships (13 skills)

| # | Skill | Slash | What it does |
|---|---|---|---|
| 1 | **Onboard wizard** | `/onboard-social` | 8-phase install (~15 min). Reads your business-brain, picks your platforms, sets your post cadence, wires Blotato (if you want), calibrates your voice. State-resumable. |
| 2 | **Brand brief** | `/brand-brief` | Auto-derives from `about-me/business-brain.md`. Asks delta questions only — no re-collecting identity. |
| 3 | **Content coach** | `/content-coach` | 5 ranked post ideas tied to your wedge. Virality-mixed (a few safe bets, a few swings). |
| 4 | **Draft LinkedIn** | `/draft-linkedin` | 500–1500 chars, hook-first, comment-CTA bias. Image-aware via asset-index. |
| 5 | **Draft Twitter / X** | `/draft-twitter` | 280-char per tweet + thread support. Native (Blotato doesn't cover X). |
| 6 | **Draft Instagram** | `/draft-instagram` | IG voice, caption length, image-mandatory awareness, hashtag block. |
| 7 | **Draft Facebook** | `/draft-facebook` | FB voice, link-preview-aware, reel-type guard. |
| 8 | **Draft TikTok** | `/draft-tiktok` | Hook ≤ 3-second script + caption + hashtags. New surface for v0.1. |
| 9 | **Draft Threads** | `/draft-threads` | 500-char + reply chains. Native (Blotato doesn't cover Threads). |
| 10 | **Grade post** | `/grade-post` | 6-dimension rubric. Hook = 50% weight. Top 3 ranked fixes + estimated post-fix score. |
| 11 | **Weekly session** | `/weekly-content-session` | Monday 2-hour batch orchestrator. Ideas → draft → grade → schedule → log. |
| 12 | **Weekly ideas** | `/generate-weekly-ideas` | Saturday 8am scheduled task. 10 ranked ideas with virality scoring. Headless — NEXT MOVE in file footer. |
| 13 | **Engine review** | `/content-engine-review` | Monthly retrospective. Platform-mix analysis + tuning proposals. |

13 commands. One wizard wires the rest.

---

## The 3 architectural foundations

Every cowork plugin we ship follows the same 3 rules. cowork-social applies them in all 13 skills.

| Foundation | What it means | Where you see it |
|---|---|---|
| **Lazy-load context** | No skill auto-loads identity at startup. Each skill reads only what it needs, only when it needs it. | `/draft-linkedin` reads `brand-brief.md` + `platform-voice.md`. It doesn't touch `business-brain.md` unless brand-brief is missing. |
| **Self-improving skills** | Every skill closes with a 10%-better self-improve prompt that lets you tune it without leaving the run. | "Anything in this run we should bake into the skill so it goes better next time?" |
| **⚡ NEXT MOVE close** | Every skill ends with a specific next action + timing — never just "let me know if you need anything else." | "⚡ NEXT MOVE: run `/draft-linkedin` against idea #3 within the next 30 min while the angle is fresh." |

Full spec: [`cowork-social/skills/_shared/foundations.md`](./cowork-social/skills/_shared/foundations.md).

---

## The Cowork-not-Code rewrite

Blotato ships 5 free Claude Skills (`content-coach`, `brand-brief`, `post-writer`, `post-grader`, `post-scheduler`) — but they target **Claude Code** (filesystem-based, `~/.claude/skills/` folder placement). cowork-social targets **Claude Cowork** (ZIP upload via Customize → Skills, sandboxed filesystem, different runtime).

We did NOT wrap or recommend Blotato's versions. We rewrote them natively for Cowork's runtime, applied our 3 architectural foundations, and folded in cowork-ai-os identity integration. We also added 2 platforms Blotato doesn't cover (`/draft-twitter`, `/draft-threads`) and 3 native orchestrators (`/weekly-content-session`, `/generate-weekly-ideas`, `/content-engine-review`).

Result: 13 skills that work the moment cowork-social is installed. No second ZIP. No filesystem path debugging.

Full rationale: [`cowork-social/docs/architecture.md`](./cowork-social/docs/architecture.md).

---

## About Blotato (the scheduling MCP)

**cowork-social is built for Blotato.** We chose it because of our experience — it works best with everything else in the Cowork stack (direct local-file upload, 16 MCP tools, OAuth-friendly, up to 20 social accounts on one seat).

- **If you already have a Blotato account:** ignore the affiliate link below. Just OAuth-connect during the wizard's Phase 4.
- **If you're new to Blotato:** sign up at [blotato.com/?ref=nuno](https://blotato.com/?ref=nuno) and use code `NUNO30` at checkout for **30% off your first 3 months** ($29/mo → $20.30/mo).
- **If you don't want Blotato at all:** the wizard skips Phase 4 cleanly. Drafts still save to `outputs/social-media-content/` — you'll schedule manually inside each platform. About 80% of cowork-social's value retained.

### How to wire Blotato in Cowork (3 clicks)

1. Settings → Connectors → **Add Custom Connector**
2. Paste the Blotato MCP URL the wizard surfaces (live-verified namespace: `mcp__claude_ai_Blotato__*`)
3. Click **Connect** → approve OAuth in the browser → done

No JSON. No CLI. No API-key juggling. The wizard's Phase 4 walks you through it.

---

## ⚡ 1-minute install

```
/plugin marketplace add AutomatedMarketer/cowork-social
/plugin install cowork-social@cowork-social
/onboard-social
```

That's it. The wizard is resumable — stop any time, pick up where you left off.

---

## Dependencies

`cowork-social` is **standalone** but plays nice with the rest of the Cowork AI OS family:

- **Soft-depends on `cowork-ai-os >= 0.10`** — for identity files (`about-me/about-me.md`, `business-brain.md`, `connections.md`). The wizard halts cleanly with a paste-ready prompt if these are missing.
- **`cowork-ai-os >= 0.10.2` recommended** — Phase 2 of the wizard delegates to `/browse-connectors`, which v0.10.2 made live (fetches `claude.com/connectors` at runtime). Older versions still work via the bundled catalog.
- **Loose-couples with `cowork-research >= 0.2`** — both plugins share the Blotato MCP cleanly. If you've already wired Blotato for cowork-research, cowork-social detects it and skips Phase 4's OAuth step.
- **No vault required** — `cowork-obsidian` is not used by v0.1; drafts and outputs live in `projects/social-media-content/` and `outputs/social-media-content/`.

---

## How it works (no jargon)

When you run `/weekly-content-session` on a Monday morning:

1. The skill reads your `about-me/business-brain.md` to know your ICP, voice, and offer.
2. It reads `projects/social-media-content/brand-brief.md` for the content-specific deltas (voice samples, banned phrases, signature hooks).
3. It pulls the 10 ranked ideas `/generate-weekly-ideas` dropped on Saturday — sorted by virality score.
4. For each idea you pick, it calls the right `/draft-*` skill with platform-aware constraints (char limits, hashtag rules, line-break behavior).
5. Each draft auto-flows into `/grade-post` (hook = 50% weight). Below 70? You see the top 3 fixes before approving.
6. On approval, posts go to Blotato's queue via `mcp__claude_ai_Blotato__blotato_create_post` — or land in `outputs/social-media-content/` if you skipped Blotato.
7. The week's calendar log is appended to `projects/social-media-content/calendar-log.md`. The library compounds.

No MCP server required for the plugin itself — Cowork has filesystem access. Blotato is the only external MCP and you wire it once during Phase 4.

---

## Shipped in v0.1

- ✅ **13 skills** — wizard + brand-brief + content-coach + 6 platform draft skills + grade-post + 3 orchestrators
- ✅ **3 architectural foundations applied in every skill** — lazy-load, self-improving, ⚡ NEXT MOVE
- ✅ **Cowork-native rewrite of Blotato's 5 official Claude Skills** + 2 native additions (X, Threads) + 3 orchestrators
- ✅ **Blotato MCP live-verified** in default Cowork environment on 2026-05-15
- ✅ **8-phase resumable wizard** with state.md persistence
- ✅ **Shared 12-step draft-skill spec** as single source of truth for all 6 platform drafts
- ✅ **11 proven hook patterns** as a callable library
- ✅ **Headless variants** for `/generate-weekly-ideas` (NEXT MOVE in file footer for cron contexts)

## What's NOT in v0.1

Deferred to v0.2+ to keep this release focused:

- ❌ **`/create-visual`** — Blotato visual templates (carousels, infographics, quote cards) via `blotato_create_visual`. Coming once we've watched 20+ cohort users hit the visual-bottleneck.
- ❌ **`/remix-source`** — YouTube/podcast/PDF scraping via `blotato_create_source` for content remix.
- ❌ **Mid-week tune-up skill** — Wednesday refresh between Monday batch and weekend ideation.
- ❌ **Custom Blotato schedules per ICP segment** — different timings for different audience segments.
- ❌ **Multi-account / multi-brand support** — one brand per workspace in v0.1.
- ❌ **Bluesky, Pinterest, YouTube publishing** — Blotato supports them; we don't wire them in v0.1.
- ❌ **Engagement-data feedback loop** — `/grade-post` learning from `blotato_list_posts` published metrics.
- ❌ **Custom Cowork MCP server** — once we've watched 20+ users hit specific friction, we'll ship `social_draft`, `social_grade`, `calendar_log` as first-class MCP tools.

---

## Who this is for

- **Solo coaches** — weekly post rhythm tied to your methodology, without the Monday-blank-page
- **Agency owners** — your own content calendar running while you fulfill client work
- **Creators** — platform-specific drafts at scale; the visuals + scheduling stay one prompt away
- **Course creators** — 5 platforms covered + idea generation tied to your course wedge
- **Solopreneurs / SMB owners** — show up consistently without it owning your week
- **Sales-led B2B** — LinkedIn + X as the front door; calendar runs while you take calls

If you've ever sat down Monday morning, stared at the post box, and said "I'll do it tomorrow" — this is the alternative.

---

## Install

### Mac

## 🍎 ✅ Mac install (recommended): zip upload

> ### ⚠️ Already tried installing this plugin before? Read this first.
>
> Cowork has a known Mac quirk: **if you've previously uploaded a plugin with the same name (even a failed or stale attempt), the next upload is silently rejected** — no error toast, no log line, the new zip just doesn't replace the old one. This happens because Cowork sends `overwrite=false` on every upload and there's no UI affordance to override it.
>
> **Fix before you re-upload (30 seconds):**
> 1. 🗑️ Open Claude Cowork → **Settings → Customize → Plugins** (or **Skills**, depending on Cowork version)
> 2. Find any existing entry for `cowork-social` — including manually-repacked attempts or stale uploads
> 3. **Remove / delete it** (trash icon, "Uninstall", or "Remove")
> 4. 🔄 Quit Cowork fully → relaunch (clears the in-memory marketplace cache)
> 5. Proceed to the install steps below
>
> If this is your **first time** installing this plugin, skip this section.

This is the recommended install path for all Mac users. It bypasses Anthropic's open Cowork-on-macOS bugs (🚧 [#26951](https://github.com/anthropics/claude-code/issues/26951), 🚧 [#28125](https://github.com/anthropics/claude-code/issues/28125)) and works on every Cowork build that supports plugin uploads. Workaround confirmed by users in [#39400](https://github.com/anthropics/claude-code/issues/39400).

### ⏱️ 6 steps, ~30 seconds

1. **📦 Download** the latest **`cowork-social-v0.1.0.zip`** (or `cowork-social.zip`) from the [**Releases page → Assets**](https://github.com/AutomatedMarketer/cowork-social/releases/latest). **Don't extract it.** Keep the file as a single `.zip`.
   > ⚠️ **Important:** download the zip from the **Releases page**, NOT the green **❌ Download ZIP** button at the top of the repo page. That button wraps the repo in an outer folder (`cowork-social-main/`) which double-nests the plugin and breaks Cowork's validator.
2. **⚙️ Open Claude Cowork** (the middle tab in Claude Desktop) → click your name (top right) → **Settings**.
3. **🔌 Customize → Browse plugins** → look for the option to **upload a custom plugin file**.
   > 💡 Menu wording varies slightly between Cowork versions — look for "Upload", "Custom plugin", or "From file".
4. **📤 Drag in the zip.** Wait for confirmation.
5. **🚀 Open a brand new Cowork task** (skills load on session start, not retroactively).
6. Type `/onboard-social` and follow the wizard.

> 💡 **Why this is the recommended Mac path:** Anthropic closed [#27196](https://github.com/anthropics/claude-code/issues/27196) ("All Anthropic plugins fail in Cowork on macOS") as **not planned** — they don't currently intend to fix the marketplace path on Mac. The zip-upload path is effectively the supported install method on macOS going forward.

### 🐛 Troubleshooting

| Symptom | What to do |
|---|---|
| 🤐 Upload appears to succeed but plugin doesn't update / still showing old version | You have a stale entry from a previous upload attempt. Remove the old entry first (see the "Already tried installing" callout at the top of this section). Cowork silently rejects same-name re-uploads. |
| 🔍 Can't find "Upload" / "Custom plugin" option | Look for "From file" / "Local plugin" / "Add manually". If genuinely absent, your Cowork version is older than the upload feature — 🔄 quit, update Claude Desktop, relaunch. |
| 📄 Upload rejects the file | Confirm the file extension is `.zip` (not `.plugin`). Re-download directly from the [Releases page](https://github.com/AutomatedMarketer/cowork-social/releases/latest); don't rename. |
| 🚫 Plugin uploads but `/onboard-social` does nothing | Open a **brand new** Cowork task. Skills load on session start, not retroactively. |
| 👻 Plugin disappears after restart | That's 🚧 [#38429](https://github.com/anthropics/claude-code/issues/38429) — Anthropic-side persistence bug. 🔄 Re-upload the zip after restart. |

### Windows

<details>
<summary><b>Windows install (click to expand)</b></summary>

```
/plugin marketplace add AutomatedMarketer/cowork-social
/plugin install cowork-social@cowork-social
```

Then in a fresh Cowork task:

```
/onboard-social
```

</details>

### Linux

<details>
<summary><b>Linux install (click to expand)</b></summary>

Same as Windows:

```
/plugin marketplace add AutomatedMarketer/cowork-social
/plugin install cowork-social@cowork-social
/onboard-social
```

</details>

---

## What's next

- **v0.2** — visual generation pipeline. `/create-visual` (Blotato templates: carousels, infographics, quote cards, manga, whiteboard). `/remix-source` (YouTube/podcast scrape → platform posts + auto-visual).
- **v0.3** — engagement feedback loop. `/grade-post` learns from published metrics. Mid-week tune-up skill. Multi-account scheduling.
- **v0.4+** — custom Cowork MCP server. Once we've watched 20+ users hit specific friction, we ship `social_draft`, `social_grade`, `calendar_log` as first-class MCP tools.
- **Modular-plugin roadmap unchanged.** `cowork-ai-os` (identity) → `cowork-obsidian` (vault) → `cowork-research` → `cowork-social` (THIS) → `cowork-financial` (P&L + cashflow) → `cowork-highlevel` (GoHighLevel CRM ops). Each ships independently. None require the others, but they compose well when stacked.

---

## Coordination with the Cowork AI OS family

| Plugin | Role | Required? |
|---|---|---|
| **`cowork-ai-os`** | Identity + connector discovery + safe-zones | Soft-required (`>= 0.10`); v0.10.2+ recommended for live connector catalogs |
| **`cowork-obsidian`** | Vault as long-term memory | Not used by cowork-social v0.1 |
| **`cowork-research`** | Research engine — briefs, audits, recaps, clips | Loose-coupled (`>= 0.2`); shares Blotato MCP if both installed |
| **`cowork-social`** *(this one)* | Social content engine — ideas, drafts, grading, scheduling | — |
| **`cowork-financial`** *(future)* | P&L, cashflow, financial briefs | Out of scope for v0.1 |
| **`cowork-highlevel`** *(future)* | GoHighLevel CRM ops | Out of scope for v0.1 |

Cohort install order: `cowork-ai-os` first → `cowork-research` (if you want research) → `cowork-social` (this one).

---

## License

[MIT](./LICENSE) — yours forever.

## Built by

[Nuno Tavares](https://nunomtavares.com) — Newsletter: [automatedmarketer.net](https://automatedmarketer.net) · YouTube: [@AutomatedMarketer](https://youtube.com/@AutomatedMarketer)

## Credits

- **Sabrina Ramonov** — her [60-minute Cowork masterclass](https://youtu.be/-q_wgmmD0e0) is the framing source for the "Hour 1 / Hour 2 / close laptop" pattern this plugin operationalizes
- **VCInc cohort students** — the cohort whose weekly-content friction shaped which 13 skills shipped first
- **Blotato team** — for the 5 free Claude Skills we used as inspiration + reference for the Cowork-native rewrites
- **Karpathy's [LLM Wiki gist](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)** — the original "Obsidian is the IDE, the LLM is the programmer, the wiki is the codebase" framing carried over from sibling cowork plugins

## Links

- [Anthropic Claude Code docs](https://docs.claude.com/en/docs/claude-code)
- [`cowork-ai-os` plugin](https://github.com/AutomatedMarketer/cowork-ai-os) — identity + connector layer
- [`cowork-research` plugin](https://github.com/AutomatedMarketer/cowork-research) — research engine
- [Blotato (affiliate)](https://blotato.com/?ref=nuno) — multi-platform scheduling MCP; code `NUNO30` for 30% off 3 months
