# PM Decision Toolkit

The difference between a good decision and a bad one usually isn't more information. It's whether you defined what matters before or after you saw the options.

Define criteria after, and you'll score to confirm what you already believe. Define criteria first, and the strongest approach surfaces on its own - even when it's a hybrid nobody proposed.

Three AI skills that enforce that sequence for anyone making decisions that matter - PMs picking product direction, founders weighing strategy, engineers evaluating architecture, or operators choosing where to invest next quarter.

## Three Skills

| Skill | What it does | Trigger |
|---|---|---|
| [1-5-X Analysis](./1-5-x-analysis) | Full decision analysis. 5+ approaches scored against weighted criteria. Top 3 recommendations, often a hybrid. | "Help me decide", "compare", "should we X or Y" |
| [1-3-1 Analysis](./1-3-1-analysis) | Same method, tighter scope. 3 approaches, 1 winner. | Say "1-3-1" |
| [Deep Research](./deep-research) | Multi-source research with cross-verification and adaptive source credibility. | "Research this", "what is X", "deep dive on" |

## Sequence

Research first, then decide.

```
"Research agentic AI workflows"          → Deep Research
"Should we build or buy our AI tooling?" → 1-5-X Analysis
"1-3-1 on which vendor to pilot"         → 1-3-1 Analysis
```

## What's Different

**Criteria before options.** Both decision skills lock weighted evaluation criteria before generating approaches. Each criterion gets concrete score anchors - what earns a 5, what earns a 1. Without anchors, every approach lands at 3s and 4s and the matrix tells you nothing.

**Hybrid construction.** The best answer is often a synthesis. Both skills build hybrids when warranted - naming which elements come from which approach, explaining why they're compatible, showing the combination scores higher than any single option. This isn't hedging. It's engineering the strongest possible recommendation from the parts that actually work.

**Adaptive credibility.** Deep Research calibrates source credibility to how mature the topic is. Established topics need institutional sources. Emerging topics - AI tooling, new protocols, anything moving faster than journals can publish - use practitioner-convergence as the credibility test: do 2+ independent builders report the same finding?

## Install

Each skill folder contains two files:
- `SKILL.md` - the skill definition. Add this to your platform's skill library.
- `README.md` - documentation.

Compatible with any platform that supports skill-based AI workflows - Claude Code, Claude Projects, Cursor, Codex, Cowork, and others.

## License

MIT
