---
name: problem-framing
description: >
  Decompose messy, multi-problem situations into clean, distinct, prioritized problem-opportunity
  statements — each ready for 1-5-X analysis. Four steps: Dump (get everything on the table),
  Untangle (separate symptoms from root causes, map dependencies, surface hidden opportunities),
  Prioritize (impact × urgency × dependency position), Package (write dual-framed 1-5-X-ready
  statements). Use this BEFORE 1-5-X when the user has multiple intertwined problems. Trigger on: "I have a lot of problems",
  "everything is broken", "where do I even start", "too many issues", "it's a mess",
  "problem-framing", "help me untangle this", "which problem should I solve first",
  "I don't know what the real problem is", "there's a lot going on", "multiple issues",
  or any situation where the user presents 2+ intertwined problems that would confuse a
  single 1-5-X run. Do NOT trigger for: single well-defined problems (use 1-5-X directly),
  expanding options (use creative-expansion), or research (use deep-research).
---

# Problem Framing

**Dump everything → Untangle the mess → Prioritize what matters → Package for 1-5-X.**

This skill exists because 1-5-X is a precision tool — it works brilliantly on one well-defined problem, but breaks down when handed a tangle of intertwined issues. When a user shows up with "everything is on fire," the instinct is to jump straight into solutions. The right move is to slow down and figure out what the actual problems are first.

This skill turns chaos into a ranked list of clean, dual-framed statements. Each one is ready to be fed into 1-5-X individually. That's the only job — decomposition and prioritization, not solutions.

### The duality principle

Problems and opportunities are the same situation viewed from different angles. "Our best salesperson quit" is a problem — but it's also an opportunity to build a sales system that doesn't depend on one person. "Declining conversion rate" is a problem — but it may also signal an untapped segment the current funnel was never designed to reach.

This skill diagnoses with full rigor — symptoms, root causes, dependencies — then flips each problem into its opportunity counterpart. The frame you hand to 1-5-X shapes every approach it generates. A problem frame triggers fix-it thinking. An opportunity frame triggers build-it thinking. Both frames together produce the strongest downstream analysis.

---

## When to Use This Skill

The user has **multiple problems tangled together** and doesn't know which one to tackle first — or isn't sure which problems are real vs. symptoms of something deeper.

**Trigger phrases:** "I have a lot of problems", "everything is broken", "where do I even start", "too many issues", "it's a mess", "help me untangle this", "which problem should I solve first", "I don't know what the real problem is", "there's a lot going on", "multiple issues", "problem-framing"

**Also trigger when** the user brings what looks like one problem to 1-5-X, but you can see it's actually 2–3 problems welded together. Rather than forcing them into a single frame, redirect to this skill first.

| | **Problem Framing** (this skill) | **Creative Expansion** | **1-5-X** | **1-3-1** | **Deep Research** |
|---|---|---|---|---|---|
| **Purpose** | Decompose & prioritize problems | Expand the solution space | Decide between approaches | Decide fast | Understand a topic |
| **Input** | A mess of intertwined issues | A single challenge, narrowly framed | One well-defined problem | One well-defined problem | A topic to investigate |
| **Output** | 2–5 ranked problem-opportunity statements | 3–5 directions to explore | Top 3 ranked approaches | 1 recommendation | Findings and insights |
| **When** | Before you know what the problem is | Before you're ready to decide | When the problem is clear | When speed matters | When you need to learn |
| **Handoff** | → 1-5-X (per problem) | → 1-5-X or 1-3-1 | ← from Problem Framing | ← from Problem Framing | ← can feed into any |

**The pipeline:** Problem Framing → 1-5-X (per problem) → Execute. Or: Problem Framing → Creative Expansion (if stuck) → 1-5-X → Execute.

---

## Default Output

Run all four steps internally. In chat, print only **Step 4 (The Problem Stack)** — the ranked list of distinct problem statements, each with its one-line diagnosis, dependency note, and the handoff prompt. No dump lists, no untangling breakdowns, no prioritization matrices in chat. Write it as clear, decisive prose — the user should read it and think "yes, that's exactly what I'm dealing with, and now I know where to start."

If the user explicitly asks to save the full analysis (e.g., "save this," "write it all out"), create a `problem-framing-[topic-slug].md` file in the workspace/outputs folder with all four steps.

---

## Step 1: Dump

Get everything out of the user's head. The goal is completeness, not organization. At this stage, don't filter, don't categorize, don't judge. Just collect.

### What to extract:

Pull from what the user has said (and probe for what they haven't):

- **Stated problems** — the things they explicitly named as issues
- **Implied problems** — frustrations, complaints, or tensions that suggest a problem they haven't articulated yet
- **Symptoms vs. causes** — don't separate these yet, just note both. "Revenue is declining" and "our best salesperson quit" might both be on the list — we'll figure out the relationship in Step 2
- **Feelings and frustrations** — these are data. "I'm exhausted by the constant firefighting" is a signal about organizational capacity. "Nobody listens to my recommendations" is a signal about decision-making structure
- **Failed solutions** — what has the user already tried? Failed attempts reveal assumptions and constraints

### How to probe:

If the user's initial description feels incomplete, ask one clarifying question — not five. Good probes:

- "What else is going on that you haven't mentioned yet?"
- "If all of these went away, would things be good — or is there something underneath?"
- "What's the thing you're most avoiding dealing with?"

List everything as raw items. 5–15 items is typical. Fewer than 3 means the user probably has a single problem and should go straight to 1-5-X. More than 15 means you're at the symptom level and need to probe for underlying causes.

---

## Step 2: Untangle

This is the step that makes the skill valuable. Raw problem dumps are full of duplicates, symptoms masquerading as problems, and hidden causal chains. Untangling separates signal from noise.

### 2a: Merge duplicates

Look for items from the dump that are the same problem described differently. "Team communication is poor" and "Nobody knows what anyone else is working on" are likely the same problem. Merge them and keep the most specific framing.

### 2b: Separate symptoms from root causes

For each item, ask: **"Is this a problem, or is it a symptom of a deeper problem?"**

The test: if you solved this item, would the other items still exist? If yes, it's a standalone problem. If solving it would dissolve 2–3 other items, those items are symptoms and this is a root cause.

Common symptom → root cause patterns:

- "Low morale" is almost always a symptom. Root causes: unclear strategy, bad management, unsustainable pace, lack of autonomy, feeling unheard
- "Communication problems" is almost always a symptom. Root causes: misaligned goals, unclear ownership, wrong org structure, trust deficit
- "We're too slow" is almost always a symptom. Root causes: too many priorities, technical debt, wrong team composition, decision paralysis, scope creep

Don't discard symptoms — they're useful data. But label them as symptoms and link them to their likely root cause.

### 2c: Map dependencies

Draw the causal relationships between the remaining problems:

- **A causes B** — solving A would dissolve or significantly reduce B. B is downstream of A.
- **A and B share a root cause C** — C might not be on the list yet. Add it if it emerges.
- **A and B are independent** — they happen to coexist but don't cause each other. Both need their own 1-5-X.
- **A and B create a vicious cycle** — each makes the other worse. Breaking the cycle at either point could work, but you need to identify the more tractable intervention point.

The dependency map is the most important artifact in this skill. It determines the attack sequence in Step 3 — you solve upstream problems before downstream ones, because solving upstream often dissolves downstream for free.

### 2d: Check for the hidden problem — and the hidden opportunity

Sometimes the dump and the untangling reveal a problem that nobody named — a structural issue, a strategic misalignment, or a capability gap that's causing multiple visible problems. If you see one, name it explicitly and add it to the map. This is often the most valuable problem to solve, and it's the one most likely to be missed without this step.

Apply the same lens to opportunities. The tangle often conceals a strategic opening that only becomes visible after untangling — a capability the team is accidentally building, a market position the competition hasn't noticed, or a constraint that, once removed, unlocks several problems at once. Name any hidden opportunity and note which problems it connects to.

### Output of Step 2:

A clean list of **distinct problems** (not symptoms), with dependency relationships noted. Typically 2–5 problems. If you have more than 5 genuinely distinct, non-symptom problems, either the situation is unusually complex or you haven't untangled deeply enough.

---

## Step 3: Prioritize

With the distinct problems identified and dependencies mapped, rank them. The ranking determines which problem to feed into 1-5-X first.

### Prioritization dimensions:

**Impact** — How much does solving this problem improve the overall situation? Consider both direct impact and cascade effects (solving this might dissolve downstream problems).

**Urgency** — How quickly does this need to be addressed? Is it actively getting worse (decaying), stable, or only matters at a future milestone?

**Dependency position** — Where does this sit in the causal chain? Upstream problems (root causes) generally rank higher than downstream problems (symptoms), because solving them has cascade effects. Exception: if an upstream problem is extremely hard to solve and a downstream problem has an available quick fix that buys time, the downstream fix might be the right first move.

**Tractability** — How solvable is this problem given current constraints? A critical problem that's genuinely unsolvable with available resources should be flagged but may rank below a slightly less critical problem that can actually be addressed.

### How to rank:

Don't use a scoring matrix — it creates false precision. Instead, make a judgment call based on the four dimensions above. The ranking should feel like the advice a trusted advisor would give: "Here's where I'd start, and here's why."

If two problems are genuinely tied, say so — and explain what information would break the tie.

---

## Step 4: Package for 1-5-X

Write each problem as a **self-contained problem statement** that 1-5-X can pick up without needing the full context of this analysis. This is the handoff format — each statement should work as a standalone input to 1-5-X's Step 1.

### For each problem (in priority order):

**Problem name** — a short, specific label. Not "Growth" but "Acquisition channel dependency on paid search."

**One-line diagnosis** — what this problem actually is, in plain language. "The team has no repeatable organic acquisition channel, so growth scales linearly with ad spend."

**Why it matters** — one sentence on the stakes. What happens if this isn't addressed?

**Dependency note** — how this problem relates to the others. "Solving this first will likely reduce Problem #3 (rising CAC) as a side effect." Or: "This is independent of the others — it needs its own solution regardless."

**Opportunity reframe** — the same situation expressed as a strategic opening. Not forced optimism — a specific advantage that becomes available by solving this problem. "Acquisition channel dependency on paid search" reframes to "First-mover window to build an organic engine competitors haven't invested in." The reframe must name a concrete strategic gain, not just invert the negative.

**What 1-5-X should focus on** — a brief steering note so 1-5-X frames the problem correctly. "Focus on sustainable acquisition channels, not quick-fix tactics."

### The handoff:

After presenting the problem stack, close with: **"Start with Problem #1 — run 1-5-X on it. The rest can wait until that's resolved (or until we see whether solving #1 changes the picture)."**

If problems are independent and can be tackled in parallel, say so: **"Problems #1 and #2 are independent — you can run 1-5-X on both in parallel."**

This makes the pipeline explicit. Problem Framing decomposes. 1-5-X solves. They're a team.

---

## Edge Cases

**User has only one problem:** If the dump reveals a single, well-defined problem with no tangles, say so directly: "This is actually one clear problem — let's skip straight to 1-5-X." Don't force the four-step process on a situation that doesn't need it.

**User has 10+ genuine problems:** If untangling still leaves more than 5 distinct problems, group them into 2–3 problem *clusters* (themes), prioritize the clusters, and then prioritize within the top cluster. Don't hand the user a list of 10 things to 1-5-X — that's overwhelming. Start with the top cluster and revisit after progress.

**User disagrees with the framing:** The user knows their situation better than this analysis does. If they push back on a dependency relationship, a priority ranking, or a symptom-vs-cause classification, listen. Adjust. The framework serves the user's understanding, not the other way around.

**Problems span different time horizons:** Some problems are "the building is on fire" and some are "we need a new roof eventually." Don't mix them. Handle the fires first (flag urgency), then frame the structural issues as a separate batch for when the crisis is past.

---

## Formatting & Style

**Chat response** (what the user sees):
- The ranked problem stack: each problem with its name, one-line diagnosis, opportunity reframe, why it matters, and dependency note
- The handoff prompt pointing to 1-5-X
- No dump lists, no untangling details, no prioritization reasoning in chat — just the clean output
- Tone: calm, clarifying, authoritative. The user arrived in chaos — the output should feel like someone turned on the lights. Short sentences. No hedging.

**The .md file** (only when explicitly requested):
- All four steps: full dump, untangling logic, dependency map, prioritization reasoning, packaged problem statements
- Use headers to separate steps
- Same writing standards as the ecosystem: no jargon without clarification, no filler, no corporate speak
