---
name: feature-prioritization
description: "Score, rank, and prioritize a list of features or initiatives using the RICE framework (Reach, Impact, Confidence, Effort). Use this skill whenever a PM asks to prioritize a backlog, rank feature requests, decide what to build next, score a list of ideas, or figure out what to cut. Trigger even if the input is messy — brain dumps, copy-pasted backlog items, customer feedback themes, or a rough list of things to build all work. Produces two outputs: a ranked RICE scorecard (.xlsx) and a narrative prioritization brief (.docx) explaining the recommendations. Designed for PMs at growth-stage SaaS companies who need a defensible, fast prioritization they can share with eng and stakeholders."
---

# Feature Prioritization — RICE Framework

A skill for turning a messy list of feature ideas into a ranked, defensible prioritization with a scored spreadsheet and a narrative brief.

**Two outputs every time:**
1. **RICE Scorecard** (`.xlsx`) — ranked table with scores, per-component breakdowns, and Now/Next/Later bucket assignments
2. **Prioritization Brief** (`.docx`) — narrative explaining the top picks, what got deprioritized, confidence caveats, and strategic flags

---

## Phase 1: Normalize the Input

The PM's input will almost never be clean. It might be a bullet list, a pasted Jira backlog, customer feedback themes, or a brain dump in a paragraph. Your first job is to normalize it.

**Steps:**
1. Read the input and extract discrete, scoreable feature items. Each item should be one thing — not a bundle.
2. If an item is too vague to score (e.g., "improve performance"), flag it and ask one clarifying question: "What specifically — which surface, which metric, for which users?"
3. If an item is actually two features bundled together, split it and note the split.
4. Present the normalized list back to the PM before scoring: "Here's what I extracted — [X] items. Does this look right, or did I miss or conflate anything?"

Don't score until the PM confirms the list (or says "looks good, keep going").

---

## Phase 2: Score Each Feature via RICE Interview

Walk the PM through scoring each feature. The goal is honest scores grounded in evidence — not inflated guesses.

### The RICE formula
```
RICE Score = (Reach × Impact × Confidence) / Effort
```

### Scoring guide (read `references/rice-guide.md` for full detail)

| Component | What to ask | Scale |
|-----------|-------------|-------|
| **Reach** | "How many users/customers would this affect per quarter?" | Raw number (e.g., 2,000 users) |
| **Impact** | "How much does this move the needle for each affected user?" | 3 = massive / 2 = high / 1 = medium / 0.5 = low / 0.25 = minimal |
| **Confidence** | "How sure are you about Reach and Impact?" | % (100 = hard data, 80 = some evidence, 50 = gut feel) |
| **Effort** | "How many person-months to design, build, and ship?" | Person-months (round up — features always take longer) |

### Interview principles

- **Don't accept round numbers without asking why.** "100% confidence" and "Impact: 3" on every feature is a red flag. Push back: "What's the evidence for a massive impact here? Is this based on user research, or a hypothesis?"
- **Effort is almost always underestimated.** If a feature sounds complex, ask: "Does that include design, QA, and any backend work? I'd suggest adding 20–30% buffer."
- **Reach must be consistent.** Make sure all features use the same timeframe (per quarter is the default). Don't mix quarterly and annual numbers.
- **Low confidence is information, not a problem.** A 50% confidence score is honest — it means the feature needs validation before committing. Flag these items explicitly in the output.

### Interview format

For shorter lists (≤8 features): walk through each feature one by one, asking all four RICE components per feature before moving to the next.

For longer lists (>8 features): ask the PM to provide rough estimates for all features first, then do a focused review pass on any outliers or high-stakes items.

If the PM is in a hurry or already has estimates, accept their numbers and proceed — but add confidence caveats to the output where scores look inflated or unsupported.

---

## Phase 3: Compute, Rank, and Bucket

Once all scores are in:

1. Compute RICE scores: `(Reach × Impact × Confidence) / Effort`
2. Rank features highest to lowest
3. Assign to one of three buckets based on score distribution and strategic context:
   - **Now** — top ~30% by score, and/or clearly aligned to current OKRs
   - **Next** — middle tier, worth doing but not yet
   - **Later / Revisit** — low score, low confidence, or explicitly out of current scope
4. Flag any features that deserve a special callout:
   - **🔴 Low confidence** — score ≥ medium but confidence ≤ 50%. Needs validation before committing.
   - **⚡ Quick win** — low effort (≤ 0.5 person-months), decent score. Candidates for filling sprint gaps.
   - **🎯 Strategic bet** — low current Reach but high potential Impact; may warrant investment despite lower RICE score.

---

## Phase 4: Generate Outputs

Read the relevant skill files before generating each output:
- For `.xlsx`: read `/mnt/skills/public/xlsx/SKILL.md`
- For `.docx`: read `/mnt/skills/public/docx/SKILL.md`

### Output 1: RICE Scorecard (.xlsx)

Use openpyxl. See `references/scorecard-spec.md` for the exact layout and formatting spec.

Two sheets:
- **Ranked Scorecard** — all features, sorted by RICE score, with columns: Rank, Feature, Reach, Impact, Confidence, Effort, RICE Score, Bucket, Flags
- **Score Guide** — a reference tab explaining the RICE components and scoring scales

### Output 2: Prioritization Brief (.docx)

See `references/brief-template.md` for the full structure.

Sections:
1. **Summary** — 3–4 sentences: what was prioritized, the key signals driving the top picks, and the most important trade-off made.
2. **Top Picks (Now)** — for each Now-bucket feature: what it is, why it ranked high, and one sentence on the expected outcome.
3. **Next Quarter** — brief rationale for the Next bucket. What would need to change to move these up?
4. **Parked / Later** — what got deprioritized and why. Be specific — "low reach" is more useful than "low score."
5. **Confidence Caveats** — any features with ≤ 50% confidence that are still in the Now bucket. What validation is needed before committing?
6. **Strategic Flags** — quick wins and strategic bets that didn't make the top score but deserve attention.

---

## Phase 5: Review Loop

After delivering both outputs:
1. Ask: "Does this ranking feel right? Any features that seem under- or over-ranked given context I don't have?"
2. If the PM disagrees with a ranking, explore whether it's a scoring issue (wrong inputs) or a strategic override (the RICE score is right, but there's a business reason to rank it differently). Document overrides explicitly in the brief.
3. Revise and re-output if needed.

---

## Reference Files

- `references/rice-guide.md` — Full RICE scoring guide with examples and common pitfalls
- `references/scorecard-spec.md` — Exact layout, column widths, and formatting for the .xlsx output
- `references/brief-template.md` — Full narrative brief template
