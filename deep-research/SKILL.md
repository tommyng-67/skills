---
name: deep-research
description: >
  Deep-dive research on any topic: trends, technologies, concepts, markets, competitors, frameworks,
  or any subject requiring thorough multi-source investigation. Use this skill whenever the user wants
  to understand a topic in depth — not make a decision (use 1-5-X or 1-3-1 for that). Triggers on:
  "research this", "look into", "what is [unfamiliar term]", "deep dive on", "what's the latest on",
  "explain [concept]", "investigate", "find out about", "how does [X] work", "what do we know about",
  or any request where the user wants to learn rather than decide.
---

# Deep Research

Structured research methodology. Six phases: **Scope → Search → Refine Outline → Triangulate → Synthesize → Package.**

Execution model: parallel subagents, one per dimension, each using `agent-browser` as the primary search tool. A dedicated verification subagent runs in Phase 4. Main agent synthesizes all briefs.

---

## When to Use This Skill

The user wants to **understand a topic** — not make a decision. They want depth, sources, and insights on a subject.

**Trigger phrases:** "research this", "look into", "what is [term]", "deep dive on", "what's the latest on", "explain [concept]", "investigate", "find out about", "how does X work", "what do we know about", or any request where the user wants to learn rather than decide.

| | **Deep Research** (this skill) | **1-5-X** | **1-3-1** |
|---|---|---|---|
| **Purpose** | Understand a topic | Decide between approaches | Decide fast |
| **Trigger** | "research", "look into", "what is X", "explain", "deep dive" | "help me decide", "compare", "which should I", "pros and cons" | User explicitly says "1-3-1" |
| **Output** | Findings, insights, implications | Top 3 ranked approaches with scoring | Single recommended approach |
| **Approaches** | N/A | 5+ | Exactly 3 |
| **Recommendations** | N/A | Multiple (often hybrid) | Exactly 1 |
| **Depth** | Exhaustive topic coverage | Exhaustive option analysis | Faster, lighter-weight |

---

## Phase 1: Scope

Before searching, define what you're investigating. Context shapes how findings are interpreted (Phase 5b), but never which evidence is sought.

**1a: Quarantine the user's context.**

- **If the user provides context** (e.g., "researching agentic AI because I'm evaluating whether to build our PM workflow on it"): record it in a **Context Note** — a separate block that captures the user's situation, goals, and any embedded hypotheses or assumptions. **Do not reference the Context Note until Phase 5b.** It does not influence dimensions, search queries, or evidence assessment. It exists solely for the interpretation layer.
- **If the user provides no context**: no Context Note. Proceed without one.

> **Context Note: [record user's stated context, goals, and embedded hypotheses here]**

The principle: context is a **lens** (shapes what findings mean for the user), not a **filter** (shapes what evidence gets collected). Filtering creates confirmation bias. Interpreting creates relevance.

**1b: Restate the research question.** Sharpen the user's request into a precise, context-neutral question about the topic itself. The question should be one that any researcher — regardless of the user's specific situation — would ask.

- With context: "researching agentic AI for our PM workflow" → research question is still "What are the current architectures, toolchains, limitations, and production use cases of agentic AI systems?" — NOT "What agentic AI tools work for PM workflows?" The context narrows interpretation later, not the research aperture now.
- Without context: same process. "Research agentic AI" → same question.

**1c: Identify dimensions.** Derive dimensions from **the topic's natural structure**, not the user's framing. Every topic has 3–6 dimensions. Map them before searching — they become your search plan.

- A **technology**: what it is, how it works, current state, key players, adoption, limitations, trajectory
- A **trend**: origin, drivers, current data, who's affected, implications, counter-arguments
- A **concept**: definition, history, key frameworks, applications, criticisms, adjacent concepts
- A **market**: size, growth, segments, key players, dynamics, risks

**Mandatory dimension: "Limitations, failures, and criticisms."** This dimension is required for every research topic, regardless of context. It cannot be skipped, merged, or deprioritized. It ensures disconfirming evidence enters the pipeline structurally — not as an afterthought.

**1d: Set depth.** Based on the question's complexity:

- **Standard** (default): 15–20 browser searches across all dimensions. Covers each dimension with 2–3 credible sources.
- **Deep**: 20–30 browser searches. Cross-references across sources, reads full articles, surfaces conflicting viewpoints.

Proceed immediately — do not ask the user to confirm scope.

---

## Phase 2: Search

Spawn **one subagent per dimension** from Phase 1. Each subagent uses `agent-browser` as its primary search tool:

1. Invoke `agent-browser` to run 3–5 searches targeting its assigned dimension from varied angles (definitional, current state, critical, comparative, applied). Instruct agent-browser to: search Google, follow the 2–3 most promising results, read full article content, and return findings with URLs.
2. For known high-value URLs (official docs, GitHub repos, specific reports), use `web_fetch` directly — faster than agent-browser for targeted retrieval of a known source.
3. Use agent-browser (not web_fetch) for: open-ended searches, JavaScript-heavy pages, paginated content, sites requiring scrolling or interaction to reveal full content.
4. Write a **dimension brief** in this format:

```
## [Dimension Name]
### Top findings (3–5 bullets, each with source attribution)
### Sources used (name, URL, credibility tier — see Phase 4)
### Gaps (what couldn't be found or remains unclear)
```

5. Save the brief to a local file (e.g., `dimension_1_brief.md`).

Main agent reads all dimension briefs after subagents complete, then proceeds to Phase 3.

**Subagent coordination rules:**
- Each subagent operates independently — no inter-subagent communication needed.
- If a subagent's dimension yields no useful results after 3 agent-browser searches, it writes a brief stating "No credible sources found" and completes. The gap gets flagged in Phase 6.
- Subagents should avoid overlapping queries. Each subagent owns its dimension exclusively.

**When to stop:** Stop searching when (a) every dimension has at least 2 credible sources, AND (b) new searches return information already found. Uncovered dimensions become knowledge gaps in Phase 6.

---

## Phase 3: Refine Outline

After evidence is gathered but before synthesis, revisit the dimension structure from Phase 1. Evidence often reveals that the initial structure was incomplete, misordered, or included dimensions with no findable information.

**Do:**
- **Add** dimensions the evidence revealed that weren't anticipated. (Example: researching "MCP protocol" — Phase 1 mapped architecture, adoption, tooling. Evidence reveals a significant security/trust dimension not initially scoped. Add it.)
- **Reorder** dimensions by significance based on what the evidence actually shows, not what seemed important before searching.
- **Flag** dimensions with no credible evidence found — these become knowledge gaps in Phase 6 rather than empty sections in the synthesis.
- **Merge** dimensions that turned out to be inseparable in the evidence (e.g., "key players" and "adoption" may be the same story).

**Do not:**
- Search for new evidence in this phase. This is a structural adjustment step, not a second research round.
- Remove dimensions that have evidence just because they seem less interesting. The evidence decides, not intuition.

---

## Phase 4: Triangulate

Before synthesizing, assess what you've found — and calibrate credibility standards to the topic.

### 4a: Assess topic maturity

| Maturity | Characteristics | Examples |
|---|---|---|
| **Established** | Abundant peer-reviewed research, official standards, years of documented practice | Relational databases, supply chain management, behavioral economics |
| **Emerging** | Rapidly evolving, few peer-reviewed sources, most signal lives in practitioner blogs, GitHub repos, conference talks, release notes | LLM applications, agentic AI workflows, MCP protocol, new AI models |
| **Mixed** | Established foundation with an emerging frontier | Cloud infrastructure (established) + serverless edge computing (emerging) |

This classification determines how credibility works in 4b.

### 4b: Source credibility — adaptive by maturity

**For established topics**, apply strict tiers:

| Tier | Source type | Trust level |
|---|---|---|
| **T1** | Official documentation, peer-reviewed research, primary data (SEC filings, gov data, company reports) | High — cite directly |
| **T2** | Reputable journalism (NYT, Bloomberg, Wired, Ars Technica), established analysts (Gartner, a16z) | Medium-high — cite with attribution |
| **T3** | Industry blogs, conference talks, known practitioners | Medium — cite as perspective, not fact |
| **T4** | Forums, social media, anonymous posts, SEO content farms | Low — signal detection only, never as evidence |

**Rule for established topics:** No claim rests solely on T3–T4 sources.

**For emerging topics**, the evidence frontier shifts. Official research and institutional analysis lag behind practitioners who are building, testing, and shipping. Apply adjusted tiers:

| Tier | Source type | Trust level |
|---|---|---|
| **T1-E** | Official project documentation, release notes, GitHub repos from core maintainers, technical RFCs | High — primary source of truth for how things actually work |
| **T2-E** | Named practitioners with demonstrated expertise (shipped products, recognized contributions), company engineering blogs, conference talks with technical depth | Medium-high — cite with attribution. Expertise is established by track record, not job title. |
| **T3-E** | General industry commentary, aggregator coverage, newsletters summarizing others' work | Medium — useful for identifying trends, not for technical claims |
| **T4-E** | Anonymous posts, hype-driven content, SEO listicles, "Top 10 AI tools" articles | Low — noise. Ignore unless corroborated. |

**Rule for emerging topics:** Claims can rest on T2-E sources when **2+ independent practitioners** report the same finding. A single practitioner's experience is an anecdote; three independent practitioners converging on the same observation is a credible signal. Flag any finding backed by a single source as "early signal — limited corroboration."

**For mixed topics:** Apply established-topic tiers to the foundation, emerging-topic tiers to the frontier. State which standard you're applying and why.

### 4c: Cross-verification of key claims

Identify the **5 most important claims** from the research — findings that the user is most likely to act on or cite.

Spawn a **verification subagent**. For each of the 5 claims, the subagent uses `agent-browser` to:

1. Search for independent corroboration from a source **not already cited** in the dimension briefs. Run a targeted search, follow the most credible-looking result, and read the full content.
2. Classify each claim as:
   - **Verified** — independent source confirms. Name the source.
   - **Contradicted** — independent source disputes. Name the source and the discrepancy.
   - **Unverifiable** — no independent source found. Flag as single-source claim.
3. Return a verification report. These classifications feed directly into the synthesis — verified claims are stated with confidence, contradicted claims are presented as tensions, unverifiable claims are flagged.

### 4d: Conflict detection

Where sources disagree, state the disagreement explicitly. Do not silently resolve it. Name the sources, their tiers, and your assessment of why they differ (different timeframes, different use cases, one source is outdated, ideological difference, etc.).

### 4e: Coverage check

Review the refined dimensions from Phase 3. For each dimension, confirm at least 2 independent sources at appropriate tier levels (T1–T2 for established, T1-E–T2-E for emerging). If not, flag the gap.

---

## Phase 5: Synthesize

### 5a: Objective synthesis

Organize findings **by insight, not by source.** The output should read as integrated analysis, not a book report that walks through Source 1, then Source 2, then Source 3.

**Structure by dimension or theme:**
- Use the **refined dimensions from Phase 3** (not the original Phase 1 dimensions) as the organizing structure
- Under each dimension, present the integrated finding — drawing from multiple sources
- Where sources converge, state the finding with confidence
- Where sources conflict, present the tension and your assessment of which is more credible (based on tier)
- Where cross-verification (Phase 4c) flagged a claim as contradicted or unverifiable, state this explicitly
- The mandatory "Limitations, failures, and criticisms" dimension must appear as a full section — not a footnote, not a disclaimer. Findings here carry equal weight to other dimensions.

**Writing standard:**
- Every claim must be attributed (source name, not just a number)
- No filler. No "it's important to note that." No "interestingly."
- Specific over vague: "adoption grew 340% YoY per Gartner 2025" not "adoption is growing rapidly"
- If you don't know something, say so — a gap identified is more valuable than a gap papered over

### 5b: Contextual interpretation (only if Context Note exists)

**Now — and only now — read the Context Note from Phase 1a.** Apply the user's context as an interpretive lens on top of the objective findings from 5a:

- **Relevance mapping:** Which findings matter most given the user's specific situation? Why?
- **Risk surfacing:** What risks are specific to the user's framing that the objective findings make visible? What assumptions in the user's context are challenged by the evidence?
- **Blind spot detection:** What does the evidence suggest the user might be wrong about, or hasn't considered? What questions should they be asking that they haven't asked?
- **Actionable implications:** Given their stated goals, what should they do with these findings?

This section should feel like a trusted advisor interpreting a report — not rewriting it. The objective findings in 5a stand on their own. 5b adds a personalized layer on top.

---

## Phase 6: Package

### Output structure:

**One-line answer** — If the research question has a direct answer, lead with it. One sentence.

**Key findings** (3–7 findings) — The most important things the user should know, ordered by objective significance (not contextual relevance). Each finding is 2–4 sentences: the insight, the evidence, and why it matters. Findings flagged as "early signal" or "unverifiable" in Phase 4c should be marked as such here.

**Detailed analysis** — The full objective synthesis from Phase 5a, organized by refined dimension. The mandatory "Limitations, failures, and criticisms" section appears with equal prominence to other dimensions.

**For your situation** (only if Context Note exists) — The contextual interpretation from Phase 5b. Which findings matter most for the user's specific goals, what risks their framing surfaces, what blind spots the evidence reveals, and what they should do next. This section is clearly separated from the objective findings — the user should see where objective analysis ends and personalized interpretation begins.

**Verification status** — Summary of Phase 4c results: how many of the top claims were verified, contradicted, or unverifiable. Tells the user how much to trust the overall findings.

**Knowledge gaps & caveats** — What couldn't be found, what's uncertain, what's changing fast enough that these findings may have a short shelf life. Include dimensions flagged in Phase 3 as having no credible evidence.

**Sources** — List the sources used, grouped by tier. Lets the user assess credibility at a glance and dig deeper into specific sources.

### Format:

**In-chat:** Print only the **one-line answer**, **key findings**, and **for your situation** (if Context Note exists).

**File:** Always create a `.md` file with the full output (all sections). Save to the workspace outputs folder.

If the user asks for a "quick summary" or "brief," skip the file — print only the one-line answer + key findings in chat.

---

## Style

Every sentence must be self-explanatory to a reader with no prior context. No jargon without immediate clarification. No filler. No corporate speak. Attribute claims to sources. State uncertainty honestly. Prefer specific data over general characterizations.
