# PM Decision Toolkit

Three AI skills for product managers, founders, and CEOs who make decisions for a living.

| Skill | Purpose | Trigger | Output |
|---|---|---|---|
| **[1-5-X Analysis](./1-5-x-analysis)** | Exhaustive decision analysis | "help me decide", "compare", "pros and cons" | Top 3 recommendations + full `.md` analysis |
| **[1-3-1 Analysis](./1-3-1-analysis)** | Fast decision: 3 options, 1 winner | User explicitly says "1-3-1" | Single recommendation + full `.md` analysis |
| **[Deep Research](./deep-research)** | Understand a topic before deciding | "research this", "look into", "what is X" | Key findings in chat + full `.md` research report |

## How They Work Together

**Research first, then decide.** Use Deep Research to understand a topic. Use 1-5-X or 1-3-1 to decide what to do about it.

```
"Research agentic AI workflows"          → Deep Research
"Should we build or buy our AI tooling?" → 1-5-X Analysis
"1-3-1 on which vendor to pilot with"   → 1-3-1 Analysis
```

## Design Principles

**Criteria before options.** Both decision skills define weighted evaluation criteria *before* generating approaches — so every pro/con is assessed against what actually matters, not random advantages.

**Topic-maturity-adaptive credibility.** Deep Research calibrates source credibility to the topic. Established topics require institutional sources. Emerging topics (AI, new protocols) recognize practitioners as primary evidence and use practitioner-convergence as the credibility test.

**Environment-adaptive.** Deep Research auto-detects agentic environments (subagent-capable platforms) and runs parallel search + dedicated verification. In chat, it executes sequentially. Same methodology, different speed.

**Hybrid recommendations.** The strongest approach is often a synthesis combining the best elements of multiple options. Both decision skills actively construct hybrids when warranted — naming which elements come from which approach and why they're compatible.

## Install

Each skill folder contains a `SKILL.md` (the skill definition) and a `README.md` (documentation). Install the `SKILL.md` files into your platform's skill library, or download the pre-packaged `.skill` files from [Releases](./releases).

## Platform Compatibility

These skills are platform-agnostic. They work on any platform that supports skill-based AI workflows — including but not limited to Claude Projects, Cowork, Claude Code, Cursor, and Codex. Agentic features (parallel search, verification subagents) activate automatically when the platform supports subagents.

## License

MIT
