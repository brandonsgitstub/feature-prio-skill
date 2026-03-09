# Feature Prioritization (RICE) — Claude Skill

A Claude skill for turning a messy backlog into a ranked, defensible prioritization. Give it a list of features, customer requests, or raw ideas — it walks you through RICE scoring, then produces two outputs: a ranked scorecard (`.xlsx`) and a narrative brief (`.docx`) you can share with engineering and stakeholders.

---

## What It Does

Takes any input (bullet list, Jira export, brain dump, customer feedback themes) and:

1. **Normalizes the list** — extracts discrete, scoreable items, splits bundled features, flags anything too vague to score
2. **Walks you through RICE scoring** — asks for Reach, Impact, Confidence, and Effort per feature; pushes back on inflated estimates
3. **Ranks and buckets** — Now / Next / Later, with special flags for quick wins, strategic bets, and low-confidence items
4. **Produces two outputs** — a ranked `.xlsx` scorecard and a narrative `.docx` brief explaining the recommendations

---

## How to Use It

### 1. Add the skill to Claude

Upload `SKILL.md` to your Claude project.

### 2. What to tell Claude

**Minimal input:**
```
Here's our Q2 backlog — can you help us prioritize it?
- In-app notifications
- CSV export
- Bulk user import
- SSO support
- Custom report builder
- API rate limit dashboard
```

**Richer input (gets you better scores):**
```
I need to prioritize these 6 features for our Q2 planning. 
We have about 2 engineers for the quarter. Our main OKR is 
reducing time-to-value for new accounts. [list features]
```

Claude normalizes your list and confirms it before scoring begins. If an item is too vague ("improve performance"), it asks one clarifying question.

---

## RICE Scoring

```
RICE Score = (Reach × Impact × Confidence) / Effort
```

| Component | What it measures | Scale |
|---|---|---|
| **Reach** | Users/customers affected per quarter | Raw number (e.g., 2,000) |
| **Impact** | How much it moves the needle per user | 3 = massive / 2 = high / 1 = medium / 0.5 = low / 0.25 = minimal |
| **Confidence** | How sure you are about Reach and Impact | % (100 = hard data, 80 = some evidence, 50 = gut feel) |
| **Effort** | Design + build + ship in person-months | Person-months (round up) |

Claude pushes back on inflated numbers. "100% confidence" across every feature is a red flag. "Impact: 3" on everything means nothing is actually high-impact.

---

## What You Get

### Output 1: RICE Scorecard (`.xlsx`)

Two sheets:
- **Ranked Scorecard** — all features sorted by RICE score, with columns for each component, bucket assignment (Now/Next/Later), and flags
- **Score Guide** — reference tab explaining the RICE components and scales

Special flags in the scorecard:
- 🔴 **Low confidence** — decent score but ≤ 50% confidence; needs validation before committing
- ⚡ **Quick win** — low effort (≤ 0.5 person-months) with a solid score; good for sprint gap-filling
- 🎯 **Strategic bet** — low current Reach but high potential Impact; may warrant investment despite lower RICE score

---

### Output 2: Prioritization Brief (`.docx`)

| Section | What's in it |
|---|---|
| **Summary** | What was prioritized, key signals, most important trade-off |
| **Top Picks (Now)** | Each Now-bucket feature: what it is, why it ranked, expected outcome |
| **Next Quarter** | Rationale for Next bucket; what would need to change to move these up |
| **Parked / Later** | What got deprioritized and specifically why ("low reach" > "low score") |
| **Confidence Caveats** | Now-bucket items with ≤ 50% confidence and what validation is needed |
| **Strategic Flags** | Quick wins and strategic bets that deserve attention despite lower RICE |

---

## Example Output (excerpt)

**Scorecard (top 3 rows):**

| Rank | Feature | Reach | Impact | Confidence | Effort | RICE Score | Bucket | Flags |
|---|---|---|---|---|---|---|---|---|
| 1 | SSO support | 1,800 | 2 | 80% | 1.5 | 1,920 | Now | 🎯 Strategic bet |
| 2 | Bulk user import | 2,400 | 1 | 90% | 0.5 | 4,320 | Now | ⚡ Quick win |
| 3 | In-app notifications | 3,000 | 1 | 70% | 2.0 | 1,050 | Next | — |

---

**Brief (Top Picks excerpt):**

> **Bulk User Import — RICE: 4,320**
> Ranks first by score. High reach (2,400 users/quarter), strong confidence based on 12 CS tickets in Q1, and low effort at 0.5 person-months. This is a quick win with immediate impact on onboarding completion rates for companies with 10+ seats — which is exactly the segment we're targeting in Q2.
>
> **SSO Support — RICE: 1,920**
> Lower raw score but flagged as a strategic bet. Reach is currently limited to 1,800 users, but SSO is a hard blocker for enterprise deals that are stalled in our pipeline. CS has flagged 4 accounts representing ~$180K ARR that are waiting on this. The RICE score undersells the business impact.

---

## File Structure

```
feature-prioritization/
├── SKILL.md                      # The Claude skill — upload this to your project
└── references/
    ├── rice-guide.md             # Full RICE scoring guide with examples and common pitfalls
    ├── scorecard-spec.md         # Exact layout and formatting spec for the .xlsx output
    └── brief-template.md         # Full narrative brief template
```

---

## Design Notes

The RICE framework is well-known but commonly misused. Two failure modes this skill is designed to prevent:

1. **Score inflation.** When every feature gets a 3 for impact and 100% confidence, the ranking is meaningless. The skill is calibrated to challenge round numbers and ask for the evidence behind high scores.

2. **Forgetting that RICE is a starting point, not a verdict.** The brief includes a section specifically for strategic overrides — cases where the RICE score is accurate but a business reason justifies a different decision. Those overrides are documented explicitly rather than silently baked into the ranking.

The two-output format (scorecard + brief) is intentional. The scorecard is for the PM and engineering lead. The brief is for stakeholders who want the narrative, not the numbers. Different audiences, same prioritization.
