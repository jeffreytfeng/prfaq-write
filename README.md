# prfaq-write

A Claude Code plugin that drafts a single section of a Mapbox PRFAQ — Introduction, Press Release, External FAQ, Internal FAQ, or any of their sub-sections (headline, problem, solution, leader/customer quote, user journey) — following the Mapbox PRFAQ standard.

Built for Mapbox PMs. Bakes Mapbox writing style, the 4-part Working Backwards structure, the Cherie + Anu approval gates, and the Legal-before-coding rule into every draft.

## What it does

Run `/prfaq-write <section> <product-or-topic>` against any in-progress PRFAQ. The skill:

1. Reads your existing PRFAQ draft (if any) plus optional context files in the project (see below).
2. Drafts the requested section against the Mapbox PRFAQ standard:
   - **Introduction** — Cherie ask in one sentence, pre-readers, launch size (Large/Medium/Small), price, business metric being moved.
   - **Press Release** — 6 paragraphs in strict order (announcement → customer problem → workaround → what we're launching → customer voice + traction → wrap), with embedded leader quote and customer quote.
   - **External FAQ** — 8 required questions in order, first-person customer voice, present tense, plain language. Pricing answer is specific (free is a defended decision).
   - **Internal FAQ** — 13 required questions in order, including the synthetic customer quote (Q13) that populates ¶5 of the press release.
   - **Headline / problem / solution / leader quote / customer quote / user journey** — any individual PR sub-section on its own.
3. Applies Mapbox writing style — no "utilize," no "leverage," no "users" for customers, no pejorative "you," no possessive "Mapbox's," no competitor names in external sections, Oxford comma, sentence casing, active voice.
4. Runs a final pass against a structured review checklist covering structure, voice, approval-readiness (3-month lead time, Legal review with Laurel Finch, Cherie + Anu invite).

## Install

```
/plugin marketplace add jeffreytfeng/prfaq-write
/plugin install prfaq-write@prfaq-write
```

## Use

```
/prfaq-write pr "Modular Maps SDK"
/prfaq-write efaq path/to/prfaq-draft.md
/prfaq-write intro
/prfaq-write
```

Section keywords: `intro` · `pr` · `efaq` · `ifaq` · `headline` · `problem` · `solution` · `quote` · `journey`.

With no args, the skill prompts you for the section and the product.

## What ships in this repo

```
prfaq-write/
├── .claude-plugin/
│   └── marketplace.json      # makes this repo installable as a single-plugin marketplace
├── plugin/
│   ├── .claude-plugin/
│   │   └── plugin.json       # plugin manifest
│   └── skills/
│       └── prfaq-write/
│           ├── SKILL.md          # the skill definition
│           └── prfaq-template.md # bundled default Mapbox PRFAQ template
├── README.md
└── LICENSE
```

The skill is **self-contained** — it works against any project layout. If the project has these files, the skill picks them up automatically for richer context:

| Optional file | What the skill does with it |
|---|---|
| `Templates/prfaq.md` | Used as the template instead of the bundled `prfaq-template.md` (your house style wins). |
| `Knowledge/Context/goals.md` (or `goals.md`, `OKRs.md`) | Aligns the Introduction's business-metric framing and the I-FAQ goal-alignment answer to current goals. |
| `Knowledge/People/Cherie Wong.md`, `Knowledge/People/Anu Sharma.md` | Reflects known priorities of the approvers in the framing. |
| `Tasks/active.md` | Picks up any in-progress PRFAQ work and recent decisions. |
| `Knowledge/Context/my-voice.md` | Applies your tone and formatting preferences to the draft. |
| Google Drive MCP tools | If available, searches for relevant meeting notes, research, or existing PRFAQ drafts. |

None of these are required. Without them the skill uses the bundled template, neutral PM voice, and the inline Mapbox style rules.

## Mapbox PRFAQ — quick refresher

The PRFAQ is rooted in Amazon's [Working Backwards](https://www.amazon.com/Working-Backwards-Insights-Stories-Secrets/dp/1250267595) methodology: write the customer experience first, then build. A Mapbox PRFAQ is **6 pages max** with four parts in this order:

1. **Introduction** — Mapbox-specific framing for the review meeting (Cherie ask, launch size, business metric).
2. **Press Release** — 6 paragraphs, present tense, as if the product has already launched.
3. **External FAQ** — customer-facing, more total content than the I-FAQ, ships on the product page.
4. **Internal FAQ** — strategic, financial, and technical questions for leadership.

The PRFAQ is reviewed at least **3 months before launch**. Approval comes from Cherie Wong (CTO/SVP) and Anu Sharma (GM). Legal review (Laurel Finch) happens at the PRFAQ stage, before coding starts. The PRFAQ is a living document — keep updating it through preview.

The test: if the PR isn't compelling enough that you'd genuinely want to use the product, redesign the product — not the PR.

## Why use this

PRFAQ reviews stall on the same things every time: a fuzzy Cherie ask, a launch-size score nobody agreed on, a press release that buries the WOW moment, an E-FAQ that ducks pricing, an I-FAQ with no adoption goal, a missing synthetic customer quote, a competitor name that should never have been in the external sections. This skill bakes the Mapbox PRFAQ standard's checks into the draft, so reviewers don't have to.

## License

MIT — see [LICENSE](LICENSE).
