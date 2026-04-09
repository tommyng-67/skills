# 1-5-X Analysis

The exhaustive version of [1-3-1](../1-3-1-analysis/). Same methodology, wider aperture: **1** precisely framed problem → weighted evaluation criteria → **5+** approaches assessed per criterion → **X** recommendations (often a hybrid combining the strongest elements across approaches).

Use this when the decision is complex enough that three options can't span the full space — multiple stakeholders, competing priorities, high irreversibility, or ambiguous trade-offs that require more approaches to surface the right path.

## When to Use

| Use **1-5-X** | Use **1-3-1** instead |
|---|---|
| Complex decisions with many viable paths | Decisions where 3 options span the space |
| Multiple stakeholders with competing priorities | Clear problem, faster turnaround needed |
| Need multiple recommendations or phased approach | Need exactly 1 decisive recommendation |
| High-stakes, irreversible decisions | Two-way-door decisions |

**Trigger phrases:** "1-5-X", "help me decide", "compare options", "should we X or Y", "what would you recommend", "pros and cons", "what's the best approach"

This skill is the default for any decision or comparison request. 1-3-1 triggers only when the user explicitly asks for it.

## What's Different from 1-3-1

| | 1-3-1 | 1-5-X |
|---|---|---|
| Approaches | Exactly 3 | 5+ (including unconventional paths) |
| Criteria | 3–5 | 4–7 (more dimensions assessed) |
| Recommendations | 1 | Top 3 ranked (conditional, phased, or hybrid) |
| Problem framing | Root cause + core tension | Adds: hidden decision surfacing, irreversibility assessment, dependency mapping |
| Risk analysis | Probability × impact | Adds: reversibility assessment, residual risk after mitigation, second-order effects |
| Best for | Clear decisions, time-constrained | Complex decisions, multiple stakeholders, high stakes |

## How It Works

### Step 1: Frame the Problem
Everything from 1-3-1's framing, plus:

- **Irreversibility assessment** — one-way door (hard to reverse, demands rigorous analysis) vs. two-way door (easily reversed, favors speed). Directly affects risk tolerance in the recommendation.
- **Dependency mapping** — what upstream decisions does this depend on? What downstream decisions does this unlock or block?
- **Hidden decision surfacing** — "should we enter market X?" might really be asking "are we a single-product company or a platform?"

### Step 2: Define Evaluation Criteria
4–7 weighted criteria with concrete 1/5 score anchors. The core tension produces at least one criterion on each side (speed vs. quality → criterion for delivery timeline AND criterion for output quality). Irreversibility influences weights — high-irreversibility decisions weight risk-related criteria more heavily.

### Step 3: Generate & Assess 5+ Approaches
Each approach is a genuinely distinct strategic path — not parameter tweaks. Must include at least one conservative path, one aggressive path, and one unconventional path that challenges an assumption from the problem frame.

Each assessed per criterion with: score, strengths, risks (probability × impact × reversibility), mitigations (with cost and residual risk), and second-order effects.

### Step 4: Decision Matrix
Summary comparison table.

### Step 5: Recommend Top 3
Recommendations can be: single best option, primary + fallback, conditional ("if X, go with A; if Y, go with B"), or hybrid combining elements across approaches. Each recommendation includes key risks, mitigations, leading indicators to watch, and immediate next steps.

## Default Output

**In-chat:** Top 3 recommendations with rationale, risks, mitigations, and next steps.

**File:** Full analysis saved as `.md` (problem frame, criteria, all approaches scored, decision matrix, recommendations).

## Installation

Upload `SKILL.md` to your AI platform's project knowledge, skills directory, or system prompt. See the [main README](../README.md) for platform-specific instructions.
