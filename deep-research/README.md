# Deep Research

Six-phase research methodology: **Scope → Search → Refine Outline → Triangulate → Synthesize → Package.**

Turns AI from "search and summarize" into a structured research process — with source credibility assessment calibrated to topic maturity, cross-verification of key claims, and parallel execution in agentic environments.

## When to Use

You want to understand a topic in depth — a new technology, trend, market, concept, or competitive landscape. You want sourced findings with honest uncertainty, not a confident summary built on one article.

**Trigger phrases:** "research this", "look into", "what is X", "deep dive on", "what's the latest on", "explain [concept]", "investigate"

## What Makes This Different

### Topic-Maturity-Adaptive Credibility

For established topics (databases, supply chain), peer-reviewed research and official documentation are the gold standard. For emerging topics (LLM tooling, agentic AI, MCP protocol), those sources don't exist yet — the signal lives in practitioner blogs, GitHub repos, and engineering posts from people who are actually building.

This skill classifies every topic as **Established**, **Emerging**, or **Mixed**, then applies different credibility standards:

- **Established:** peer-reviewed > reputable journalism > industry blogs > forums
- **Emerging:** core maintainer docs and named practitioners with shipped products become primary sources. The credibility test: "Do 2+ independent practitioners report the same finding?" One person's experience is an anecdote. Three converging independently is a signal.

### Dynamic Outline Refinement

Research that locks its structure before seeing any evidence produces reports organized around assumptions, not findings. This skill maps dimensions before searching (Phase 1), then *revises the structure after evidence gathering* (Phase 3) — adding dimensions the evidence revealed, reordering by significance, flagging gaps.

### Cross-Verification

The top 5 claims — the findings most likely to be acted on — are independently verified from sources not already cited. Each classified as **verified**, **contradicted**, or **unverifiable**. This surfaces false consensus and single-source claims before they reach the user.

### Environment-Adaptive Execution

| | Chat (single-agent) | Agentic (subagent-capable) |
|---|---|---|
| Search | 6–8 sequential searches | 15–20+ parallel (one subagent per dimension) |
| Verification | Top 3 claims checked inline | Dedicated verification subagent, top 5 claims |
| Depth | Standard coverage | Deep coverage with full-article reading |

Same methodology. Execution scales with the platform. No lock-in.

## How It Works

1. **Scope** — Assess why the user is researching (context sharpens relevance, not conclusions). Restate the question precisely. Map 3–6 dimensions. Set depth.
2. **Search** — Parallel subagents per dimension (agentic) or sequential queries (chat). Varied query types per dimension: definitional, current state, critical, comparative, applied.
3. **Refine Outline** — Post-evidence structural adjustment. Add, reorder, merge, or flag dimensions. No new searches — structural only.
4. **Triangulate** — Classify topic maturity. Apply adaptive credibility tiers. Cross-verify top claims. Detect conflicts. Check coverage.
5. **Synthesize** — Organize by insight, not by source. Attribute every claim. State convergence with confidence, conflicts with transparency, gaps with honesty.
6. **Package** — One-line answer, key findings (3–7), detailed analysis, verification status, knowledge gaps, sources grouped by tier.

## Default Output

**In-chat:** One-line answer + key findings.

**File:** Full research output saved as `.md`.

## Installation

Upload `SKILL.md` to your AI platform's project knowledge, skills directory, or system prompt. See the [main README](../README.md) for platform-specific instructions.
