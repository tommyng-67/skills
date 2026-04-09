# 1-3-1 Analysis

One problem. Three approaches. One recommendation. No hedging.

The constrained sibling of 1-5-X. Same analytical method - criteria-first, per-criterion assessment, mitigations factored into scoring - but scoped to exactly three options and a single winner. For decisions where three well-chosen paths and one decisive call is enough.

## How It Works

| Step | What happens |
|---|---|
| **Frame** | Same depth as 1-5-X: root cause separation, status quo baseline, core tension, success definition. |
| **Criteria** | 3-5 weighted criteria with concrete score anchors. Tighter than 1-5-X's 4-7. |
| **Three approaches** | Three genuinely distinct paths spanning the decision space - typically conservative, moderate, bold. Each scored per criterion with risks, mitigations, and second-order effects. |
| **Matrix** | 3-column summary table. |
| **One winner** | Single recommendation. Can be a hybrid of elements from the three. No hedging - pick one and commit. |

## Example Output (Abbreviated)

What the recommendation looks like:

> **Recommendation: Approach B (Moderate) with one element from C**
>
> Run the 4-week pilot with the existing vendor (B) but adopt C's success criteria - measure behavior change, not satisfaction scores. B wins on speed-to-learning (score: 4.1) and reversibility (score: 4.5). C's measurement framework is the strongest of the three but the implementation timeline kills it.
>
> **Why not A:** Conservative path avoids the risk but also avoids the data. You learn nothing in 90 days.
>
> **Why not C:** Right destination, wrong sequence. The 12-week build assumes requirements that the pilot will surface.
>
> **Next steps:** Vendor kickoff by Friday. Define the 3 behavioral metrics by EOD tomorrow. First checkpoint at day 14.

## When to Use

Use 1-3-1 when you say "1-3-1." That's the only trigger. Every other decision or comparison request goes to 1-5-X.

| Use 1-3-1 | Use 1-5-X instead | Use Deep Research instead |
|---|---|---|
| You want speed and a single call | Decision space is wide, need 5+ options | You need to understand the topic first |
| Three options is enough | Multiple recommendations or hybrid needed | "Research this", "what is X" |

## Output

**In chat:** The single recommended approach with rationale, risks, and next steps.

**File:** Full analysis saved as `.md` - problem frame, criteria, all three approaches with per-criterion scoring, decision matrix, and the recommendation.

## Install

Add `SKILL.md` to your platform's skill library.

## Part of the PM Decision Toolkit

- [1-5-X Analysis](../1-5-x-analysis) - Full decision analysis
- [1-3-1 Analysis](../1-3-1-analysis) - Fast decision: 3 options, 1 winner (this skill)
- [Deep Research](../deep-research) - Understand before deciding
