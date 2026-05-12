# RICE Scorecard — .xlsx Specification

Use openpyxl to generate this file. Follow the xlsx SKILL.md for all formatting rules.

---

## Workbook structure

Two sheets:
1. `Ranked Scorecard` (primary)
2. `Score Guide` (reference)

---

## Sheet 1: Ranked Scorecard

### Column layout

| Col | Header | Width | Notes |
|-----|--------|-------|-------|
| A | Rank | 8 | Integer, auto-assigned 1–N after sorting |
| B | Feature | 36 | Feature name — left-aligned, wrap text |
| C | Reach | 14 | Raw number (e.g., 2000) — comma formatted |
| D | Impact | 12 | 0.25 / 0.5 / 1 / 2 / 3 |
| E | Confidence | 14 | Percentage (e.g., 80%) |
| F | Effort | 12 | Person-months (e.g., 1.5) |
| G | RICE Score | 14 | Formula: =(C*D*E)/F — 1 decimal place |
| H | Bucket | 14 | "Now" / "Next" / "Later" |
| I | Flags | 20 | 🔴 Low Confidence / ⚡ Quick Win / 🎯 Strategic Bet — may be blank |

### Header row formatting
- Row 1: bold, white text, brand blue fill (`1A56DB`), 12pt Arial
- Freeze row 1 (freeze_panes = 'A2')

### Data rows
- Alternating row shading: white (#FFFFFF) and light gray (#F9FAFB)
- Bucket column color-coded:
  - "Now" → green fill `#DCFCE7`, dark green text `#166534`
  - "Next" → amber fill `#FEF9C3`, dark amber text `#713F12`
  - "Later" → light gray fill `#F3F4F6`, gray text `#6B7280`
- RICE Score column: bold, slightly larger (12pt)
- Flags column: left-aligned, 10pt, emoji-safe font

### RICE Score formula
Always use an Excel formula, not a hardcoded value:
```
=ROUND((C{row}*D{row}*(E{row}/100))/F{row},1)
```
Note: Confidence is stored as a decimal percentage (80% stored as 80, not 0.8) — divide by 100 in formula.

### Sorting
Sort rows by RICE Score descending before writing. Assign Rank after sorting.

### Summary row at bottom
Add a summary row after all features:
- Col A: "Total features: N"
- Col G: Average RICE score across all features (formula: `=AVERAGE(G2:G{last_row})`)
- Apply a top border to this row

---

## Sheet 2: Score Guide

A clean reference sheet explaining the RICE components. No interactivity needed — just well-formatted reference content.

### Layout
- Title: "RICE Scoring Reference" — bold, 14pt, brand blue
- One section per RICE component (Reach, Impact, Confidence, Effort)
- For Impact and Confidence: include the scale tables from rice-guide.md as formatted Excel tables
- Column widths: A=20, B=50

### Impact scale table
| Score | Label | When to use |
|-------|-------|-------------|
| 3 | Massive | Core to retention or revenue |
| 2 | High | Meaningfully improves experience |
| 1 | Medium | Useful but not a retention driver |
| 0.5 | Low | Nice to have |
| 0.25 | Minimal | Marginal polish |

### Confidence scale table
| Score | Label | Evidence level |
|-------|-------|----------------|
| 100% | High | Direct data (analytics, research, A/B test) |
| 80% | Good | Some evidence (interviews, proxy metrics) |
| 50% | Medium | Educated guess / anecdotal |
| 20–40% | Low | Hypothesis only — validate before building |
