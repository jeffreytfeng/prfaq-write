# prfaq-write

A Claude Code plugin that drafts and critiques Mapbox PRFAQs. Draft any section — Introduction, Press Release, External FAQ, Internal FAQ, or any sub-section — then run a critique pass that flags unsupported claims, logical gaps, and weak persuasive arguments before the doc goes to review.

Built for Mapbox PMs. Bakes Mapbox writing style, the 4-part Working Backwards structure, the approval-readiness checklist, and the Legal-before-coding rule into every draft.

## What it does

**Draft mode** — Run `/prfaq-write <section> <product-or-topic>` against any in-progress PRFAQ. The skill:

1. Reads your existing PRFAQ draft (if any) plus optional context files in the project (see below).
2. Drafts the requested section against the Mapbox PRFAQ standard:
   - **Introduction** — Cherie ask in one sentence, pre-readers, launch size (Large/Medium/Small), price, business metric being moved.
   - **Press Release** — 6 paragraphs in strict order (announcement → customer problem → workaround → what we're launching → customer voice + traction → wrap), with embedded leader quote and customer quote.
   - **External FAQ** — 8 required questions in order, first-person customer voice, present tense, plain language. Pricing answer is specific (free is a defended decision).
   - **Internal FAQ** — 13 required questions in order, including the synthetic customer quote (Q13) that populates ¶5 of the press release.
   - **Headline / problem / solution / leader quote / customer quote / user journey** — any individual PR sub-section on its own.
3. Applies Mapbox writing style — no "utilize," no "leverage," no "users" for customers, no pejorative "you," no possessive "Mapbox's," no competitor names in external sections, Oxford comma, sentence casing, active voice.
4. Runs a final pass against a structured review checklist covering structure, voice, and approval-readiness (3-month lead time, Legal review, Cherie + Anu invite).

**Critique mode** — Run `/prfaq-write critique` (or paste a draft and ask it to critique). The skill reads the full or partial PRFAQ and flags weaknesses across six dimensions:

- **Unsupported claims** — assertions a reviewer could challenge with "how do you know that?" that have no data, quote, or citation behind them.
- **Logical gaps** — problem/solution mismatches, "why now" statements without a forcing function, dependencies listed without confirmation from the dependent team.
- **Vague language** — TBDs, directional-but-unmeasurable outcomes ("improve," "accelerate"), and "we're exploring" placeholders that mask unresolved decisions.
- **Weak problem framing** — inconvenience described as pain, no named persona or vertical, no evidence the problem is real and material.
- **Solution not earning the WOW** — feature-list writing instead of customer outcomes, generic quotes, implicit before/after contrast.
- **Internal consistency** — conflicts between the Introduction's business metric and the I-FAQ adoption goal, timeline contradictions, scope claimed in one place and limited in another.

Output is a table with section reference, severity (🔴 blocks approval / 🟡 generates questions), one-line issue, and one-line fix — plus the top three gaps and an overall assessment. After drafting any full section, the skill automatically appends a critique block so you see the weaknesses before you share.

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

Section keywords: `intro` · `pr` · `efaq` · `ifaq` · `headline` · `problem` · `solution` · `quote` · `journey` · `critique`.

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

PRFAQ reviews stall on the same things every time: a fuzzy Cherie ask, a launch-size score nobody agreed on, a press release that buries the WOW moment, an E-FAQ that ducks pricing, an I-FAQ with no adoption goal, a missing synthetic customer quote, a competitor name that should never have been in the external sections. This skill bakes the Mapbox PRFAQ standard's checks into every draft — and the critique pass catches unsupported claims and weak arguments before a reviewer does.

## License

MIT — see [LICENSE](LICENSE).
