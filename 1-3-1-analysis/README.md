# 1-3-1 Analysis

Structured decision framework: **1** precisely framed problem → weighted evaluation criteria → exactly **3** approaches assessed per criterion → **1** recommendation.

Criteria before options. Scoring before gut feel. One clear recommendation backed by evidence, not opinion.

## When to Use

You have a decision to make — product direction, architecture choice, hiring strategy, market entry, vendor selection, resource allocation, or any problem with multiple viable paths and real trade-offs.

**Trigger phrases:** "1-3-1", "one-three-one", "1 3 1 analysis", "do a 1-3-1 on this"

## How It Works

### Step 1: Frame the Problem
Most problems as initially stated are symptoms, not root causes. "Our conversion dropped" is a symptom — the root cause might be pricing, onboarding, targeting, or a competitive shift. This step separates the two, then establishes:

- **Status quo baseline** — what happens if you do nothing? What's the cost of inaction?
- **Core tension** — the competing forces that make this decision hard (speed vs. quality, cost vs. control, short-term vs. long-term)
- **Success definition** — what specific outcome makes this decision clearly right in 6–12 months?
- **Hidden decision** — "build vs. buy" often masks "is this capability core to our differentiation?"

### Step 2: Define Evaluation Criteria
3–5 weighted criteria derived from the problem frame — not a generic template. Each criterion has concrete score-5 and score-1 anchors so scores mean something. Criteria are locked *before* any options are generated. This is the step most people skip — and it's why their decisions fall apart.

### Step 3: Generate & Assess 3 Approaches
Three genuinely distinct paths — not three flavors of the same idea. Typically: one conservative, one aggressive, one that reframes the problem. Each scored per criterion with:

- Specific strengths and risks (rated by probability × impact × reversibility)
- Practical mitigations for each risk — with their own costs and residual risk
- Second-order effects: what does this approach enable or prevent in the future?

Mitigations that actually reduce risk raise the score. Mitigations that are expensive or introduce new risks don't.

### Step 4: Decision Matrix
Summary comparison table for quick scanning after the detailed breakdown.

### Step 5: Recommend 1
Often a hybrid — combining the best elements of multiple approaches while mitigating their individual weaknesses. This isn't hedging ("it depends"). It's synthesis: deliberately selecting which components from which approaches to combine, explaining why they're compatible, and showing the combination outperforms any individual option.

## Default Output

**In-chat:** The single recommended approach with rationale, risks, mitigations, and next steps.

**File:** Full analysis saved as `.md` (problem frame, criteria, all 3 approaches scored, decision matrix, recommendation).

## Example

> "We're losing enterprise deals to a competitor with better reporting. Should we build custom reporting, integrate a third-party BI tool, or partner with the competitor's reporting vendor?"

The skill frames the root cause (is the problem reporting quality, or is reporting a proxy for a deeper trust/credibility gap?), defines criteria weighted to the actual constraint (enterprise sales cycle timing, eng capacity, competitive positioning), scores all three approaches per criterion, and recommends — often a hybrid like "integrate third-party BI for immediate gap closure + build 2 proprietary reports on your unique data advantage that the competitor can't replicate."

## Installation

Upload `SKILL.md` to your AI platform's project knowledge, skills directory, or system prompt. See the [main README](../README.md) for platform-specific instructions.
