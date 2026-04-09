---
name: 1-5-x-analysis
description: >
  Conduct a structured 1-5-X decision analysis: 1 precisely framed problem, up to 5+ approaches
  with weighted scoring, X recommendations. Default skill for any decision, comparison, or
  "help me decide" request. Triggers on: "1-5-X", "pros and cons", "compare options", "which
  should I choose", "what would you recommend", "should we X or Y", "I'm torn between", or any
  problem that needs structured thinking — even without explicit framework request.
---

# 1-5-X Analysis

**1** precisely framed problem → evaluation criteria → **5+** approaches assessed against those criteria → **X** recommendations (often a hybrid).

---

## When to Use This Skill

The user wants to **make a decision** — not just understand a topic. They have a problem, and they need approaches evaluated and a recommendation.

**Trigger phrases:** "help me decide", "which should I choose", "compare options", "what would you recommend", "should we X or Y", "I'm torn between", "pros and cons", "what's the best approach", "1-5-X", or any problem requiring structured evaluation of multiple paths — even without an explicit framework request.

| | **Deep Research** | **1-5-X** (this skill) | **1-3-1** |
|---|---|---|---|
| **Purpose** | Understand a topic | Decide between approaches | Decide fast |
| **Trigger** | "research", "look into", "what is X", "explain", "deep dive" | "help me decide", "compare", "which should I", "pros and cons" | User explicitly says "1-3-1" |
| **Output** | Findings, insights, implications | Top 3 ranked approaches with scoring | Single recommended approach |
| **Approaches** | N/A | 5+ | Exactly 3 |
| **Recommendations** | N/A | Multiple (often hybrid) | Exactly 1 |
| **Depth** | Exhaustive topic coverage | Exhaustive option analysis | Faster, lighter-weight |

---

## Default Output

**In-chat:** Print **Step 5: top 3 recommendations** only.

**File:** Always create a `.md` file containing the full analysis (problem frame, criteria, all approaches with criterion-by-criterion assessment, decision matrix, and recommendations). Save to `/mnt/user-data/outputs/`.

---

## Step 1: Frame the Problem

This step determines whether everything downstream is relevant or wasted. Most problems as initially stated are symptoms, not root causes. Most decisions as initially framed are narrower or broader than they should be.

### 1a: Separate Symptom from Root Cause

The user's stated problem is the starting point, not the answer. Ask: *why* is this a problem? If the answer reveals a deeper issue, frame that instead.

Example: "Our conversion rate dropped 15%" is a symptom. The root cause might be a pricing mismatch, a broken onboarding flow, a competitive shift, or a targeting change. The 1-5-X should address the root cause, not the symptom — otherwise every approach treats the wrong thing.

If the root cause is ambiguous, state the 2–3 most likely root causes and which one you're framing around (and why).

### 1b: Establish the Status Quo Baseline

Define what happens if no action is taken. This is not optional — it's the anchor for evaluating every approach. Specifically:

- **Current trajectory**: Where does the status quo lead in 3/6/12 months?
- **Cost of inaction**: What's lost by waiting or doing nothing? (Revenue, market position, morale, optionality)
- **Decay rate**: Is the situation stable, slowly degrading, or in freefall? This determines how much urgency the recommendation should carry.

### 1c: Scope the Decision

Draw explicit boundaries:

- **In scope**: What this decision covers.
- **Out of scope**: What adjacent problems or decisions this analysis is NOT addressing, and why.
- **Dependencies**: What upstream decisions or external factors does this depend on? What downstream decisions does this unlock or constrain?
- **Irreversibility**: Is this a one-way door (hard to reverse, demands rigorous analysis) or a two-way door (easily reversed, favors speed over perfection)? This directly affects how much risk tolerance the recommendation should carry.

### 1d: Name the Core Tension

Every meaningful decision has competing forces. Name them explicitly: speed vs. quality, cost vs. control, short-term revenue vs. long-term positioning, team capacity vs. market window. The tension is what makes the decision hard — if there were no tension, there'd be no decision to make.

### 1e: Define Success

What specific outcome, measurable where possible, would make this decision clearly right in 6–12 months? This becomes the anchor for evaluation criteria in Step 2.

### 1f: Surface the Hidden Decision

Often the stated decision masks a deeper strategic question. "Should we build or buy?" might really be asking "Is this capability core to our differentiation?" "Should we enter market X?" might really be asking "Are we a single-product company or a platform?" If a hidden decision exists, name it — it changes which approaches are even worth considering.

**Format:** Write the problem frame as a tight narrative — 2–4 paragraphs that a stranger with no context could read and immediately understand the decision, the stakes, and what "good" looks like.

---

## Step 2: Define Evaluation Criteria

Criteria must be locked **before** generating approaches. They exist to ensure every approach is assessed against *what actually matters to this decision*, not against generic dimensions.

### How to derive criteria:

Every criterion must trace directly to the problem frame. Specifically:

- The **core tension** from 1d should produce at least one criterion on each side of the tension (e.g., if the tension is speed vs. quality, there should be a criterion for time-to-delivery AND a criterion for output quality).
- The **success definition** from 1e should map to at least one criterion.
- **Constraints** (budget, timeline, capacity) should appear as criteria if they're binding.
- **Irreversibility** from 1c should influence weights: high-irreversibility decisions should weight risk-related criteria more heavily.

Do NOT use generic criteria like "feasibility" or "impact" without making them specific to this decision. "Feasibility" means nothing. "Can ship with current 3-person eng team in Q2" means something.

**4–7 criteria.** Fewer than 4 misses important dimensions. More than 7 dilutes signal.

### For each criterion:

| Element | Detail |
|---|---|
| **Name** | Specific to this decision. "Time to first paying customer" not "Speed." |
| **Weight** | % of total (must sum to 100%). Derived from the problem frame, not arbitrary. |
| **Why it matters** | One sentence connecting it to the problem frame. |
| **Score 5** | What concretely earns a 5. Observable, not subjective. |
| **Score 1** | What concretely earns a 1. Observable, not subjective. |

The 1/5 anchors exist to prevent score inflation. Without them, every approach gets 3s and 4s and the matrix is useless.

---

## Step 3: Generate & Assess Approaches (5+ Minimum)

### Generating approaches:

Each approach must be a **genuinely distinct strategic path**, not a parameter tweak on another approach. Test: if two approaches would be executed by the same team in roughly the same way with roughly the same dependencies, they're not distinct.

Span the decision space deliberately. Include at least:
- One **conservative / low-risk** path
- One **aggressive / high-upside** path
- One **unconventional** path that reframes the problem or challenges an assumption from Step 1

If a hybrid approach is obvious from the start, still generate the component approaches individually first — the hybrid gets constructed in Step 5 from assessed parts, not assumed upfront.

### Assessing each approach:

For every approach, provide:

**Name & one-sentence summary.**

**How it works** — operationally specific. Not "leverage partnerships" but "sign distribution agreement with X-type partners, compensated via Y model, targeting Z volume in N months." Include what capabilities, buy-in, sequencing, and dependencies are required to execute. If the approach requires something the team doesn't currently have (a skill, a tool, a relationship, regulatory approval), say so — that's a real cost.

**Criterion-by-criterion assessment:**

For each criterion from Step 2:

- **Score (1–5)** anchored to the 1/5 definitions. Justify in one sentence.
- **Strengths** under this criterion. Be specific — not "good for growth" but "opens access to 50K SMB accounts via partner's existing distribution."
- **Risks & threats** under this criterion. Categorize each:
  - **Probability**: How likely? (High / Medium / Low)
  - **Impact if realized**: How bad? (Severe / Moderate / Minor)
  - **Reversibility**: If this goes wrong, can we recover? At what cost?
- **Mitigations** for each significant risk:
  - What specific action reduces probability or impact?
  - What does the mitigation itself cost (time, money, complexity)?
  - What **residual risk** remains after mitigation?
  - Mitigations that are free or cheap with high risk reduction should raise the criterion score. Mitigations that are expensive or introduce new risks should not.
- **Second-order effects**: What does this approach enable or prevent in the future? Does it build a capability, create a dependency, open a door, or close one? Second-order effects often matter more than first-order outcomes.

**Approach total:** Weighted score + one-sentence profile (e.g., "Highest upside but depends on a partnership that doesn't exist yet").

---

## Step 4: Decision Matrix

Summary table after the detailed breakdowns:

| Criterion (Weight) | Approach A | Approach B | Approach C | Approach D | Approach E |
|---|---|---|---|---|---|
| Criterion 1 (X%) | Score | Score | Score | Score | Score |
| ... | ... | ... | ... | ... | ... |
| **Weighted Total** | **X.X** | **X.X** | **X.X** | **X.X** | **X.X** |

---

## Step 5: Recommend (X — Top 3)

### On hybrid recommendations:

The strongest recommendation is often a **hybrid** that combines the best elements of multiple approaches while mitigating their individual weaknesses. This is not hedging — hedging is "it depends" without specifics. A hybrid is **synthesis**: deliberately selecting which components from which approaches to combine, explaining why each component was chosen, and how the combination neutralizes risks that any single approach would carry alone.

When constructing a hybrid:
- Name which specific elements come from which approaches
- Explain why these elements are compatible (not all combinations work)
- Identify any new risks the combination introduces (integration complexity, conflicting dependencies)
- Show that the hybrid scores higher on the criteria than any individual approach

If a single approach clearly dominates without needing hybridization, recommend it outright. Don't force a hybrid when one isn't warranted.

### Recommendation structure (for each of the top 3):

1. **Which approach (or hybrid)** — one sentence.
2. **Why it wins** — tied to criteria scores and qualitative judgment. What makes this approach's profile better than the alternatives?
3. **Critical risks and mitigations** — the 2–3 risks most likely to derail this approach, with specific mitigations and residual risk.
4. **What to watch** — leading indicators that this approach is working (or failing). When would you revisit the decision?
5. **Immediate next steps** — the first 2–3 actions to start executing.

Rank the top 3 in order of overall strength. If #1 is clearly superior, say so. If #1 and #2 are close, explain what factor tips the balance.

---

## Formatting & Style

- Tables for criteria and decision matrix in the `.md` file.
- Headers to separate steps in the `.md` file.
- **Writing standard:** Every sentence must be self-explanatory to a reader with no prior context. No jargon without immediate clarification. No filler. No corporate speak. No "leverage," "synergy," "best-in-class," or "holistic." If a word can be deleted without losing meaning, delete it.
