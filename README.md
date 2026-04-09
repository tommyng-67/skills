# AI Decision & Research Skills

## Who This Is For

Founders make expensive bets they can't defend when the board asks "what else did you consider?" PMs default to the first plausible option, ship it, then discover the edge cases they would have caught in 30 minutes of structured thinking. Engineers build features where nobody can explain why this approach over the three alternatives. Designers get overruled by whoever argues loudest, not whoever reasoned deepest. And when decisions do get made, nobody can reconstruct *why* six months later.

The pattern is always the same: jump to options before defining what matters, evaluate with gut feel instead of criteria, and confuse "I researched it" with "I read one article and formed an opinion."

These two skills break the pattern.

---

## 1-3-1 Analysis — Decide with thorough & structured approach, not gut feel

**Problem frame** (root cause, core tension, status quo baseline, what success looks like)

→ **Evaluation criteria** (weighted, with concrete score anchors — locked before any options are generated)

→ **3 approaches** (each assessed per criterion: strengths, risks rated by probability × impact × reversibility, practical mitigations with cost and residual risk, second-order effects)

→ **Decision matrix** (3 approaches scored against criteria, weighted totals)

→ **Recommendation** (one — often a hybrid combining the strongest elements across approaches, with mitigations for each weakness)

### Without the skill:

> **"Should we build or buy our analytics pipeline?"**
>
> "I think we should buy. Building takes too long and we need it for Q3. Mixpanel or Amplitude would work. Let's go with Amplitude — I've used it before and it's solid."

One option considered. No criteria defined. No trade-offs evaluated. The decision is anchored to personal familiarity, not the team's actual constraints. When Q3 arrives and Amplitude can't handle the custom event taxonomy, nobody remembers why this path was chosen — because the reasoning was never there.

### With the skill:

> **Problem frame:** The core tension is speed vs. control. A 4-person data team needs production-ready analytics by Q3, but the product roadmap requires custom event taxonomies that most off-the-shelf tools handle poorly. Budget is $200K. The hidden decision: is analytics a commodity or a differentiator for this company?
>
> **Criteria (before any options):**
> - Custom event taxonomy support (30%) — must handle nested product-specific events, not just pageviews
> - Time to production (25%) — Q3 hard deadline, 14 weeks from now
> - Total cost of ownership over 2 years (20%)
> - Team maintainability (15%) — 4-person team can't babysit infrastructure
> - Migration optionality (10%) — can we switch later without rebuilding?
>
> **Three approaches assessed against these criteria.** Each scored with specific evidence, risks rated by probability and impact, mitigations costed.
>
> **Recommendation:** Hybrid — buy Amplitude for standard analytics (ships in 2 weeks), build a thin custom event layer on top using the existing data warehouse (ships in 8 weeks). This scores highest because it meets the Q3 deadline, handles custom taxonomies through the custom layer, and preserves migration optionality since the custom layer is warehouse-native, not Amplitude-native.

Same question. The difference: criteria were defined before options. Three distinct paths were evaluated — not one. The recommendation explains *why* and holds up when someone asks about it six months later.

**→ [Read the full skill documentation](./1-3-1-analysis/)**

---

## Deep Research — Research with method, not luck

**Scope** (assess user's context and why, sharpen the question, map 3–6 dimensions of the topic)

→ **Search** (one subagent per dimension in parallel, or sequential in chat — varied query types: definitional, current state, critical, comparative, applied)

→ **Refine outline** (restructure dimensions based on what the evidence actually revealed — add, reorder, merge, flag gaps)

→ **Triangulate** (classify topic maturity, apply adaptive credibility tiers, cross-verify top 5 claims from independent sources, detect conflicts)

→ **Synthesize** (organize by insight not by source, attribute every claim, state uncertainty honestly)

→ **Package** (one-line answer, key findings with verification status, full analysis, knowledge gaps, sources grouped by credibility tier)

### Without the skill:

> **"Research MCP protocol for our internal tools"**
>
> "MCP (Model Context Protocol) is an open standard by Anthropic for connecting AI models to external tools. It's gaining adoption — I saw a blog post saying it's the future of AI integrations. Seems solid, we should probably build on it."

One source. No credibility assessment. No dimensions mapped — nothing on maturity, limitations, competing approaches, or production stability. "I saw a blog post" is the entire evidence base. The conclusion ("we should probably build on it") isn't supported by anything except the absence of negative information — which was never searched for.

### With the skill:

> **One-line answer:** MCP is production-viable for internal tooling with caveats — the protocol is stable but the ecosystem is early, with significant gaps in authentication, observability, and multi-tenant support.
>
> **Key findings:**
>
> 1. **Adoption is real but narrow.** MCP has 40+ official connectors and active integrations across Claude, Cursor, and Windsurf — but production deployments are concentrated in developer tools, not enterprise internal tools. (Sources: Anthropic docs [T1-E], 3 independent practitioner reports [T2-E])
>
> 2. **Authentication is the biggest gap.** No built-in auth standard for multi-user environments. Teams building internal tools need to layer their own auth, adding 2–4 weeks of integration work. (Sources: 2 engineering blogs describing workarounds [T2-E]. Cross-verified — both reached the same conclusion independently.)
>
> 3. **Competing approaches exist.** OpenAI's function calling and LangChain's tool framework solve similar problems with different tradeoffs — MCP is more standardized but less flexible. (Sources: protocol documentation [T1-E], comparative analysis by a named practitioner [T2-E])
>
> 4. **Early signal — limited corroboration:** One practitioner reports latency issues at scale (>50 concurrent tool calls). Single source; treat as a risk to monitor, not a confirmed limitation.
>
> **Verification status:** 3 of 5 key claims verified by independent sources. 1 contradicted (initial blog overstated connector count). 1 unverifiable (latency claim, single source).

Same question. The difference: six dimensions mapped before searching. Sources assessed by credibility tier — emerging-topic tiers that recognize practitioner expertise. Key claims cross-verified from independent sources. Gaps and uncertainty stated honestly instead of papered over with confidence.

**→ [Read the full skill documentation](./deep-research/)**

---

## Installation

### Claude Projects (claude.ai)

1. Create or open a Project
2. Go to **Project Knowledge**
3. Upload the `SKILL.md` file from each skill folder

### Claude Cowork / Claude Code

```bash
git clone https://github.com/[your-username]/ai-skills.git

cp -r ai-skills/1-3-1-analysis ~/.claude/skills/
cp -r ai-skills/deep-research ~/.claude/skills/
```

### Other Platforms (Cursor, Codex, etc.)

Each skill is a self-contained `SKILL.md` — a structured methodology that any AI platform with tool access can follow. Add the content to your system prompt or project context.

---

## License

MIT — use, modify, and distribute freely.

## Author

**Tommy** — Lead/Staff PM building AI-native workflows for product teams. These skills are part of a broader system for using AI as a thinking partner across the full product craft: decisions, research, strategy, and communication.
