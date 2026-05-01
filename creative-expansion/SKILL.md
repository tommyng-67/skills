---
name: creative-expansion
description: >
  Break tunnel vision and expand the solution space through structured divergent thinking.
  Uses 7 expansion moves — assumption inversion, constraint removal, analogical transfer,
  edge-case amplification, perspective rotation, time-horizon shift, scale inversion — to
  generate new directions. Output is DIRECTIONS, not decisions (use 1-5-X to converge).
  Trigger on: "think outside the box", "what am I missing", "explore options", "I'm stuck",
  "expand my thinking", "what else could we do", "brainstorm", "more ideas", "tunnel vision",
  "blind spots", "what are we not seeing", "creative-expansion", "fresh perspective",
  "lateral thinking", "divergent thinking", "open it up", or any situation where the user
  seems locked into one approach. Do NOT trigger for: decisions (use 1-5-X), fast decisions
  (use 1-3-1), or research (use deep-research).
---

# Creative Expansion

**Frame the real challenge → Run 7 expansion moves → Cluster into directions → Hand off to convergence.**

This skill exists for one purpose: to make the solution space bigger before the user narrows it down. It's the opposite of deciding. It's the thing you do *before* deciding, when you suspect you haven't seen enough options yet.

---

## When to Use This Skill

The user is **stuck, narrowing too early, or only seeing one path.** They need more options on the table — not a recommendation.

**Trigger phrases:** "think outside the box", "what am I missing", "explore options", "I'm stuck", "expand my thinking", "what else could we do", "brainstorm", "more ideas", "tunnel vision", "blind spots", "what are we not seeing", "creative-expansion", "fresh perspective", "lateral thinking", "open it up", "widen the aperture"

**Also trigger when** the user hasn't asked for expansion but is clearly locked in — they've been iterating on one approach and haven't considered alternatives, or their framing is suspiciously narrow.

| | **Creative Expansion** (this skill) | **1-5-X** | **1-3-1** | **Deep Research** |
|---|---|---|---|---|
| **Purpose** | Expand the solution space | Decide between approaches | Decide fast | Understand a topic |
| **Output** | 3–5 directions to explore | Top 3 ranked with scoring | 1 recommendation | Findings and insights |
| **Mindset** | Divergent — more is better | Convergent — best wins | Convergent — fastest path | Investigative — truth wins |
| **When** | Before you're ready to decide | When you have options to evaluate | When you need a quick call | When you need to learn first |
| **Handoff** | → 1-5-X or 1-3-1 | ← from Creative Expansion | ← from Creative Expansion | ← can feed into any |

**The pipeline:** Creative Expansion → 1-5-X (or 1-3-1) → Execute. This skill is Step 1.

---

## Default Output

Run all steps internally. In chat, print only **Step 3 (Directions)** — the 3–5 clustered directions with what each challenges, what each unlocks, and the handoff prompt. No step labels, no headers, no expansion move breakdowns in chat. Write it as energized, direct prose — each direction should feel like a door opening, not a report section.

If the user explicitly asks to save the full expansion (e.g., "save this," "write the full analysis"), create a `creative-expansion-[topic-slug].md` file in the workspace/outputs folder with all steps, all expansion moves, and the clustering logic.

---

## Step 1: Frame the Real Challenge

The expansion is only as good as the framing. A badly framed challenge produces creative answers to the wrong question. This step borrows from 1-5-X's problem framing but bends it toward creative exploration rather than decision-making.

### 1a: What's the user actually stuck on?

The stated problem is often a symptom or a premature solution. Dig one level deeper. "We need a better onboarding flow" might really be "new users don't understand why this product exists." "How do I grow my newsletter?" might really be "I don't know who my newsletter is for."

Restate the challenge as a **"How might we..."** question. This is deliberate — "How might we..." is open-ended by design. It implies many possible answers and no predetermined path. It's the framing that makes divergent thinking possible.

If the challenge has multiple valid framings, name 2–3 and pick the one that opens the widest creative aperture. Tell the user which framing you chose and why.

### 1b: Surface the hidden assumptions

Every stuck point has assumptions holding it in place. Name 3–5 assumptions the user is currently operating under — things they're treating as fixed that might not be. These become the raw material for the expansion moves.

Types of assumptions to look for:

- **Audience assumptions** — "Our users are X" (but are they? all of them?)
- **Constraint assumptions** — "We can't do Y" (says who? is that truly immovable?)
- **Solution assumptions** — "The answer involves Z" (does it have to?)
- **Success assumptions** — "Good looks like W" (by whose definition?)
- **Timing assumptions** — "This needs to happen now/fast/before X" (what if it didn't?)

Don't judge the assumptions — just surface them. The expansion moves will do the challenging.

### 1c: Map the current solution space

Briefly describe the options the user has already considered (or the single path they're locked into). This is the "before" snapshot — it shows how narrow the current thinking is and gives the expansion moves something concrete to push against.

---

## Step 2: Run the Expansion Moves

Each expansion move is a **named creative lens** that forces thinking in a direction the user's current frame makes invisible. Run all 7. Each move produces 1–3 new options that didn't exist before.

The moves are designed to be complementary — they attack different blind spots. Some will produce breakthrough ideas, others will produce duds. That's expected. The point is to generate volume and variety, not to filter.

### Move 1: Assumption Inversion

Take each assumption from Step 1b and ask: **"What if the exact opposite were true?"**

- "Our users are enterprise buyers" → What if the real user is the individual contributor who never talks to sales?
- "This has to be a software solution" → What if the answer is a service, a process change, or doing nothing?
- "We need to move fast" → What if moving slowly and deliberately is the actual advantage?

Don't evaluate whether the inversions are practical yet. Some will be absurd — that's the point. Absurd inversions often contain a kernel of insight that leads to a practical option nobody had considered.

### Move 2: Constraint Removal

Ask: **"If [constraint] didn't exist, what would we do?"**

Take each binding constraint (budget, timeline, team size, technology, regulation, organizational politics) and temporarily delete it. Not to fantasize, but to reveal the *shape* of the ideal solution. Once you see the shape, you can often find a way to approximate it within the actual constraints.

- "If we had unlimited engineering time..." → reveals what the team actually wants to build
- "If there were no legacy system to maintain..." → reveals how much the current architecture is distorting the solution
- "If we didn't care about this quarter's numbers..." → reveals the long-term play being sacrificed

### Move 3: Analogical Transfer

Ask: **"What domain has already solved a problem shaped like this — and what did they do?"**

Pull from domains that are structurally similar but superficially unrelated. The further the analogy, the more novel the solution — but it has to be structurally valid, not just a cute metaphor.

- Marketplace growth problem? → How did early telephone networks solve the chicken-and-egg?
- User retention problem? → How do gyms, games, or religions maintain long-term engagement?
- Pricing challenge? → How do airlines, auctions, or street vendors handle the same tension?

Name the source domain, the structural parallel, and the specific mechanism that transfers.

### Move 4: Edge-Case Amplification

Ask: **"What if we designed for the weirdest 5% instead of the average user?"**

Mainstream thinking optimizes for the center of the bell curve. But the edges often reveal unmet needs, emerging behaviors, and opportunities that the mainstream will eventually adopt.

- Who is the most extreme user of this product? What do they need?
- Who is using this product in a way you never intended? What are they trying to accomplish?
- What's the smallest viable version of this? The most absurdly ambitious version?
- Who would benefit from this if it were 10x more expensive? 10x cheaper? Free?

### Move 5: Perspective Rotation

Ask: **"How would [someone with a completely different worldview] approach this?"**

Rotate through perspectives that would see the challenge fundamentally differently:

- **The competitor** — How would they exploit the opening you're leaving?
- **The skeptic** — Why is this problem not worth solving at all?
- **The newcomer** — Someone with no industry knowledge. What obvious thing would they try that insiders dismiss?
- **The end user's user** — Not your customer, but your customer's customer. What do *they* need?
- **The person in 2030** — Looking back, what will seem obvious that you're missing now?

Pick 2–3 perspectives that create the most contrast with the user's current viewpoint.

### Move 6: Time-Horizon Shift

Ask: **"What changes if you zoom out to 5 years — or zoom in to this week?"**

Most people are stuck at one time scale. Shifting the horizon reveals different strategic options:

- **Zoom out (3–5 years):** What's the version of this that compounds? What would you build if you were playing an infinite game, not a finite one? What decision today would give you the most optionality in 3 years?
- **Zoom in (this week):** What's the smallest thing you could do in 48 hours to learn something? What's the "ugly prototype" that tests the core assumption? What would you do if this had to ship Friday?

The zoom-out often reveals that the user is solving a tactical problem when they need a strategic one (or vice versa).

### Move 7: Scale Inversion

Ask: **"What if you did this at 100x the scale — or 1/100th?"**

Changing the scale of the problem often changes its nature entirely:

- **100x scale:** What breaks at 100x? What works *better* at 100x? (Network effects, economies of scale, data advantages.) If 100x scale is the goal, does the current approach even make sense as a starting point?
- **1/100th scale:** What does this look like as an artisanal, handcrafted, zero-automation version? Sometimes the smallest-scale version reveals the *essence* of the value proposition — what you'd keep if you had to strip away everything else.
- **Zero:** What if you stopped doing this entirely? What would happen? (Sometimes the answer is "nothing," which means this isn't the right problem.)

---

## Step 3: Cluster into Directions

Now synthesize. The 7 expansion moves will have generated 10–20+ raw options, many overlapping, some contradictory, some brilliant, some useless. The job is to cluster them into **3–5 genuinely distinct directions** — each representing a fundamentally different path forward.

### How to cluster:

Group options that share a common strategic logic — not by which expansion move produced them, but by the *kind of bet* they represent. A good direction answers: "If we went this way, what would we be betting on?"

### For each direction:

**Name it** — a short, evocative label that captures the strategic bet. Not "Option A" but "Go upstream" or "Burn the playbook" or "Serve the edges first."

**Describe it** in 2–3 sentences — what this direction looks like in practice. Concrete enough that the user can picture it, not so detailed that it becomes a plan (planning comes later).

**Which assumptions it challenges** — connect back to Step 1b. Every direction should challenge at least one assumption. If a direction doesn't challenge any assumptions, it's probably not a new direction — it's a variant of what the user was already considering.

**What it unlocks** — what new possibilities does this direction create? What doors open if you go this way? Second-order effects matter here.

**What it risks** — one sentence on what you'd be giving up or betting against. Not a full risk assessment (that's 1-5-X's job), just enough to see the tradeoff.

### The handoff:

After presenting the directions, close with: **"Ready to converge? Run 1-5-X on these directions to evaluate and decide."**

This makes the pipeline explicit. Creative Expansion opens the space. 1-5-X narrows it. They're complementary tools, not competing ones.

---

## Formatting & Style

**Chat response** (what the user sees):
- The "How might we..." reframe (1 sentence)
- The 3–5 directions, each with: name, description, what it challenges, what it unlocks, what it risks
- The handoff prompt
- No step labels, no expansion move breakdowns, no headers heavier than the direction names
- Tone: energizing, not bureaucratic. This should feel like a creative conversation, not a consulting deck. Short sentences. Active verbs. Surprise the user.

**The .md file** (only when explicitly requested):
- All steps: framing, assumptions, current solution space, all 7 expansion moves with their outputs, clustering rationale, final directions
- Use headers to separate steps and moves
- Same writing standards as the rest of the skill ecosystem: no jargon without clarification, no filler, no corporate speak
