# 1-5-X Analysis

Structured decision-making: **1** precisely framed problem → weighted evaluation criteria → **5+** distinct approaches assessed per criterion → **X** recommendations (often a hybrid combining the best elements).

## Why This Exists

Most decision-making is either gut-feel or shallow pros/cons lists. This skill forces rigor: define what matters *before* generating options, assess every option against *the same criteria*, and construct recommendations by cherry-picking the strongest elements across approaches — not just picking one.

## How It Works

| Step | What happens |
|---|---|
| **Frame the Problem** | Separates symptom from root cause. Establishes status quo baseline (what happens if nothing is done). Names the core tensions. Defines measurable success. Surfaces hidden decisions. |
| **Define Criteria** | 4–7 weighted evaluation criteria derived from the problem frame. Each criterion has concrete score anchors (what earns a 5, what earns a 1) to prevent inflation. |
| **Generate & Assess 5+ Approaches** | Each approach assessed per criterion with scores, strengths, risks (probability × impact × reversibility), practical mitigations with residual risk, and second-order effects. |
| **Decision Matrix** | Summary table — weighted scores across all approaches and criteria at a glance. |
| **Recommend Top 3** | Often a hybrid that synthesizes the best-scoring elements across approaches. Includes critical risks, mitigations, leading indicators, and immediate next steps. |

## Output

**In chat:** Top 3 recommendations with rationale, risks, and next steps.

**File:** Full analysis (problem frame, criteria, all approaches with per-criterion assessment, decision matrix, recommendations) saved as `.md`.

## When to Use

| Use **1-5-X** | Use **1-3-1** instead | Use **Deep Research** instead |
|---|---|---|
| Any decision or comparison | User explicitly says "1-3-1" | User wants to understand a topic, not decide |
| "Help me decide", "compare", "pros and cons" | Faster, lighter-weight decision | "Research this", "what is X", "deep dive" |
| Multiple recommendations needed | Exactly 3 options, 1 winner | Findings and insights, not ranked approaches |

## Install

Download `1-5-x-analysis.skill` and add it to your project's skill library.

## Part of the PM Decision Toolkit

Three skills that work together:

- **[1-5-X Analysis](../1-5-x-analysis)** — Exhaustive decision analysis (this skill)
- **[1-3-1 Analysis](../1-3-1-analysis)** — Fast decision: 3 options, 1 winner
- **[Deep Research](../deep-research)** — Understand a topic before deciding
