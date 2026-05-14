# LinkedIn Graphics

A design system that turns your content into publish-ready LinkedIn visuals — carousels and infographics — with built-in typography, color tokens, component libraries, and one-click export.

---

## Two Skills, One Design Language

| Skill | Format | Output | When to use |
|---|---|---|---|
| [**Carousel**](./carousel/) | 10 slides, 1080x1080px | Swipeable HTML + PNG/PDF export | Multi-slide breakdowns, listicles, how-tos, case studies |
| [**Infographic**](./infographic/) | Single image, 1080x1350px (4:5) | HTML + PNG export | Myth-busts, single insights, X vs Y comparisons |

Both skills share the same design language: Newsreader + Public Sans + JetBrains Mono typography, a 7-token color system, decorative elements on every surface, and a creator badge. Each is fully self-contained — use one or both.

---

## Quick Start

### Claude Cowork / Claude Code

```bash
git clone https://github.com/tommy-ngn/skills.git

# Install both
cp -r skills/linkedin-graphics/carousel ~/.claude/skills/
cp -r skills/linkedin-graphics/infographic ~/.claude/skills/

# Or just one
cp -r skills/linkedin-graphics/carousel ~/.claude/skills/
```

Then tell Claude: *"Make a carousel about [topic]"* or *"Make an infographic about [topic]"*

### Claude Projects (claude.ai)

1. Create or open a Project
2. Go to **Project Knowledge**
3. Upload the `SKILL.md` and `references/*.md` files from whichever skill you want

### Other Platforms (Cursor, Codex, etc.)

Each skill is two markdown files. Add the content of `SKILL.md` and its `references/*.md` to your system prompt or project context.

---

## Customization

Both skills ship with identical default design tokens. Customize once, apply to both.

### Brand Color

Default: **sage teal** (`#3d8b8a`). To use your own brand color:

1. Pick your hex color
2. Update `PRIMARY_COLOR` in each skill's `SKILL.md`
3. Re-derive the 7-token palette using these rules:

```
CORE        = your hex color
CORE_SOFT   = your color at 12% opacity
CORE_LIGHT  = 40% lighter (secondary accent on dark backgrounds)
CORE_DEEP   = 40% darker (gradients, high-contrast text on light backgrounds)
CANVAS      = cool off-white (light background)
CANVAS_RULE = subtle gray (dividers on light backgrounds)
INK         = cool near-black (dark background)
```

### Brand Identity

Update in each skill's `SKILL.md`:

```
DISPLAY_NAME  = Your Name
HANDLE        = @yourhandle
CREATOR_SUB   = Your Topic Area
```

### Typography

Default: Newsreader (headings) + Public Sans (body) + JetBrains Mono (labels). All loaded via Google Fonts CDN. The carousel engine documents four alternative pairings for different vibes (sharp/technical, bold/expressive, warm/human, clean/modern).

---

## How It Works

Each skill is a **design engine** — it takes your content and produces beautiful, consistent HTML with export capabilities. You provide the content (headlines, body copy, narrative arc), the engine handles typography, color, layout, components, and decorative elements.

The design floor is high enough that even the worst output looks professional. Every surface has decorative elements (no flat backgrounds), every content element has a visual component, and the full design system is baked into the generation spec.

**Output:** Self-contained HTML files. Open in a browser, preview the design, export as PNG (infographic) or PNG/PDF (carousel) for direct LinkedIn upload.

---

## File Structure

```
linkedin-graphics/
├── README.md                              # This file
├── carousel/
│   ├── SKILL.md                           # Carousel skill instructions + brand config
│   ├── README.md                          # Carousel-specific docs
│   └── references/
│       └── carousel-engine.md             # Complete carousel HTML/CSS/JS spec
└── infographic/
    ├── SKILL.md                           # Infographic skill instructions + brand config
    ├── README.md                          # Infographic-specific docs
    └── references/
        └── infographic-engine.md          # Complete infographic HTML/CSS/JS spec
```

---

## License

MIT — use, modify, and distribute freely.
