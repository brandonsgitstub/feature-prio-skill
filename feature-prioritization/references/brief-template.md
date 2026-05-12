# Prioritization Brief — Template

Use this as the structural guide for the `.docx` narrative output. Read `/mnt/skills/public/docx/SKILL.md` before generating. Adapt depth to the size of the feature list — a 5-feature list doesn't need the same brief as a 20-feature backlog.

---

## [Product Area or Team Name] — Feature Prioritization Brief
**Framework:** RICE (Reach × Impact × Confidence / Effort)
**Scored:** [Date]
**Prepared by:** [PM Name — TBD]
**Features evaluated:** [N]
**Quarter:** [Q — TBD]

---

## 1. Summary

*3–4 sentences. Cover: how many features were evaluated, what the top signal driving the rankings was, and the single most important trade-off or tension in the prioritization. Write for a stakeholder who won't read the rest of the doc.*

Example:
> We scored 12 features across the growth and retention surface. The top picks are driven by high Reach among our active daily cohort and evidence from Q3 user interviews that friction in the onboarding flow is the primary driver of 14-day churn. The main trade-off: three high-Impact platform features scored low due to significant Effort, and are parked until H2 when eng capacity opens up.

---

## 2. Now — Build This Quarter

*For each feature in the Now bucket, write 2–4 sentences: what it is, why it ranked high (which RICE components were strongest), and the expected outcome. Don't just restate the score.*

### [Feature Name] — RICE Score: [X]
[Description of what the feature is and who it's for.]
[Why it ranked high — specific signal: "Reach of 3,400 users/quarter driven by high activity in the dashboard surface" or "80% confidence based on 8 user interviews in Q3."]
[Expected outcome: "Expected to reduce 7-day activation drop-off by reducing time-to-first-value for new users."]

*Repeat for each Now-bucket feature.*

---

## 3. Next Quarter

*Brief rationale for the Next bucket as a group, then 1–2 sentences per feature on what would need to change to move it up.*

These features scored well but are blocked by [capacity / confidence / dependencies / strategic timing].

**[Feature Name]** — Scored [X]. [What would move it to Now: "Moves up when eng capacity opens in Q3" or "Moves up if discovery interviews confirm the Reach estimate."]

*Repeat briefly for each Next-bucket feature.*

---

## 4. Parked — Not This Half

*What got deprioritized and the specific reason. Be concrete — "low Reach" is more useful than "low score."*

| Feature | RICE Score | Primary reason parked |
|---------|------------|----------------------|
| [Name] | [X] | Low Reach: only affects [N] users/quarter |
| [Name] | [X] | High Effort: [N] person-months for low impact |
| [Name] | [X] | Low Confidence: hypothesis only — needs validation |

---

## 5. Confidence Caveats

*Surface any Now-bucket features where Confidence was ≤ 50%. These are features we're recommending to build despite uncertainty — flag what validation is needed.*

**[Feature Name]** — Confidence: [X]%. 
[What we don't know: "Reach estimate of 2,000 users is based on proxy data from a related feature — actual affected users may be lower."]
[Recommended validation: "Run 5 discovery sessions with [user segment] to confirm Reach and Impact before committing to a sprint."]

*If no Now-bucket features have low confidence, note: "All top-priority features have ≥ 80% confidence. No validation flags."*

---

## 6. Strategic Flags

*Quick wins and strategic bets that didn't make the top score but deserve explicit attention.*

### ⚡ Quick Wins
Features with Effort ≤ 0.5 person-months that scored reasonably well. Good candidates for filling sprint gaps or shipping alongside larger initiatives.

| Feature | RICE Score | Effort | Why it's a quick win |
|---------|------------|--------|----------------------|
| [Name] | [X] | [X] months | [Reason] |

### 🎯 Strategic Bets
Features with lower current Reach but high potential Impact or strategic importance. These may warrant building even if the RICE score is modest.

**[Feature Name]** — [Why it's a strategic bet despite a lower score: "Low current Reach because the user segment is small today, but this is a key ICP for the H2 enterprise motion."]

*If no quick wins or strategic bets exist, omit this section.*

---

## 7. Score Assumptions

*List any RICE component estimates that were assumed rather than data-backed. Mirror the [ASSUMED] items from the scoring session.*

- **[Feature] — Reach:** Estimated [N] users/quarter. [Source or assumption: "Based on analytics showing X sessions/month on the affected surface."]
- **[Feature] — Impact:** Scored [X]. [Basis: "Based on 3 user interviews, not a full research study."]

*If all scores were provided directly by the PM with stated evidence, note: "All scores were provided by [PM] based on [stated evidence]. No additional assumptions made."*
