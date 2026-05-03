# AI Thinking Skills

Structured methodologies that turn AI into a rigorous thinking partner — for decisions, research, creative exploration, and diagnostics.

The pattern they break: jumping to options before defining what matters, evaluating with gut feel instead of criteria, and confusing "I researched it" with "I read one article and formed an opinion."

---

## The System

Six skills, each with a distinct purpose. They compose into a pipeline:

```
Problem Framing → Creative Expansion → 1-5-X or 1-3-1 → Execute
                        ↑                    ↑
                   Deep Research ─────────────┘

RCA (diagnose failures independently)
```

| Skill | Purpose | Output | When to Use |
|---|---|---|---|
| [**Problem Framing**](./problem-framing/) | Decompose tangled problems | 2–5 dual-framed problem-opportunity statements | Multiple intertwined issues, unclear where to start |
| [**1-3-1 Analysis**](./1-3-1-analysis/) | Decide fast | 1 recommendation | You have a decision with 3 clear options |
| [**1-5-X Analysis**](./1-5-x-analysis/) | Decide thoroughly | Top 3 ranked | Complex decisions, multiple stakeholders, high stakes |
| [**Deep Research**](./deep-research/) | Understand a topic | Sourced findings with verification status | You need depth, not a decision |
| [**Creative Expansion**](./creative-expansion/) | Widen the solution space | 3–5 new directions | You're stuck or narrowing too early |
| [**RCA**](./rca/) | Diagnose failures | Root causes, tensions, gaps | Something broke and you need to know *why* |

Each skill is self-contained. Use one alone or chain them — Problem Framing decomposes chaos into clean problems, Creative Expansion opens options, 1-5-X evaluates them, Deep Research feeds evidence into any.

---

## What Changes

**Without structured thinking:**

> *"Should we build or buy our analytics pipeline?"*
>
> "Buy Amplitude — I've used it before, it's solid, and we need it for Q3."

One option. No criteria. No trade-offs. Anchored to familiarity, not constraints.

**With 1-3-1 Analysis:**

> The core tension is speed vs. control — a 4-person team needs production analytics by Q3, but the roadmap requires custom event taxonomies that off-the-shelf tools handle poorly. Three approaches scored against 5 weighted criteria. Recommendation: buy Amplitude for standard analytics (ships in 2 weeks) + build a thin custom event layer on the existing warehouse (ships in 8 weeks). Meets the deadline, handles custom taxonomies, preserves migration optionality.

Criteria before options. Three paths evaluated. The recommendation explains *why* and holds up six months later.

**→ Each skill's folder contains a detailed README with methodology and examples.**

---

## Installation

### Claude Projects (claude.ai)

1. Create or open a Project
2. Go to **Project Knowledge**
3. Upload the `SKILL.md` file from each skill folder

### Claude Cowork / Claude Code

```bash
git clone https://github.com/tommy-ngn/skills.git

cp -r skills/1-3-1-analysis ~/.claude/skills/
cp -r skills/1-5-x-analysis ~/.claude/skills/
cp -r skills/deep-research ~/.claude/skills/
cp -r skills/creative-expansion ~/.claude/skills/
cp -r skills/rca ~/.claude/skills/
cp -r skills/problem-framing ~/.claude/skills/
```

### Other Platforms (Cursor, Codex, etc.)

Each skill is a self-contained `SKILL.md` — a structured methodology any AI platform can follow. Add the content to your system prompt or project context.

---

## License

MIT — use, modify, and distribute freely.

## Author

**Tommy Nguyen** — building AI-native thinking workflows for product teams. These skills are part of a broader system for using AI as a rigorous partner across decisions, research, strategy, and communication.
