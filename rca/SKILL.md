---
name: rca
description: >
  Root Cause Analysis skill for systematically diagnosing failures in the Claude setup
  (CLAUDE.md logic, skill triggers, memory system, pipeline chains, session behavior).
  Traces 8 steps back and 8 steps forward from the failure point. Surfaces tensions,
  root causes, inconsistencies, and gaps. Explicitly holds the solutioning phase.
  Triggers on: "Run RCA", "RCA on this", "RCA:", "do an RCA".
---

# RCA — Root Cause Analysis

Systematic diagnostic protocol for Claude setup failures. Pure diagnosis. No solutions.

---

## When to Use This Skill

The user has encountered a failure, malfunction, or unexpected behavior in the Claude workbench — a skill didn't trigger, CLAUDE.md logic broke, memory wasn't persisted, a pipeline chain fired incorrectly, or session behavior was inconsistent with expectations.

**Trigger phrases:** "Run RCA", "RCA on this", "RCA:", "do an RCA", "root cause this", "diagnose this"

The goal is a complete, structured diagnostic — not a fix. Solutioning is a separate phase, invoked only after the RCA is complete and the user confirms the diagnosis.

---

## Before You Begin

Ask the user (or infer from context) the following. Do NOT proceed to Phase 1 without these anchors:

1. **The failure statement** — what broke, in one sentence. ("Skill X did not trigger when I said Y.")
2. **The failure point** — the specific moment or action where the breakdown became visible.
3. **Expected vs. actual** — what should have happened vs. what did happen.
4. **Session context** — any relevant session state: compaction occurred, new files added, CLAUDE.md edited, etc.

If the user says "RCA on this" with no other context, ask for the failure statement before proceeding.

---

## Phase 1 — Issue Identification

State the failure clearly and completely. No inference, no editorializing.

**Format:**
```
FAILURE: [one sentence — what broke]
FAILURE POINT: [the specific action, trigger, or moment where breakdown became visible]
EXPECTED: [what should have happened]
ACTUAL: [what did happen]
SCOPE: [which components are implicated — CLAUDE.md / skill / memory / trigger / session / pipeline]
```

This block is the anchor for everything downstream. Every step in the chain must connect back to it.

---

## Phase 2 — Event-Causal Chain

The spine of the RCA. Trace 8 steps backward from the failure point, then 8 steps forward. At each step, answer three questions:

- **What happened** — the observable event or state at this step
- **Why** — the causal mechanism that connected this step to the next (or prior)
- **Tension** — any inconsistency, gap, ambiguity, or competing force exposed at this step

Steps do not need to be equal in time. A "step" is a discrete causal event — a parse, a trigger check, a file read, a memory write, a session state change.

If a step is unknown or uncertain, mark it `[UNKNOWN]` and state what would need to be true for the chain to be complete. Do NOT infer or fabricate.

---

### 8 Steps Back (Preconditions)

Trace backward from the failure point. Step -1 is the immediate precondition; Step -8 is the earliest recoverable context.

```
STEP -8: [What happened] | Why: [causal link to -7] | Tension: [if any]
STEP -7: [What happened] | Why: [causal link to -6] | Tension: [if any]
STEP -6: [What happened] | Why: [causal link to -5] | Tension: [if any]
STEP -5: [What happened] | Why: [causal link to -4] | Tension: [if any]
STEP -4: [What happened] | Why: [causal link to -3] | Tension: [if any]
STEP -3: [What happened] | Why: [causal link to -2] | Tension: [if any]
STEP -2: [What happened] | Why: [causal link to -1] | Tension: [if any]
STEP -1: [What happened] | Why: [causal link to FAILURE] | Tension: [if any]

>>> FAILURE POINT <<<
```

---

### 8 Steps Forward (Propagation)

Trace forward from the failure point. Step +1 is the immediate effect; Step +8 is the furthest downstream impact observed or inferable.

```
>>> FAILURE POINT <<<

STEP +1: [What happened] | Why: [causal link from failure] | Tension: [if any]
STEP +2: [What happened] | Why: [causal link from +1] | Tension: [if any]
STEP +3: [What happened] | Why: [causal link from +2] | Tension: [if any]
STEP +4: [What happened] | Why: [causal link from +3] | Tension: [if any]
STEP +5: [What happened] | Why: [causal link from +4] | Tension: [if any]
STEP +6: [What happened] | Why: [causal link from +5] | Tension: [if any]
STEP +7: [What happened] | Why: [causal link from +6] | Tension: [if any]
STEP +8: [What happened] | Why: [causal link from +7] | Tension: [if any]
```

After completing both directions: flag the **3 highest-tension nodes** — steps where the tension marker revealed the most significant inconsistency, gap, or competing force. These become the input to Phase 4.

---

## Phase 3 — Dimension Completeness Check (Fishbone Scan)

The Event-Causal Chain traces sequence. This phase checks whether any *category* of cause was missed.

Scan across 5 dimensions. For each, answer: does this dimension contain a contributing cause not already captured in the chain?

| Dimension | What to check | Finding |
|---|---|---|
| **System** | Claude architecture, model behavior, context window, compaction logic | [gap / no gap / unknown] |
| **Process** | Skill trigger logic, pipeline chains, auto-invoke rules, ordering | [gap / no gap / unknown] |
| **Content** | CLAUDE.md instructions, SKILL.md definitions, memory file content, formatting | [gap / no gap / unknown] |
| **Memory** | MEMORY.md index, memory file accuracy, staleness, missing pointers | [gap / no gap / unknown] |
| **Environment** | Session state, prior compaction, context loaded, file system state | [gap / no gap / unknown] |

If a dimension reveals a cause NOT in the chain, add it as a supplemental node — labeled `[FISHBONE: dimension]` — and note where in the chain it would connect.

---

## Phase 4 — 5 Whys Drill (Critical Fault Nodes)

Run iterative "why?" drilling on the **3 highest-tension nodes** identified at the end of Phase 2. Stop at 5 levels or when the answer becomes a system constraint (something that cannot be decomposed further within the Claude setup).

**Format for each node:**

```
NODE: [Step label from Phase 2 — e.g., STEP -3]
Observation: [restate what happened at this node]

Why 1: [first-level cause]
Why 2: [why did Why 1 occur?]
Why 3: [why did Why 2 occur?]
Why 4: [why did Why 3 occur?]
Why 5: [why did Why 4 occur?]

Bottom cause: [the deepest answerable cause — name it plainly]
Nature: [LOGIC GAP / MISSING DEFINITION / AMBIGUOUS INSTRUCTION / COMPETING RULE / SYSTEM CONSTRAINT / UNKNOWN]
```

Do NOT stop early because an answer "seems obvious." Do NOT skip a level because the cause feels self-evident. The drill exists precisely to get past the obvious.

---

## Phase 5 — Diagnostic Synthesis

Consolidate findings from Phases 2, 3, and 4 into four named outputs. No solutions. No recommendations. No "we should." Diagnosis only.

---

### 5a — Root Causes

List the deepest causal factors identified. These are the conditions whose absence would have prevented the failure. Rank by confidence (confirmed / probable / suspected).

```
ROOT CAUSE 1 (confirmed): [name it plainly — one sentence]
ROOT CAUSE 2 (probable): [name it plainly — one sentence]
ROOT CAUSE 3 (suspected): [name it plainly — one sentence]
```

---

### 5b — Tensions

List the competing forces, contradictions, or ambiguities exposed by the analysis. A tension is a place where two rules, expectations, or states pull in opposite directions. Name both sides.

```
TENSION 1: [X pulls toward A] ↔ [Y pulls toward B]
TENSION 2: ...
```

---

### 5c — Inconsistencies

List places where the system state contradicts what it should be according to its own rules — CLAUDE.md says X but behavior was Y; memory says X is true but current file says otherwise; skill trigger says "invoke on Z" but Z did not invoke it.

```
INCONSISTENCY 1: [Expected: X] ↔ [Actual: Y] — source: [where the rule/state is defined]
INCONSISTENCY 2: ...
```

---

### 5d — Gaps

List missing definitions, absent rules, unspecified behaviors, or undocumented assumptions that the system relied on implicitly. A gap is something that *should exist* but doesn't.

```
GAP 1: [what is missing] — [where it should be defined]
GAP 2: ...
```

---

## Diagnostic Complete

```
╔══════════════════════════════════════════════════════╗
║  DIAGNOSTIC COMPLETE — NO SOLUTIONS PROPOSED         ║
║  Solutioning phase begins only on explicit request.  ║
╚══════════════════════════════════════════════════════╝
```

State the total count of findings:
- Root causes identified: N (confirmed / probable / suspected)
- Tensions surfaced: N
- Inconsistencies found: N
- Gaps identified: N
- Unknown steps in chain: N

Ask the user: "Ready to move to solutioning, or do any of these findings need further investigation first?"

---

## Execution Rules

1. **No imperative verbs in the diagnostic.** "We should," "fix," "update," "change," "add," "remove" — none of these appear until the user explicitly opens the solutioning phase.
2. **Mark unknowns explicitly.** Never infer a step to fill a gap. `[UNKNOWN]` is a valid and important finding.
3. **Steps must be discrete.** A "step" is a single event. Do not collapse two events into one step to hit 8.
4. **Causality is directional.** "Why" must explain the connection *from* the prior step *to* the current one, not just re-describe the current step.
5. **Tensions must name both sides.** A tension without both sides named is just a complaint, not a diagnosis.
6. **Fishbone supplements, never replaces.** The chain is the primary structure. Fishbone findings are added as supplemental nodes only.
7. **5 Whys drill only on flagged nodes.** Do not drill every step — only the 3 highest-tension nodes from Phase 2.
8. **Source every inconsistency.** Each inconsistency must name where the contradicting rule or state is defined (CLAUDE.md line, skill name, memory file).
