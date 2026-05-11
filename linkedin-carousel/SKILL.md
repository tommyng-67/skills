---
name: linkedin-carousel
description: >
  Create publish-ready LinkedIn carousel posts as swipeable HTML with per-slide
  PNG download and LinkedIn-uploadable PDF assembly. Use this skill whenever
  the user mentions "carousel", "slides", "LinkedIn carousel", "slide deck for
  LinkedIn", "carousel about [topic]", or any request to create multi-slide
  LinkedIn content. Also trigger when the user says "make a carousel from this
  post", "turn this into slides", or "visual content for LinkedIn". Handles
  visual design and HTML generation — pair with your own content drafting
  workflow for best results. Always use this over generic HTML/presentation
  skills for any LinkedIn carousel work.
---

# LinkedIn Carousel Skill

## How This Skill Works

This skill generates fully designed, publish-ready LinkedIn carousels as a single self-contained HTML file. Every carousel includes a swipeable LinkedIn-style preview, per-slide PNG download buttons, a "Download All" option, and a "Download PDF" button for LinkedIn-uploadable PDF assembly using jsPDF.

This is a **design engine**. It takes your content (slide copy, narrative arc) and produces beautiful, consistent carousel HTML. You provide the content — either directly in your prompt or via a content spec document.

**Before every session:** Read `references/carousel-engine.md` — it contains the complete HTML/CSS/JS generation system plus all design tokens.

---

## 1. Carousel Types

Every carousel has a narrative type that shapes its visual arc, component selection, and pacing. Pick the type that fits your content, then follow its arc in `carousel-engine.md` Section 7.

| Type | When to use | Example cover hook |
|---|---|---|
| **Analytical Breakdown** | Expose a common mistake or flawed mental model, then reframe | "Most teams segment by demographics. That's why their roadmaps fail." |
| **Listicle** | Curated list of tools, tactics, lessons, or resources | "9 AI tools I actually use every week (not the ones everyone recommends)" |
| **How-To / Process** | Step-by-step walkthrough, playbook, or setup guide | "How I set up Claude to write production code in 20 minutes" |
| **Myth-Bust / Reframe** | Challenge conventional wisdom with evidence | "You don't need 10K followers to launch a product. Here's why." |
| **Comparison** | X vs Y, before/after, old way vs new way | "Junior PMs build features. Senior PMs build systems. Here's the difference." |
| **Story / Case Study** | Narrative arc with a business or personal lesson | "I mass-produced dashboards for 6 months. Nobody looked at them." |

**Auto-detection:** If the content doesn't specify a type, infer from the narrative arc. Two-act rug-pull = Analytical Breakdown. Step-by-step = How-To. Contrarian claim = Myth-Bust. Default: Analytical Breakdown.

---

## 2. Brand Configuration

Customize these defaults for your personal brand. Replace the values below with your own:

```
DISPLAY_NAME   = Your Name           (on creator badge)
HANDLE         = @yourhandle
CREATOR_SUB    = {topic-specific}    (e.g. "Product & Growth", "AI & Engineering")
PRIMARY_COLOR  = #3d8b8a             (sage teal — see Color System below)
FONT_VIBE      = Editorial serif + clean sans (Newsreader + Public Sans + JetBrains Mono)
SLIDE_COUNT    = 10 (default; 8-12 range)
```

The `CREATOR_SUB` line on the creator badge should match the carousel's topic. Keep it under 4 words.

**CTA examples** (adapt to your topic):

- Frameworks/product: "Follow for frameworks that actually ship."
- Growth/tactics: "Follow for growth tactics that work."
- AI/tools: "Follow for AI insights worth saving."
- Story/case study: "Follow for lessons from the trenches."

### Color System (derived from PRIMARY_COLOR #3d8b8a)

The skill ships with a default **sage teal** palette — distinctive in the LinkedIn feed without being polarizing. To use your own brand color, re-derive the full palette using the rules in `carousel-engine.md` Step 1.

```
CORE        = #3d8b8a              Primary accent (sage teal)
CORE_SOFT   = rgba(61,139,138,0.12) Subtle fill backgrounds, tag chips
CORE_LIGHT  = #6abfbe              Secondary accent on dark slides
CORE_DEEP   = #1a5c5b              Gradient anchor, high-contrast text on light slides
CANVAS      = #F3F6FA              Light slide background (cool off-white)
CANVAS_RULE = #E0E6EE              Dividers, borders on light slides
INK         = #0D1421              Dark slide background (cool near-black)
```

### Typography

```
HEADING_FONT = Newsreader (weights 600, 700, 800; optical sizing enabled)
BODY_FONT    = Public Sans (weights 400, 500, 600, 700)
MONO_FONT    = JetBrains Mono (weights 400, 500, 600)
```

Import:

```css
@import url('https://fonts.googleapis.com/css2?family=Newsreader:ital,opsz,wght@0,6..72,400;0,6..72,600;0,6..72,700;0,6..72,800;1,6..72,400&family=Public+Sans:ital,wght@0,400;0,500;0,600;0,700;1,400&family=JetBrains+Mono:wght@400;500;600&display=swap');
```

---

## 3. Visual-First Design Principles

Every content slide should lead with a visual mechanism, not walls of text. The component library in `carousel-engine.md` Section 5 includes:

**Structural components (diagrams & layouts):**
- Convergence diagrams, segment-to-product rows, two-column contrast grids, icon grids

**Data & emphasis components:**
- Big stat callouts, comparison tables, feature boxes

**Text-forward components (use sparingly):**
- Mono-rows, SVG-icon rows, numbered steps, quote blocks, checklist rows

**Callouts & accents:**
- Move-up callouts, emphasis callouts, level contrast blocks, strikethrough pills

See `carousel-engine.md` Section 5 for full HTML/CSS specs of each component.

---

## 4. Workflow

### Step 1: Map Content to Visual Arc

Read the content spec or user prompt. Identify the carousel type and map each slide to a visual component. Present the visual plan:

```
SLIDE 1 (Cover / Gradient): [Hook headline + subtitle + creator badge]
SLIDE 2 (Setup / INK): [Component: two-column contrast grid]
SLIDES 3 to N-2 (Alternating INK/CANVAS): [Component per slide]
SLIDE N-1 (Summary / INK): [Comparison table or checklist rows]
SLIDE N (CTA / Gradient): [CTA + creator badge + save prompt]
```

Wait for approval before generating HTML.

### Step 2: Generate the HTML Carousel

Read `carousel-engine.md` and follow it precisely. The output is a single self-contained `.html` file that includes:

1. **LinkedIn preview frame** (540px wide, swipeable, dot indicators, page label, action bar)
2. **All slides** (540x540px preview, 1080x1080px export via html2canvas scale:2)
3. **Download panel** (per-slide PNG buttons + "Download All" + "Download PDF" via jsPDF)
4. **Slide counter** on every slide (bottom-left)
5. **Swipe arrow** on every slide except the last
6. **Decorative elements** on every slide (circles, dot grids, gradients — no flat backgrounds)
7. **Save prompt** on CTA slide only
8. **Custom SVG icons and infographics** on content slides

---

## 5. Output Checklist

Before delivering, verify:

- [ ] Cover has a specific, debatable hook (not a topic title)
- [ ] Every content slide leads with a visual element — not walls of text
- [ ] Every slide has at least one decorative element (no flat backgrounds)
- [ ] Text never overlaps slide counter (bottom 44px reserved)
- [ ] Light/dark slides alternate for visual rhythm
- [ ] Dot indicators present and functional below viewport
- [ ] Download panel present with per-slide buttons + Download All + Download PDF
- [ ] Slide counter format: `01 / 10` (zero-padded)
- [ ] No swipe arrow on final slide
- [ ] Save prompt on CTA slide only
- [ ] Creator badge on cover and CTA slides
- [ ] Summary slide has visual design weight (table or left-rule bullets)
- [ ] Google Fonts load before download (350ms+ wait in html2canvas calls)
- [ ] PDF download button uses jsPDF inline (no separate script needed)
- [ ] All content rendered correctly (no truncation, no placeholder text, no missing slides)

---

## 6. File Naming

```
carousel-[slug].html
```
