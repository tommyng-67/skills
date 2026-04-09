---
name: 1-3-1-analysis
description: >
  Conduct a structured 1-3-1 decision analysis: 1 precisely framed problem, exactly 3 approaches,
  exactly 1 recommendation. Triggers ONLY when user explicitly says "1-3-1", "one-three-one",
  or "1 3 1 analysis". All other decision/comparison requests go to 1-5-x-analysis.
---

# 1-3-1 Analysis

**1** precisely framed problem → evaluation criteria → exactly **3** approaches assessed against those criteria → **1** recommendation.

The 1-3-1 is the faster sibling of 1-5-X. Three well-chosen options, one decisive call.

---

## When to Use This Skill

The user explicitly asks for a **1-3-1** — a fast, constrained decision framework. Three options, one winner.

**Trigger phrases:** "1-3-1", "one-three-one", "1 3 1 analysis", "do a 1-3-1 on this". No other phrases trigger this skill — all other decision requests default to 1-5-X.

| | **Deep Research** | **1-5-X** | **1-3-1** (this skill) |
|---|---|---|---|
| **Purpose** | Understand a topic | Decide between approaches | Decide fast |
| **Trigger** | "research", "look into", "what is X", "explain", "deep dive" | "help me decide", "compare", "which should I", "pros and cons" | User explicitly says "1-3-1" |
| **Output** | Findings, insights, implications | Top 3 ranked approaches with scoring | Single recommended approach |
| **Approaches** | N/A | 5+ | Exactly 3 |
| **Recommendations** | N/A | Multiple (often hybrid) | Exactly 1 |
| **Depth** | Exhaustive topic coverage | Exhaustive option analysis | Faster, lighter-weight |

---

## Default Output

**In-chat:** Print **Step 5: the single recommended approach** only.

**File:** Always create a `.md` file containing the full analysis (problem frame, criteria, all 3 approaches with criterion-by-criterion assessment, decision matrix, and recommendation). Save to `/mnt/user-data/outputs/`.

---

## Step 1: Frame the Problem

This step determines whether everything downstream is relevant or wasted. Most problems as initially stated are symptoms, not root causes. Most decisions as initially framed are narrower or broader than they should be.

### 1a: Separate Symptom from Root Cause

The user's stated problem is the starting point, not the answer. Ask: *why* is this a problem? If the answer reveals a deeper issue, frame that instead.

Example: "We're losing deals to Competitor X" is a symptom. The root cause might be pricing, feature gaps, sales process, positioning, or a market segment mismatch. The 1-3-1 should address the root cause — otherwise every approach treats the wrong thing.

If the root cause is ambiguous, state the most likely root cause and why you're framing around it.

### 1b: Establish the Status Quo Baseline

Define what happens if no action is taken:

- **Current trajectory**: Where does the status quo lead in 3/6/12 months?
- **Cost of inaction**: What's lost by waiting? (Revenue, market position, morale, optionality)
- **Decay rate**: Stable, slowly degrading, or in freefall? This sets the urgency bar for the recommendation.

### 1c: Scope the Decision

- **In scope**: What this decision covers.
- **Out of scope**: What this analysis is NOT addressing, and why.
- **Dependencies**: What upstream factors does this depend on? What downstream decisions does this unlock or block?
- **Irreversibility**: One-way door (hard to reverse → demands rigorous analysis) or two-way door (easily reversed → favors speed)? Directly affects risk tolerance in the recommendation.

### 1d: Name the Core Tension

Every meaningful decision has competing forces. Name them: speed vs. quality, cost vs. control, short-term revenue vs. long-term positioning. The tension is what makes it hard — no tension, no decision.

### 1e: Define Success

What specific, measurable outcome would make this decision clearly right in 6–12 months?

### 1f: Surface the Hidden Decision

Often the stated decision masks a deeper strategic question. "Should we hire a contractor or full-time?" might really be "Is this function core to our company or a commodity?" If a hidden decision exists, name it.

**Format:** Write the problem frame as a tight narrative — 1–3 paragraphs a stranger could read and immediately grasp.

---

## Step 2: Define Evaluation Criteria

Criteria must be locked **before** generating approaches. Every approach gets assessed against *what actually matters to this decision*.

### How to derive criteria:

- The **core tension** from 1d should produce at least one criterion on each side.
- The **success definition** from 1e maps to at least one criterion.
- Binding **constraints** appear as criteria.
- **Irreversibility** from 1c influences weights: high-irreversibility → weight risk-related criteria more heavily.

No generic criteria. Not "feasibility" — instead, "Can execute with current 4-person team by end of Q3."

**3–5 criteria.** Tight enough for a fast framework, rigorous enough to differentiate approaches.

### For each criterion:

| Element | Detail |
|---|---|
| **Name** | Specific to this decision. |
| **Weight** | % of total (sum to 100%). |
| **Why it matters** | One sentence tied to the problem frame. |
| **Score 5** | Concretely, what earns a 5. Observable. |
| **Score 1** | Concretely, what earns a 1. Observable. |

---

## Step 3: Generate & Assess Exactly 3 Approaches

### Generating approaches:

Each approach must be a **genuinely distinct strategic path**. Test: if two approaches would be executed by the same team in roughly the same way, they're not distinct.

Span the decision space: one conservative, one aggressive, one that reframes the problem or challenges an assumption from Step 1. If the best answer is clearly a hybrid, still generate the component approaches individually — the hybrid gets constructed in Step 5 from assessed parts.

### Assessing each approach:

**Name & one-sentence summary.**

**How it works** — operationally specific. Not "improve partnerships" but "renegotiate terms with top 3 distributors from net-60 to net-30, offer 2% early-payment discount, targeting $400K cash flow improvement per quarter." Include required capabilities, buy-in, sequencing, and dependencies. If the approach requires something the team doesn't have, say so.

**Criterion-by-criterion assessment:**

For each criterion from Step 2:

- **Score (1–5)** anchored to the 1/5 definitions. One-sentence justification.
- **Strengths** under this criterion — specific, not generic.
- **Risks & threats** under this criterion:
  - **Probability**: High / Medium / Low
  - **Impact if realized**: Severe / Moderate / Minor
  - **Reversibility**: Can we recover? At what cost?
- **Mitigations** for significant risks:
  - What action reduces probability or impact?
  - What does the mitigation cost?
  - What **residual risk** remains after mitigation?
  - Cheap, high-reduction mitigations should raise the score. Expensive mitigations that introduce new risks should not.
- **Second-order effects**: What does this approach enable or prevent in the future? Doors opened, doors closed, dependencies created or removed.

**Approach total:** Weighted score + one-sentence profile.

---

## Step 4: Decision Matrix

| Criterion (Weight) | Approach A | Approach B | Approach C |
|---|---|---|---|
| Criterion 1 (X%) | Score | Score | Score |
| ... | ... | ... | ... |
| **Weighted Total** | **X.X** | **X.X** | **X.X** |

---

## Step 5: Recommend Exactly 1

### On hybrid recommendations:

The strongest recommendation is often a **hybrid** — combining the best elements of multiple approaches while mitigating their individual weaknesses. This is not hedging. Hedging is "it depends" without specifics. A hybrid is **synthesis**: deliberately selecting which components from which approaches to combine, explaining why they're compatible, and showing how the combination neutralizes risks that any single approach would carry alone.

When constructing a hybrid:
- Name which elements come from which approaches
- Explain why these elements are compatible
- Identify new risks the combination introduces
- Show the hybrid scores higher than any individual approach

If one approach clearly dominates without hybridization, recommend it outright. Don't force a hybrid.

### Recommendation structure:

1. **The approach** (or hybrid) — one sentence.
2. **Why it wins** — tied to criteria scores and qualitative factors.
3. **Critical risks and mitigations** — the 2–3 risks most likely to derail this, with specific mitigations and residual risk.
4. **What to watch** — leading indicators it's working or failing. When to revisit the decision.
5. **Immediate next steps** — first 2–3 actions.

Take a decisive position. If you can't choose, explain what information would break the tie — then still name which one you'd pick today.

---

## Formatting & Style

- Tables for criteria and decision matrix in the `.md` file.
- Headers to separate steps in the `.md` file.
- **Writing standard:** Every sentence must be self-explanatory to a reader with no prior context. No jargon without immediate clarification. No filler. No corporate speak. No "leverage," "synergy," "best-in-class," or "holistic." If a word can be deleted without losing meaning, delete it.
- The 1-3-1 `.md` file should be noticeably shorter than a 1-5-X on the same problem.
