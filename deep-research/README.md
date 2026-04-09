# Deep Research

Structured multi-source research: **Scope → Search → Refine Outline → Triangulate → Synthesize → Package.** Adapts to your environment — parallel subagent search in agentic platforms, sequential search in chat.

## Why This Exists

Unstructured web research produces inconsistent results: missed dimensions, single-source claims presented as fact, structure locked before evidence is seen, no verification of key findings. This skill enforces a methodology that covers topics systematically, calibrates source credibility to the topic's maturity, and verifies the claims that matter most.

## How It Works

| Phase | What happens |
|---|---|
| **Scope** | Assesses user context (why they're researching). Sharpens the question. Maps 3–6 dimensions of the topic. Sets depth (Standard or Deep). |
| **Search** | One search per dimension minimum. In agentic environments: one subagent per dimension running 3–5 searches in parallel. In chat: sequential. |
| **Refine Outline** | After evidence is gathered, revises the dimension structure — adds dimensions the evidence revealed, reorders by significance, flags empty dimensions. Structure follows evidence, not the other way around. |
| **Triangulate** | Classifies topic maturity (Established / Emerging / Mixed). Applies adaptive source credibility tiers. Cross-verifies the 5 most important claims from independent sources. |
| **Synthesize** | Organized by insight, not by source. Integrates findings across sources per dimension. States convergence with confidence, conflicts with transparency, and gaps honestly. |
| **Package** | One-line answer, key findings, detailed analysis, verification status, knowledge gaps, sources grouped by tier. |

## Key Design Decisions

**Topic-maturity-adaptive credibility.** For established topics (databases, supply chain), strict tiers apply — peer-reviewed and institutional sources required. For emerging topics (LLM applications, agentic AI, new protocols), a parallel tier system recognizes that practitioners who are building and shipping are the primary evidence source, not institutions that haven't caught up yet. The credibility test shifts from "is this an institutional source?" to "do 2+ independent practitioners converge on the same finding?"

**Environment-adaptive execution.** Auto-detects whether subagents are available. In agentic environments (Cowork, Claude Code, Cursor, Codex): parallel search across dimensions + dedicated verification subagent. In chat: sequential search + inline verification. Same methodology, different execution speed.

**Dynamic outline refinement.** Most research tools lock their structure before seeing evidence. This skill revises its dimension structure after evidence gathering — adding what the evidence revealed, removing what turned out empty, reordering by actual significance.

**Cross-verification.** The 5 most important claims get independently verified from sources not already cited. Each claim is classified as verified, contradicted, or unverifiable. These classifications appear in the final output so the user knows how much to trust each finding.

## Output

**In chat:** One-line answer + key findings (3–7).

**File:** Full research output (answer, findings, detailed analysis, verification status, knowledge gaps, sources by tier) saved as `.md`.

## When to Use

| Use **Deep Research** | Use **1-5-X** instead | Use **1-3-1** instead |
|---|---|---|
| Understand a topic in depth | Make a decision between approaches | Make a fast decision |
| "Research this", "look into", "what is X" | "Help me decide", "compare options" | User explicitly says "1-3-1" |
| Findings, insights, implications | Top 3 ranked approaches with scoring | Single recommended approach |

## Install

Download `deep-research.skill` and add it to your project's skill library.

## Part of the PM Decision Toolkit

Three skills that work together:

- **[1-5-X Analysis](../1-5-x-analysis)** — Exhaustive decision analysis
- **[1-3-1 Analysis](../1-3-1-analysis)** — Fast decision: 3 options, 1 winner
- **[Deep Research](../deep-research)** — Understand a topic before deciding (this skill)
