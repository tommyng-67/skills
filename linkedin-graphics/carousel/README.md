# LinkedIn Carousel

A design engine that turns your content into publish-ready LinkedIn carousel posts — with swipeable preview, per-slide PNG export, and one-click PDF download for LinkedIn upload.

---

## What It Does

Give it your slide content (a hook, key points, a CTA) and it generates a single self-contained HTML file with:

- **10 designed slides** at 1080x1080px (alternating dark/light for visual rhythm)
- **Swipeable LinkedIn-style preview** with dot indicators and drag navigation
- **Per-slide PNG download** buttons + "Download All" batch export
- **One-click PDF assembly** via jsPDF — upload directly to LinkedIn as a document post
- **Full design system** built in: typography scale, color tokens, decorative elements, component library

Every slide gets decorative elements (dot grids, gradient circles, concentric rings) — no flat backgrounds. Every content slide leads with a visual component (diagrams, contrast grids, icon rows, comparison tables) — not walls of text.

## What It Doesn't Do

This is a visual design engine, not a copywriter. It takes your content and makes it look great. For best results, draft your content first (hook, narrative arc, slide-by-slide copy), then hand it to this skill for design.

---

## Quick Start

### Claude Cowork / Claude Code

```bash
# Clone this repo
git clone https://github.com/tommy-ngn/skills.git

# Copy the skill to your Claude skills directory
cp -r skills/linkedin-carousel ~/.claude/skills/
```

Then tell Claude: *"Make a carousel about [your topic]"*

### Claude Projects (claude.ai)

1. Create or open a Project
2. Go to **Project Knowledge**
3. Upload `SKILL.md` and `references/carousel-engine.md`

### Other Platforms

The skill is two markdown files. Add the content of `SKILL.md` and `references/carousel-engine.md` to your system prompt or project context.

---

## Customization

### Brand Colors

The skill ships with a **sage teal** default palette. To use your own brand color, update the `PRIMARY_COLOR` in `SKILL.md` and the skill will auto-derive a full 7-token palette:

```
PRIMARY_COLOR = #your-hex-color
```

The color derivation rules are in `references/carousel-engine.md` Section 1.

### Brand Identity

Update these in `SKILL.md` Section 2:

```
DISPLAY_NAME  = Your Name
HANDLE        = @yourhandle
CREATOR_SUB   = Your Topic Area
```

### Typography

Default: Newsreader (headings) + Public Sans (body) + JetBrains Mono (labels). Four alternative pairings are documented in the engine for different vibes (sharp/technical, bold/expressive, warm/human, clean/modern).

---

## Carousel Types

| Type | When to use |
|---|---|
| **Analytical Breakdown** | Expose a mistake or flawed model, then reframe |
| **Listicle** | Curated list of tools, tactics, lessons |
| **How-To / Process** | Step-by-step walkthrough or playbook |
| **Myth-Bust / Reframe** | Challenge conventional wisdom with evidence |
| **Comparison** | X vs Y, before/after, old way vs new way |
| **Story / Case Study** | Narrative arc with a lesson |

---

## Component Library

The design engine includes a full component library for building visually rich slides:

**Structural:** Convergence diagrams, segment-to-product rows, two-column contrast grids, icon grids

**Data & emphasis:** Big stat callouts, comparison tables, feature boxes

**Text-forward:** Mono-rows, SVG-icon rows, numbered steps, quote blocks, checklists

**Callouts:** Move-up callouts, emphasis callouts, level contrast blocks, strikethrough pills

Every component has dark-slide and light-slide variants with full HTML/CSS specs.

---

## File Structure

```
linkedin-carousel/
├── SKILL.md                         # Skill instructions + brand config
├── README.md                        # This file
└── references/
    └── carousel-engine.md           # Complete HTML/CSS/JS generation spec
```

---

## License

MIT — use, modify, and distribute freely.
