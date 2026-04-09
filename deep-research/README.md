# Deep Research

Structured multi-source research that adapts to what it finds. The outline isn't locked before the evidence comes in - it gets revised after. Claims get cross-verified. Source credibility is calibrated to how mature the topic actually is.

## How It Works

Six phases. The order matters.

**Scope.** Assess why the user is researching this. Sharpen the question. Map 3-6 dimensions of the topic. Set depth - standard or deep.

**Search.** One search per dimension minimum. In agentic environments (Claude Code, Cursor, Codex): one subagent per dimension running 3-5 parallel searches. In chat: sequential. Same methodology, different speed.

**Refine the outline.** This is what most research tools skip. After evidence is gathered, revise the dimension structure - add what the evidence revealed, cut what turned out empty, reorder by actual significance. Structure follows evidence, not the other way around.

**Triangulate.** Classify topic maturity: established, emerging, or mixed. Apply adaptive credibility tiers. For established topics (databases, supply chain), institutional sources carry weight. For emerging topics (LLM applications, agentic AI), practitioners building and shipping are the primary evidence - the credibility test becomes "do 2+ independent practitioners converge on the same finding?" Cross-verify the 5 most important claims from independent sources.

**Synthesize.** Organize by insight, not by source. State convergence with confidence, conflicts with transparency, gaps honestly.

**Package.** One-line answer, key findings, detailed analysis, verification status for each major claim, knowledge gaps, sources grouped by credibility tier.

## Example Output (Abbreviated)

What the findings section looks like:

> **One-line answer:** Multi-agent orchestration is converging on supervisor patterns, but the real bottleneck is handoff reliability, not agent capability.
>
> **Key findings:**
>
> 1. Multi-agent frameworks are converging on a supervisor pattern - a routing agent that delegates to specialized sub-agents. CrewAI, AutoGen, and LangGraph all implement variations. The "flat peer" architecture (agents negotiating directly) works in demos but breaks at 4+ agents due to context pollution.
>
> 2. Cost per agentic task is dropping faster than quality is improving. Median cost for a research-grade workflow fell from ~$2.40 to ~$0.35 in 8 months (based on 3 independent practitioner benchmarks). Quality gains are incremental.
>
> **Verification:** Finding 1 verified (4 independent sources). Finding 2 partially verified - cost figures converge across sources, quality assessment based on 2 sources with different evaluation criteria.

## When to Use

Use Deep Research when you need to understand something before making a call. If you already understand the topic and need to decide, use 1-5-X or 1-3-1.

| Use Deep Research | Use 1-5-X instead | Use 1-3-1 instead |
|---|---|---|
| "Research this", "what is X", "deep dive" | "Help me decide", "compare options" | Say "1-3-1" for speed |
| You want findings and implications | You want ranked approaches with scoring | You want one winner |

## Install

Add `SKILL.md` to your platform's skill library.

## Part of the PM Decision Toolkit

- [1-5-X Analysis](../1-5-x-analysis) - Full decision analysis
- [1-3-1 Analysis](../1-3-1-analysis) - Fast decision: 3 options, 1 winner
- [Deep Research](../deep-research) - Understand before deciding (this skill)
