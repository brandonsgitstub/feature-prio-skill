# RICE Scoring Guide

## What is RICE?

RICE is a prioritization framework that produces a numerical score for each feature, making it easier to rank and compare items consistently. It was developed by Intercom and is widely used by growth-stage PMs because it's fast, transparent, and forces honest thinking about scope and confidence.

**Formula:**
```
RICE Score = (Reach × Impact × Confidence) / Effort
```

Higher score = higher priority.

---

## Component Breakdown

### Reach — How many people does this affect?

**Definition:** The number of customers or users this feature will impact over a set time period. Default to per quarter unless the PM specifies otherwise. Keep this unit consistent across all features being scored.

**How to get it:**
- Use actual data where possible: DAU/MAU, segment size, support ticket volume, survey respondents
- If estimating, be conservative — it's better to underestimate and be pleasantly surprised
- "All users" is not a Reach number. Get specific: how many users actually encounter this surface?

**Examples:**
- "This affects users who use the reporting tab" → check analytics for monthly reporting tab sessions
- "This is for enterprise accounts only" → how many enterprise accounts do you have?
- "This is for new users in onboarding" → how many new signups per quarter?

**Common mistake:** Confusing total user base with affected users. A feature in a rarely-used settings menu does not have a Reach of 10,000 even if you have 10,000 users.

---

### Impact — How much does it move the needle per user?

**Definition:** A multiplier representing the depth of impact on each individual user who experiences the feature. This is qualitative, so use the standard scale:

| Score | Label | What it means |
|-------|-------|---------------|
| 3 | Massive | Core to why users stay or churn; directly drives the primary value metric |
| 2 | High | Meaningfully improves the experience; users would notice if it disappeared |
| 1 | Medium | Useful improvement; adds value but not a retention driver |
| 0.5 | Low | Nice to have; users probably wouldn't miss it |
| 0.25 | Minimal | Marginal polish; very few users would notice |

**How to calibrate:**
- Ask: "If we never built this, what's the worst-case outcome for a user?" 
- Ask: "Is this in a user's critical path, or is it a side path?"
- Cross-check against support tickets, NPS verbatims, and churn interviews — these are the most reliable signals for Impact scores

**Common mistake:** Giving every feature an Impact of 2 or 3. If everything is high-impact, the framework loses its value. Reserve 3 for features that are genuinely tied to retention or revenue.

---

### Confidence — How sure are you?

**Definition:** A percentage expressing how confident you are in your Reach and Impact estimates. This is the most important component for avoiding overcommitment.

| Score | Label | What it means |
|-------|-------|---------------|
| 100% | High | You have direct data: analytics, user research, A/B test results |
| 80% | Good | You have some evidence: a few user interviews, proxy metrics, prior similar features |
| 50% | Medium | Mostly gut feel or anecdotal signals; you're making an educated guess |
| 20–40% | Low | Very uncertain; this is a hypothesis that needs validation before building |

**How to use it:**
- Confidence is a penalty. A feature with great Reach and Impact but 50% confidence scores half of what it would at 100%.
- Low confidence is not a reason to deprioritize — it's a signal to validate first. Add a note: "Run a 5-user discovery session to get this to 80% confidence before committing."
- Never give 100% confidence unless you have actual data to back it.

**Common mistake:** Inflating confidence to preserve a high score. If you're guessing, say 50%.

---

### Effort — How much work is this?

**Definition:** The total person-months required to design, build, and ship the feature. Include all roles: product design time, engineering, QA, and any data/infrastructure work.

**How to estimate:**
- Use actual sprint velocity and team size where possible
- If you haven't done technical scoping, add a 20–30% buffer to whatever your instinct says
- Break complex features into component estimates if it helps (e.g., "backend: 1 month, frontend: 0.5 months, design: 0.5 months = 2 person-months total")

**Scale:**
| Score | Effort |
|-------|--------|
| 0.25 | A few days — no design, minimal eng |
| 0.5 | ~2 weeks — small scope, clean implementation |
| 1 | ~1 month — typical single-feature build |
| 2 | ~2 months — meaningful scope, some complexity |
| 3+ | Quarter-scale project — multi-team, significant architecture |

**Common mistake:** Only counting engineering time and forgetting design, QA, and product iteration cycles.

---

## Interpreting RICE Scores

RICE scores are only meaningful relative to each other — the absolute number doesn't matter, only the ranking. Don't read into "a score of 120 is good" — what matters is that it's higher than the score of 80 below it.

**Score distribution:** In a healthy prioritization, you'll typically see a power-law-like distribution — a few features with very high scores, and many with low scores. If all features cluster in a tight range, your Reach or Impact estimates are probably too uniform.

**Overriding the model:** RICE is a decision-support tool, not a decision-maker. It's valid to override a RICE ranking if:
- A feature has strategic importance that isn't captured in near-term Reach (e.g., it unlocks a new market)
- There's a contractual or regulatory commitment driving prioritization
- Leadership has explicitly deprioritized a feature regardless of score

Document overrides explicitly — "we're building X despite a lower RICE score because [reason]."

---

## Common RICE Mistakes to Avoid

1. **Inconsistent time period for Reach** — mixing quarterly and annual numbers kills the comparison
2. **Effort only = engineering time** — always include design + QA
3. **100% confidence on everything** — if you have data on everything, you don't need RICE
4. **Using RICE to justify decisions already made** — if you're reverse-engineering scores to get the outcome you want, the framework isn't helping you
5. **Forgetting that low-effort items punch above their weight** — a small Reach + medium Impact feature can outscore a large Reach + high Effort feature if Effort is 0.25 vs. 3
