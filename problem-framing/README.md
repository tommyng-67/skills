# Problem Framing

Decompose messy, multi-problem situations into clean, prioritized problem statements: **Dump → Untangle → Prioritize → Package for 1-5-X.**

This skill exists because 1-5-X is a precision tool — it works brilliantly on one well-defined problem, but breaks down when handed a tangle of intertwined issues. Problem Framing turns chaos into a ranked list of clean problem statements, each ready to be fed into 1-5-X individually.

## When to Use

You have **multiple problems tangled together** and don't know which one to tackle first — or aren't sure which problems are real vs. symptoms of something deeper.

**Trigger phrases:** "everything is broken", "where do I even start", "too many issues", "it's a mess", "help me untangle this", "which problem should I solve first", "I don't know what the real problem is", "multiple issues"

**Also triggers when** what looks like one problem turns out to be 2–3 problems welded together.

## How It Works

### Step 1: Dump
Get everything out: stated problems, implied problems, symptoms, frustrations, failed solutions. 5–15 raw items. No filtering, no judging — just collecting.

### Step 2: Untangle
The step that makes the skill valuable. Merge duplicates, separate symptoms from root causes, map causal dependencies between problems, and surface hidden structural issues nobody named.

Key moves:

- **Symptom test:** If you solved this item, would the other items still exist? If solving it dissolves 2–3 others, those are symptoms and this is the root cause.
- **Dependency map:** Which problems cause which? Upstream problems rank higher because solving them often dissolves downstream problems for free.
- **Hidden problem check:** Does the tangle reveal a structural issue nobody named? Name it.

### Step 3: Prioritize
Rank the distinct problems across four dimensions: impact (including cascade effects), urgency (decaying vs. stable), dependency position (root cause vs. downstream), and tractability (solvable with current constraints). Judgment call, not a scoring matrix.

### Step 4: Package for 1-5-X
Write each problem as a self-contained statement that 1-5-X can pick up cold: problem name, one-line diagnosis, why it matters, dependency note, and a steering note for how 1-5-X should frame it.

### Handoff
"Start with Problem #1 — run [1-5-X](../1-5-x-analysis/) on it. The rest can wait until that's resolved."

## Default Output

**In-chat:** The ranked problem stack — each problem with its name, diagnosis, stakes, and dependency note, plus the handoff prompt. No dump lists or untangling breakdowns.

**File:** Full analysis saved as `.md` when explicitly requested.

## Installation

Upload `SKILL.md` to your AI platform's project knowledge, skills directory, or system prompt. See the [main README](../README.md) for platform-specific instructions.
