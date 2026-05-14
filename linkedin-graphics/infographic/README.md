# LinkedIn Infographic

A design engine that turns your content into publish-ready LinkedIn infographics — single-image 4:5 portrait format with one-click PNG export for direct LinkedIn upload.

---

## What It Does

Give it your content (a headline, body sections, bottom line) and it generates a single self-contained HTML file with:

- **One designed infographic** at 1080x1350px (4:5 portrait — highest-reach single-image ratio on LinkedIn)
- **One-click PNG download** via html2canvas at 2x resolution
- **Three visual formats**: Myth-Busting Reframe, One Insight, X vs Y Comparison
- **Full design system** built in: typography scale, color tokens, decorative elements
- **Creator badge** with your name and topic

Every infographic gets decorative elements (radial glows, noise textures, dot patterns, accent lines) — no flat backgrounds. Text is sized for single-image impact (larger than carousel equivalents).

## What It Doesn't Do

This is a visual design engine, not a copywriter. It takes your content and makes it look great. For best results, draft your content first (headline, body sections, bottom line), then hand it to this skill for design.

---

## Quick Start

### Claude Cowork / Claude Code

```bash
# Clone the repo
git clone https://github.com/tommy-ngn/skills.git

# Copy the skill to your Claude skills directory
cp -r skills/linkedin-graphics/infographic ~/.claude/skills/
```

Then tell Claude: *"Make an infographic about [your topic]"*

### Claude Projects (claude.ai)

1. Create or open a Project
2. Go to **Project Knowledge**
3. Upload `SKILL.md` and `references/infographic-engine.md`

### Other Platforms

The skill is two markdown files. Add the content of `SKILL.md` and `references/infographic-engine.md` to your system prompt or project context.

---

## Customization

### Brand Colors

The skill ships with a **sage teal** default palette. To use your own brand color, update the `PRIMARY_COLOR` in `SKILL.md` and re-derive the full 7-token palette:

```
PRIMARY_COLOR = #your-hex-color
```

The color derivation rules are in `references/infographic-engine.md` Section 1.

### Brand Identity

Update these in `SKILL.md` Section 2:

```
DISPLAY_NAME  = Your Name
HANDLE        = @yourhandle
CREATOR_SUB   = Your Topic Area
```

### Typography

Default: Newsreader (headings) + Public Sans (body) + JetBrains Mono (labels). Infographic text is sized larger than carousel equivalents (42px headline, 16px body) because a single image needs more presence to stop scrolls.

---

## Infographic Formats

| Format | When to use |
|---|---|
| **Myth-Busting Reframe** | Challenge conventional wisdom — bold myth on top, reframe below |
| **One Insight** | Single bold number or statement with supporting context |
| **X vs Y Comparison** | Two approaches compared side by side with insight line |

---

## File Structure

```
infographic/
├── SKILL.md                         # Skill instructions + brand config
├── README.md                        # This file
└── references/
    └── infographic-engine.md        # Complete HTML/CSS/JS generation spec
```

---

## License

MIT — use, modify, and distribute freely.
