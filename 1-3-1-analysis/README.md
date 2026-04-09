# 1-3-1 Analysis

Constrained decision-making: **1** precisely framed problem → weighted evaluation criteria → exactly **3** approaches → **1** recommendation. The faster sibling of 1-5-X.

## Why This Exists

Not every decision warrants a full 1-5-X. Sometimes three well-chosen options and one decisive call is enough. The 1-3-1 delivers the same analytical rigor — criteria-first, per-criterion assessment, mitigations factored into scoring — but in a tighter package with a single clear winner.

## How It Works

| Step | What happens |
|---|---|
| **Frame the Problem** | Same depth as 1-5-X: root cause separation, status quo baseline, core tension, success definition, hidden decisions. |
| **Define Criteria** | 3–5 weighted criteria (tighter than 1-5-X's 4–7). Concrete score anchors to prevent inflation. |
| **Generate & Assess Exactly 3 Approaches** | Three genuinely distinct paths spanning the decision space (e.g., conservative / moderate / bold). Each assessed per criterion with scores, risks, mitigations, and second-order effects. |
| **Decision Matrix** | 3-column summary table. |
| **Recommend Exactly 1** | Single winner. Can be a hybrid combining elements from multiple approaches. No hedging — pick one. |

## Output

**In chat:** The single recommended approach with rationale, risks, and next steps.

**File:** Full analysis (problem frame, criteria, all 3 approaches with per-criterion assessment, decision matrix, recommendation) saved as `.md`.

## When to Use

| Use **1-3-1** | Use **1-5-X** instead | Use **Deep Research** instead |
|---|---|---|
| User explicitly says "1-3-1" | Any other decision or comparison | User wants to understand a topic, not decide |
| Faster, lighter-weight decision | Complex decisions needing 5+ options | "Research this", "what is X", "deep dive" |
| 3 options and 1 winner is sufficient | Multiple recommendations or hybrid needed | Findings and insights, not ranked approaches |

**Trigger:** Only activates when you explicitly say "1-3-1". All other decision requests default to 1-5-X.

## Install

Download `1-3-1-analysis.skill` and add it to your project's skill library.

## Part of the PM Decision Toolkit

Three skills that work together:

- **[1-5-X Analysis](../1-5-x-analysis)** — Exhaustive decision analysis
- **[1-3-1 Analysis](../1-3-1-analysis)** — Fast decision: 3 options, 1 winner (this skill)
- **[Deep Research](../deep-research)** — Understand a topic before deciding
