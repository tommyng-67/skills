---
name: linkedin-infographic
description: >
  Create publish-ready LinkedIn infographics as single-image HTML with PNG
  export. Three visual formats: Myth-Busting Reframe, One Insight, and X vs Y
  Comparison. Use this skill whenever the user mentions "infographic", "single
  image post", "myth bust", "one insight", "X vs Y", "comparison infographic",
  "make an infographic about", "visual post", "scroll-stopper", or any request
  for a single-image LinkedIn visual that is NOT a multi-slide carousel.
  Handles visual design and HTML generation — pair with your own content
  drafting workflow for best results. Always use this over generic HTML/image
  skills for any LinkedIn infographic work.
---

# LinkedIn Infographic Skill

## How This Skill Works

This skill generates publish-ready LinkedIn infographics as self-contained HTML files with a one-click PNG download button. Each infographic is a single 1080x1350 image (4:5 portrait, the highest-reach single-image ratio on LinkedIn).

This is a **design engine**. It takes your content (headline, body sections, bottom line) and produces a designed, export-ready infographic. You provide the content — either directly in your prompt or via a content spec document.

**Before every session:** Read `references/infographic-engine.md` — it contains the complete HTML/CSS/JS generation system plus all design tokens.

---

## 1. Format Selection

Map your content to a visual template:

| Content Type | Format | Engine Template |
|---|---|---|
| Contrarian reframe, myth vs reality | **Myth-Busting Reframe** | `myth-bust` |
| Single stat or insight with context | **One Insight** | `one-insight` |
| Two approaches compared side by side | **X vs Y Comparison** | `x-vs-y` |

**Auto-detection:** If the content doesn't specify a format, infer from the structure. Myth-vs-reality framing = Myth-Bust. Bold number/stat = One Insight. Side-by-side comparison = X vs Y. Default: Myth-Bust.

---

## 2. Brand Configuration

Customize these defaults for your personal brand. Replace the values below with your own:

```
DISPLAY_NAME   = Your Name           (on creator badge)
HANDLE         = @yourhandle
CREATOR_SUB    = {topic-specific}    (e.g. "Product & Growth", "AI & Engineering")
PRIMARY_COLOR  = #3d8b8a             (sage teal — see Color System below)
ASPECT_RATIO   = 4:5 portrait
DIMENSIONS     = 1080 x 1350px (preview: 540 x 675px, export at scale 2)
FONT_VIBE      = Editorial serif + clean sans (Newsreader + Public Sans + JetBrains Mono)
```

The `CREATOR_SUB` line on the creator badge should match the infographic's topic. Keep it under 4 words.

**CTA examples** (adapt to your topic):

- Frameworks/product: "Follow for frameworks that actually ship."
- Growth/tactics: "Follow for growth tactics that work."
- AI/tools: "Follow for AI insights worth saving."
- Story/case study: "Follow for lessons from the trenches."

### Color System (derived from PRIMARY_COLOR #3d8b8a)

The skill ships with a default **sage teal** palette — distinctive in the LinkedIn feed without being polarizing. To use your own brand color, re-derive the full palette using the rules in `infographic-engine.md` Section 1.

```
CORE        = #3d8b8a              Primary accent (sage teal)
CORE_SOFT   = rgba(61,139,138,0.12) Subtle fill backgrounds, tag chips
CORE_LIGHT  = #6abfbe              Secondary accent on dark slides
CORE_DEEP   = #1a5c5b              Gradient anchor, high-contrast text on light slides
CANVAS      = #F3F6FA              Light background (cool off-white)
CANVAS_RULE = #E0E6EE              Dividers, borders on light backgrounds
INK         = #0D1421              Dark background (cool near-black)
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

## 3. Workflow

### Step 1: Map Content to Visual Template

Read the content spec or user prompt. Identify the format and validate that the content contains all required fields:

| Field | Required | Description |
|---|---|---|
| format | Yes | myth-bust / one-insight / x-vs-y |
| eyebrow | Yes | Uppercase label (e.g., "THE MYTH", "SEGMENTATION") |
| headline | Yes | 8-12 words, the scroll-stopper |
| sub_headline | No | Secondary line (myth-bust: "THE REALITY" reframe) |
| body_sections | Yes | Content blocks (rows, bullets, comparisons) adapted per format |
| bottom_line | Yes | One-line thesis anchor or insight summary |
| creator_subtitle | Yes | Topic label for creator badge (under 4 words) |

If any required field is missing, flag it before proceeding.

Select the visual format (myth-bust, one-insight, or x-vs-y) based on the content structure. Present the visual plan before generating HTML.

### Step 2: Generate HTML

Read `references/infographic-engine.md` and follow it precisely. Output: a single `.html` file with embedded PNG download button.

---

## 4. Visual Quality Gates

### The 3-Second Scroll-Stop Test

1. **Headline readable at thumbnail size?** Must be parseable on a phone screen without zooming. If it needs the body text to make sense, rewrite.
2. **Self-identification in 3 seconds?** The reader should think "this is about a mistake I might be making," not "this is about [generic topic]."
3. **Curiosity gap present?** The infographic delivers one insight but implies more lives on your profile.

### Audience Breadth Test

Would your target segments all parse the headline instantly? If any segment struggles, the headline is too jargon-heavy.

---

## 5. Output Checklist

Before delivering, verify:

- [ ] Correct format template used (myth-bust / one-insight / x-vs-y)
- [ ] 4:5 portrait aspect ratio (540x675 preview, 1080x1350 export)
- [ ] Headline passes 3-Second Scroll-Stop Test
- [ ] Passes Audience Breadth Test
- [ ] Creator badge present (bottom area)
- [ ] Decorative elements present (no flat backgrounds)
- [ ] PNG download button functional
- [ ] Google Fonts load before download (400ms+ wait in html2canvas)
- [ ] Post-render content check: open the HTML, visually confirm all content spec text rendered correctly (no truncation, no placeholder text, no missing sections)

---

## 6. File Naming

```
infographic-myth-[slug].html          (Myth-Busting Reframe)
infographic-insight-[slug].html       (One Insight)
infographic-xvy-[slug].html           (X vs Y Comparison)
```
