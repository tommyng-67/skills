# RCA — Root Cause Analysis

Systematic diagnostic protocol: **Issue identification → Event-causal chain (8 steps back, 8 forward) → Fishbone scan → 5 Whys drill → Diagnostic synthesis.**

Pure diagnosis. No solutions until the diagnosis is confirmed.

## When to Use

Something broke — a skill didn't trigger, logic misfired, a pipeline chain failed, behavior was inconsistent with expectations. You need to understand *why* before you fix anything.

**Trigger phrases:** "Run RCA", "RCA on this", "RCA:", "do an RCA", "root cause this", "diagnose this"

## How It Works

### Phase 1: Issue Identification
State the failure clearly: what broke, where the breakdown became visible, expected vs. actual behavior, which components are implicated.

### Phase 2: Event-Causal Chain
The spine of the RCA. Trace **8 steps backward** from the failure point (preconditions), then **8 steps forward** (propagation). At each step: what happened, why (the causal mechanism), and what tension was exposed. Flag the 3 highest-tension nodes for deeper drilling.

### Phase 3: Fishbone Scan
Check whether any *category* of cause was missed by scanning 5 dimensions: System, Process, Content, Memory, Environment. Supplements the chain — never replaces it.

### Phase 4: 5 Whys Drill
Run iterative "why?" drilling on the 3 highest-tension nodes. Stop at 5 levels or when the answer becomes a system constraint. Each drill bottoms out at a named cause type: logic gap, missing definition, ambiguous instruction, competing rule, system constraint, or unknown.

### Phase 5: Diagnostic Synthesis
Four named outputs — no solutions, no recommendations, no imperative verbs:

- **Root causes** — ranked by confidence (confirmed / probable / suspected)
- **Tensions** — competing forces or contradictions exposed
- **Inconsistencies** — where system state contradicts its own rules
- **Gaps** — missing definitions or undocumented assumptions

Solutioning begins only on explicit request after the diagnosis is confirmed.

## Default Output

**In-chat:** The full diagnostic — issue identification, causal chain, fishbone findings, 5 Whys results, and synthesis with counts of root causes, tensions, inconsistencies, and gaps.

## Installation

Upload `SKILL.md` to your AI platform's project knowledge, skills directory, or system prompt. See the [main README](../README.md) for platform-specific instructions.
