# Carousel Engine — HTML/CSS/JS Generation Reference

Complete technical spec for generating LinkedIn carousel HTML files. Follow precisely.

---

## Table of Contents

1. [Design Tokens & Color System](#1-design-tokens--color-system)
2. [Typography Setup](#2-typography-setup)
3. [Slide Format & Layout Rules](#3-slide-format--layout-rules)
4. [Required Elements on Every Slide](#4-required-elements-on-every-slide)
5. [Slide Content Components](#5-slide-content-components)
6. [Decorative Design Elements](#6-decorative-design-elements)
7. [Standard Slide Sequence](#7-standard-slide-sequence)
8. [LinkedIn Preview Frame](#8-linkedin-preview-frame)
9. [PNG & PDF Download Panel](#9-png--pdf-download-panel)
10. [High-Quality Export via Playwright](#10-high-quality-export-via-playwright)
11. [Common Export Mistakes](#11-common-export-mistakes)

---

## 1. Design Tokens & Color System

Copy this entire `:root` block and the Google Fonts `@import` into every output HTML `<style>`. These are the single source of truth for all visual tokens.

```css
@import url('https://fonts.googleapis.com/css2?family=Newsreader:ital,opsz,wght@0,6..72,400;0,6..72,600;0,6..72,700;0,6..72,800;1,6..72,400&family=Public+Sans:ital,wght@0,400;0,500;0,600;0,700;1,400&family=JetBrains+Mono:wght@400;500;600&display=swap');

:root {
  /* ---------- Primary brand palette ---------- */
  --core:        #3d8b8a;                       /* Sage teal — primary accent */
  --core-soft:   rgba(74, 144, 217, 0.12);      /* Subtle fill, tag chips */
  --core-light:  #6abfbe;                       /* Secondary accent on dark */
  --core-deep:   #1a5c5b;                       /* High-contrast text on light */

  /* ---------- Backgrounds ---------- */
  --canvas:      #F3F6FA;                       /* Cool off-white. Never #fff. */
  --canvas-rule: #E0E6EE;                       /* Dividers/borders on light */
  --ink:         #0D1421;                       /* Cool near-black */

  /* ---------- Text on dark ---------- */
  --text-dark-primary:   #ffffff;
  --text-dark-secondary: rgba(255, 255, 255, 0.55);
  --text-dark-tertiary:  rgba(255, 255, 255, 0.35);

  /* ---------- Text on light ---------- */
  --text-light-primary:   #0D1421;
  --text-light-secondary: #777777;
  --text-light-tertiary:  #bbbbbb;

  /* ---------- Brand gradient (Cover/CTA only) ---------- */
  --brand-gradient:
    radial-gradient(circle at 75% 18%, rgba(61,139,138,0.22) 0%, rgba(61,139,138,0.10) 28%, transparent 58%),
    radial-gradient(circle at 12% 92%, rgba(61,139,138,0.14) 0%, transparent 45%),
    #0D1421;

  /* ---------- Type families ---------- */
  --font-head:    'Newsreader', Georgia, serif;
  --font-body:    'Public Sans', -apple-system, system-ui, sans-serif;
  --font-mono:    'JetBrains Mono', ui-monospace, monospace;

  /* ---------- Spacing scale ---------- */
  --sp-xs: 4px;
  --sp-sm: 8px;
  --sp-md: 12px;
  --sp-lg: 18px;
  --sp-xl: 28px;

  /* ---------- Slide geometry ---------- */
  --slide-pad-top:    44px;
  --slide-pad-bottom: 56px;
  --slide-pad-x:      40px;
  --slide-w:          540px;
  --slide-h:          540px;

  /* ---------- Radii ---------- */
  --r-sm: 4px;
  --r-md: 8px;
  --r-lg: 10px;
  --r-xl: 16px;
  --r-pill: 32px;
}
```

### Custom Color Derivation

When a different primary color is provided, derive the full 7-token palette:

```
CORE        = {user's color}                  // Primary accent
CORE_SOFT   = {primary at 12% opacity}        // Subtle fill backgrounds, tag chips
CORE_LIGHT  = {primary lightened ~28%}        // Secondary accent on dark slides
CORE_DEEP   = {primary darkened ~35%}         // Gradient anchor, high-contrast text
CANVAS      = {tinted off-white}              // Light slide background (never pure #fff)
CANVAS_RULE = {1-2 shades darker than CANVAS} // Dividers, borders on light slides
INK         = {near-black, brand-tempered}    // Dark slide background
```

**Derivation by hue:**
- Warm primaries (reds, oranges, golds): CANVAS `#FAF8F4`, INK `#18150f`
- Cool primaries (blues, greens, purples): CANVAS `#F3F6FA`, INK `#0D1421`
- Neutral primaries: CANVAS `#F7F7F5`, INK `#141414`

**Brand gradient** (cover + CTA slides):
```css
background:
  radial-gradient(circle at 75% 18%, rgba({CORE_RGB},0.22) 0%, rgba({CORE_RGB},0.10) 28%, transparent 58%),
  radial-gradient(circle at 12% 92%, rgba({CORE_RGB},0.14) 0%, transparent 45%),
  {INK};
```

---

## 2. Typography Setup

**Default pairing (Editorial serif + clean sans):**

| Element | Font | Size | Weight | Line-height | Letter-spacing |
|---|---|---|---|---|---|
| Cover headline | Newsreader | 38px | 700 | 1.10 | -0.01em |
| Slide headings | Newsreader | 28px | 700 | 1.14 | -0.005em |
| Compact headings | Newsreader | 22px | 600 | 1.18 | — |
| Body text | Public Sans | 14px | 400 | 1.55 | — |
| Small text | Public Sans | 11.5px | 400 | 1.45 | — |
| Caption text | Public Sans | 10.5px | 500 | — | — |
| Eyebrow labels | JetBrains Mono | 10px | 500 | — | 0.18em, UPPERCASE |
| Slide counters | JetBrains Mono | 11px | 500 | — | 0.08em |
| Level badges | JetBrains Mono | 10px | 500 | — | 0.14em, UPPERCASE |
| Table headers | JetBrains Mono | 9px | 500 | — | 0.12em, UPPERCASE |

**Shared typography classes** (copy into output HTML):

```css
/* --- Headings --- */
.h-cover { font-family: var(--font-head); font-size: 38px; font-weight: 700; line-height: 1.10; position: relative; z-index: 2; font-variation-settings: 'opsz' 60; letter-spacing: -0.01em; }
.h-slide { font-family: var(--font-head); font-size: 28px; font-weight: 700; line-height: 1.14; position: relative; z-index: 2; font-variation-settings: 'opsz' 36; letter-spacing: -0.005em; }
.h-compact { font-family: var(--font-head); font-size: 22px; font-weight: 600; line-height: 1.18; position: relative; z-index: 2; font-variation-settings: 'opsz' 24; }

/* --- Body --- */
.t-body { font-family: var(--font-body); font-size: 14px; line-height: 1.55; position: relative; z-index: 2; }
.t-small { font-family: var(--font-body); font-size: 11.5px; line-height: 1.45; position: relative; z-index: 2; }
.t-caption { font-family: var(--font-body); font-size: 10.5px; font-weight: 500; position: relative; z-index: 2; }

/* --- Eyebrow --- */
.eyebrow { font-family: var(--font-mono); font-size: 10px; font-weight: 500; letter-spacing: 0.18em; text-transform: uppercase; }
.eyebrow-dark { color: var(--core-light); }
.eyebrow-light { color: var(--core-deep); }

/* --- Counter --- */
.counter { font-family: var(--font-mono); font-size: 11px; font-weight: 500; letter-spacing: 0.08em; }
.counter-dark { position: absolute; bottom: 20px; left: 28px; color: rgba(255,255,255,0.25); z-index: 9; }
.counter-light { position: absolute; bottom: 20px; left: 28px; color: rgba(0,0,0,0.2); z-index: 9; }

/* --- Level badges --- */
.lvl-badge { display: inline-block; font-family: var(--font-mono); font-size: 10px; font-weight: 500; letter-spacing: 0.14em; text-transform: uppercase; padding: 4px 10px; border-radius: var(--r-sm); }
.lvl-bottom-80-dark { background: rgba(255,255,255,0.08); color: rgba(255,255,255,0.5); }
.lvl-top-20-dark { background: rgba(61,139,138,0.15); color: var(--core); }
.lvl-top-10-dark { background: rgba(61,139,138,0.20); color: var(--core-light); }
.lvl-top-1-dark { background: var(--core); color: var(--ink); }
.lvl-bottom-80-light { background: rgba(0,0,0,0.06); color: rgba(0,0,0,0.4); }
.lvl-top-20-light { background: rgba(61,139,138,0.15); color: var(--core-deep); }
.lvl-top-10-light { background: rgba(61,139,138,0.25); color: var(--core-deep); }
.lvl-top-1-light { background: var(--core); color: var(--ink); }
```

**Alternative pairings** (if user requests a different vibe):

| Vibe | Heading | Body | Best for |
|---|---|---|---|
| Sharp / technical | Inter Tight 700 | Inter Tight 400 | Engineering, data, startups |
| Bold / expressive | Fraunces | Outfit | Storytelling, strong POV |
| Warm / human | Lora | Nunito Sans | Coaching, HR, personal brand |
| Clean / modern | Plus Jakarta Sans 800 | Plus Jakarta Sans 400 | GTM, generalist |

---

## 3. Slide Format & Layout Rules

- **Aspect ratio:** 1:1 square
- **Preview size:** 540x540px (inside HTML prototype)
- **Export size:** 1080x1080px (via `device_scale_factor: 2` or html2canvas `scale: 2`)
- Each slide is a fully self-contained 540x540px block
- Alternate CANVAS and INK backgrounds for visual rhythm; gradient only for Cover and CTA

**Layout constraints:**
1. Text must never overlap the slide counter. Reserve the bottom 44px.
2. Decorative elements are mandatory on every slide — no flat, plain backgrounds.
3. One idea per slide, no exceptions.
4. Use real, specific numbers. Vague claims lose credibility.
5. The cover earns the swipe. The summary earns the save. The CTA earns the follow.
6. **Visual-first:** Every content slide should lead with a visual element — not walls of text.

**Slide base classes:**

```css
.slide { width: 540px; height: 540px; flex-shrink: 0; position: relative; overflow: hidden; padding: 44px 40px 56px; display: flex; flex-direction: column; }
.slide-gradient {
  background:
    radial-gradient(circle at 75% 18%, rgba(61,139,138,0.22) 0%, rgba(61,139,138,0.10) 28%, transparent 58%),
    radial-gradient(circle at 12% 92%, rgba(61,139,138,0.14) 0%, transparent 45%),
    #0D1421;
  color: #fff;
}
.slide-ink { background: var(--ink); color: #fff; }
.slide-canvas { background: var(--canvas); color: var(--ink); }
```

---

## 4. Required Elements on Every Slide

### Slide Counter (bottom-left, every slide)

```html
<div class="counter counter-dark">01 / 10</div>  <!-- on dark/gradient slides -->
<div class="counter counter-light">03 / 10</div>  <!-- on light slides -->
```

### Swipe Arrow (right edge, all slides except last)

```css
.swipe-arrow { position: absolute; right: 0; top: 0; bottom: 0; width: 44px; display: flex; align-items: center; justify-content: center; z-index: 8; pointer-events: none; }
.swipe-dark { background: linear-gradient(to right, transparent, rgba(255,255,255,0.05)); }
.swipe-light { background: linear-gradient(to right, transparent, rgba(0,0,0,0.03)); }
```

```html
<!-- Dark variant -->
<div class="swipe-arrow swipe-dark">
  <svg width="20" height="20" viewBox="0 0 20 20" fill="none"><path d="M7 5l5 5-5 5" stroke="rgba(255,255,255,0.28)" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/></svg>
</div>
<!-- Light variant -->
<div class="swipe-arrow swipe-light">
  <svg width="20" height="20" viewBox="0 0 20 20" fill="none"><path d="M7 5l5 5-5 5" stroke="rgba(0,0,0,0.18)" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/></svg>
</div>
```

### Save Prompt (CTA slide only, bottom-right)

```html
<div class="save-prompt">
  <svg width="13" height="13" viewBox="0 0 24 24" fill="none" stroke="rgba(255,255,255,0.45)" stroke-width="2.5"><path d="M19 21l-7-5-7 5V5a2 2 0 0 1 2-2h10a2 2 0 0 1 2 2z"/></svg>
  <span>Save this post</span>
</div>
```

```css
.save-prompt { position: absolute; bottom: 20px; right: 28px; display: flex; align-items: center; gap: 6px; z-index: 9; }
.save-prompt span { font-family: var(--font-body); font-size: 10px; color: rgba(255,255,255,0.4); letter-spacing: 0.5px; }
```

---

## 5. Slide Content Components

### Eyebrow Tag

```html
<span class="eyebrow eyebrow-dark">{LABEL}</span>   <!-- on dark slides -->
<span class="eyebrow eyebrow-light">{LABEL}</span>   <!-- on light slides -->
```

### Creator Badge (Cover + CTA slides)

```html
<div class="creator">
  <div class="creator-av"><span>{INITIALS}</span></div>
  <div>
    <div class="creator-name">{DISPLAY_NAME}</div>
    <div class="creator-sub">{CREATOR_SUB}</div>
  </div>
</div>
```

```css
.creator { display: flex; align-items: center; gap: 10px; position: relative; z-index: 2; }
.creator-av { width: 38px; height: 38px; border-radius: 50%; background: rgba(255,255,255,0.12); border: 1.5px solid rgba(255,255,255,0.20); display: flex; align-items: center; justify-content: center; flex-shrink: 0; }
.creator-av span { font-family: var(--font-head); color: #fff; font-weight: 700; font-size: 15px; }
.creator-name { font-family: var(--font-head); font-size: 13px; font-weight: 400; color: #fff; letter-spacing: 0.2px; }
.creator-sub { font-family: var(--font-body); font-size: 10px; color: rgba(255,255,255,0.45); }
```

### Mono-Rows

```html
<div class="mono-rows">
  <div class="mono-row">
    <span class="label">{ROLE}</span>
    <span class="text">{Consequence for this role}</span>
  </div>
</div>
```

```css
.mono-rows { display: flex; flex-direction: column; gap: 0; position: relative; z-index: 2; }
.mono-row { display: flex; align-items: center; gap: 12px; padding: 10px 14px; background: rgba(255,255,255,0.04); border-radius: var(--r-md); margin-bottom: 6px; }
.mono-row .label { font-family: var(--font-mono); font-size: 10px; color: var(--core); font-weight: 600; min-width: 60px; }
.mono-row .text { font-family: var(--font-body); font-size: 11.5px; color: var(--text-dark-secondary); line-height: 1.4; }
```

### SVG-Icon Consequence Rows (dark slides)

```html
<div style="display:flex;align-items:flex-start;gap:16px;padding:14px 16px;background:rgba(255,255,255,0.04);border-radius:var(--r-lg);">
  <div style="flex-shrink:0;width:36px;height:36px;position:relative;margin-top:2px;">
    <svg width="36" height="36" viewBox="0 0 36 36" fill="none">
      <!-- Custom icon — use var(--core) for fills/strokes -->
    </svg>
  </div>
  <div>
    <div style="font-family:var(--font-head);font-size:15px;font-weight:700;color:#fff;margin-bottom:3px;">{Title}</div>
    <div style="font-family:var(--font-body);font-size:11.5px;color:var(--text-dark-secondary);line-height:1.45;">{Explanation}</div>
  </div>
</div>
```

**Icon design rules:** 36x36 viewBox, simple geometric shapes, use `var(--core)` for fills, 3-5 SVG elements max.

### Convergence Diagram (light slides)

```html
<div style="display:flex;flex-direction:column;align-items:center;gap:0;flex:1;justify-content:center;">
  <div style="display:flex;gap:10px;width:100%;margin-bottom:0;">
    <div style="flex:1;padding:12px 14px;background:#fff;border:1.5px solid var(--canvas-rule);border-radius:var(--r-pill);font-family:var(--font-body);font-size:12px;font-weight:500;color:var(--ink);text-align:center;line-height:1.3;box-shadow:0 1px 3px rgba(0,0,0,0.06);">{Input 1}</div>
    <div style="flex:1;padding:12px 14px;background:#fff;border:1.5px solid var(--canvas-rule);border-radius:var(--r-pill);font-family:var(--font-body);font-size:12px;font-weight:500;color:var(--ink);text-align:center;line-height:1.3;box-shadow:0 1px 3px rgba(0,0,0,0.06);">{Input 2}</div>
    <div style="flex:1;padding:12px 14px;background:#fff;border:1.5px solid var(--canvas-rule);border-radius:var(--r-pill);font-family:var(--font-body);font-size:12px;font-weight:500;color:var(--ink);text-align:center;line-height:1.3;box-shadow:0 1px 3px rgba(0,0,0,0.06);">{Input 3}</div>
  </div>
  <svg width="420" height="48" viewBox="0 0 420 48" fill="none" style="display:block;margin:0 auto;">
    <path d="M70 0 L210 42" stroke="var(--ink)" stroke-width="1" stroke-dasharray="4 3" opacity="0.18"/>
    <path d="M210 0 L210 42" stroke="var(--ink)" stroke-width="1" stroke-dasharray="4 3" opacity="0.18"/>
    <path d="M350 0 L210 42" stroke="var(--ink)" stroke-width="1" stroke-dasharray="4 3" opacity="0.18"/>
    <circle cx="210" cy="44" r="3" fill="var(--core)"/>
  </svg>
  <div style="padding:18px 28px;background:rgba(61,139,138,0.10);border:1.5px dashed var(--core);border-radius:var(--r-lg);text-align:center;max-width:320px;width:100%;">
    <div style="font-family:var(--font-mono);font-size:9px;letter-spacing:0.12em;text-transform:uppercase;color:var(--core-deep);margin-bottom:6px;">They all produce</div>
    <div style="font-family:var(--font-head);font-size:20px;font-weight:700;color:var(--core-deep);line-height:1.2;">{Convergent output}</div>
    <div style="font-family:var(--font-body);font-size:11px;color:var(--text-light-secondary);margin-top:5px;">{Why this is a problem}</div>
  </div>
</div>
```

### Segment-to-Product Rows (dark slides)

```html
<div style="display:flex;align-items:stretch;gap:0;border-radius:var(--r-lg);overflow:hidden;">
  <div style="flex:1;padding:14px 16px;background:rgba(255,255,255,0.04);">
    <div style="font-family:var(--font-mono);font-size:8px;font-weight:500;letter-spacing:0.12em;text-transform:uppercase;color:rgba(255,255,255,0.30);margin-bottom:5px;">SEGMENT</div>
    <div style="font-family:var(--font-body);font-size:12px;color:rgba(255,255,255,0.55);line-height:1.4;">{Segment description}</div>
  </div>
  <div style="display:flex;align-items:center;padding:0 8px;background:rgba(255,255,255,0.02);">
    <svg width="16" height="16" viewBox="0 0 16 16" fill="none"><path d="M5 3l5 5-5 5" stroke="rgba(255,255,255,0.15)" stroke-width="1.5" stroke-linecap="round"/></svg>
  </div>
  <div style="flex:1;padding:14px 16px;background:rgba(61,139,138,0.08);border-left:2px solid var(--core);">
    <div style="font-family:var(--font-mono);font-size:8px;font-weight:500;letter-spacing:0.12em;text-transform:uppercase;color:var(--core);margin-bottom:5px;">PRODUCT</div>
    <div style="font-family:var(--font-body);font-size:12px;color:var(--core-light);line-height:1.4;font-weight:600;">{Product implication}</div>
  </div>
</div>
```

### Two-Column Contrast Grid (light slides)

```html
<div style="display:grid;grid-template-columns:1fr 1fr;gap:8px 16px;position:relative;z-index:2;">
  <div style="font-family:var(--font-mono);font-size:9px;font-weight:500;letter-spacing:0.14em;text-transform:uppercase;color:#999;margin-bottom:2px;">{Left label}</div>
  <div style="font-family:var(--font-mono);font-size:9px;font-weight:500;letter-spacing:0.14em;text-transform:uppercase;color:var(--core-deep);margin-bottom:2px;">{Right label}</div>
  <div style="padding:10px;background:rgba(0,0,0,0.04);border-radius:var(--r-sm);font-family:var(--font-body);font-size:11px;line-height:1.4;color:var(--ink);">{Left value}</div>
  <div style="padding:10px;background:rgba(61,139,138,0.15);border-radius:var(--r-sm);font-family:var(--font-body);font-size:11px;line-height:1.4;color:var(--ink);">{Right value}</div>
</div>
```

### Comparison Table (dark slides)

```css
.cmp-table { width: 100%; border-collapse: separate; border-spacing: 0; position: relative; z-index: 2; font-size: 11px; }
.cmp-table th { font-family: var(--font-mono); font-size: 9px; font-weight: 500; letter-spacing: 0.12em; text-transform: uppercase; padding: 8px 6px 10px; color: rgba(255,255,255,0.35); text-align: left; border-bottom: 1px solid rgba(255,255,255,0.06); }
.cmp-table td { padding: 10px 6px; vertical-align: top; border-bottom: 1px solid rgba(255,255,255,0.06); }
.cmp-table tr:last-child td { border-bottom: none; }
```

### Feature Box

```html
<!-- Light variant -->
<div style="padding:16px 18px;background:rgba(61,139,138,0.12);border-radius:var(--r-lg);border:1px solid var(--core-soft);position:relative;z-index:2;">
  <div style="font-family:var(--font-head);font-size:20px;font-weight:700;color:var(--core-deep);margin-bottom:6px;">{Title}</div>
  <p class="t-small" style="color:var(--text-light-secondary);line-height:1.5;">{Supporting argument}</p>
</div>

<!-- Dark variant -->
<div style="padding:14px 16px;background:rgba(61,139,138,0.10);border-radius:var(--r-lg);border:1px solid rgba(61,139,138,0.20);position:relative;z-index:2;">
  <div style="font-family:var(--font-head);font-size:22px;font-weight:700;color:var(--core-light);line-height:1.2;margin-bottom:6px;">{Title}</div>
  <p style="font-family:var(--font-body);font-size:11.5px;color:var(--core-light);line-height:1.5;">{Supporting argument}</p>
</div>
```

### Move-Up Callout (dark slides)

```html
<div style="padding:10px 14px;background:rgba(61,139,138,0.08);border-left:2px solid var(--core);border-radius:0 var(--r-md) var(--r-md) 0;position:relative;z-index:2;">
  <p style="font-family:var(--font-body);font-size:11px;color:var(--core-light);line-height:1.5;">{Key takeaway}</p>
</div>
```

### Emphasis Callout (light slides)

```html
<div style="padding:12px 16px;background:var(--core-soft);border-left:3px solid var(--core);border-radius:0 var(--r-md) var(--r-md) 0;position:relative;z-index:2;">
  <p style="font-family:var(--font-body);font-size:11px;color:var(--ink);line-height:1.5;font-weight:500;">{Emphasis text}</p>
</div>
```

### Before / After Comparison

```css
.ba { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; position: relative; z-index: 2; }
.ba-cell { padding: 14px 16px; border-radius: var(--r-lg); }
.ba-before { background: rgba(0,0,0,0.04); border: 1px solid var(--canvas-rule); }
.ba-after { background: var(--core-soft); border: 1px solid var(--core); }
.ba-lbl { font-family: var(--font-mono); font-size: 9px; font-weight: 500; letter-spacing: 0.14em; text-transform: uppercase; margin-bottom: 8px; }
.ba-before .ba-lbl { color: #bbb; }
.ba-after .ba-lbl { color: var(--core-deep); }
.ba-before .ba-t { font-family: var(--font-body); font-size: 12px; color: #999; line-height: 1.45; }
.ba-after .ba-t { font-family: var(--font-body); font-size: 12px; color: var(--ink); font-weight: 600; line-height: 1.45; }
/* Dark variants */
.ba-before-dk { background: rgba(255,255,255,0.04); border: 1px solid rgba(255,255,255,0.06); }
.ba-after-dk { background: rgba(61,139,138,0.10); border: 1px solid var(--core); }
.ba-before-dk .ba-lbl { color: rgba(255,255,255,0.3); }
.ba-after-dk .ba-lbl { color: var(--core); }
.ba-before-dk .ba-t { color: rgba(255,255,255,0.45); }
.ba-after-dk .ba-t { color: var(--core-light); font-weight: 600; }
```

### Strikethrough Pill

```html
<span style="font-family:var(--font-body);font-size:11px;padding:5px 13px;border:1px solid rgba(255,255,255,0.1);border-radius:20px;color:#555;text-decoration:line-through;">{Old thing}</span>
```

### CTA Button (final slide only)

```html
<div class="cta-btn">{CTA label} &rarr;</div>
```

```css
.cta-btn { display: inline-flex; align-items: center; gap: 8px; padding: 14px 32px; background: #fff; color: var(--core-deep); font-family: var(--font-body); font-weight: 700; font-size: 14px; border-radius: var(--r-pill); letter-spacing: 0.2px; }
```

---

## 6. Decorative Design Elements

Every slide must include at least one decorative element. These are not optional.

### On light slides (CANVAS background):

```html
<div class="deco-circ" style="top:-80px;right:-60px;width:260px;height:260px;opacity:0.06;"></div>
<div class="deco-circ" style="top:40px;right:30px;width:100px;height:100px;opacity:0.03;"></div>
```

```css
.deco-circ { position: absolute; border-radius: 50%; background: var(--core); pointer-events: none; }
```

### On dark slides (INK background):

```html
<div class="deco-dots"></div>
<div class="deco-circ" style="bottom:-100px;right:-80px;width:300px;height:300px;opacity:0.06;"></div>
```

```css
.deco-dots { position: absolute; inset: 0; background-image: radial-gradient(rgba(255,255,255,0.03) 1px, transparent 1px); background-size: 22px 22px; pointer-events: none; }
```

### On gradient slides (Cover + CTA):

```html
<div class="deco-grad-dots"></div>
<div class="deco-ring" style="width:460px;height:460px;"></div>
<div class="deco-ring" style="width:340px;height:340px;"></div>
<div class="deco-ring" style="width:220px;height:220px;"></div>
```

```css
.deco-grad-dots { position: absolute; inset: 0; background-image: radial-gradient(rgba(255,255,255,0.05) 1px, transparent 1px); background-size: 18px 18px; pointer-events: none; }
.deco-ring { position: absolute; top: 50%; left: 50%; transform: translate(-50%,-50%); border-radius: 50%; border: 1px solid rgba(61,139,138,0.10); pointer-events: none; }
```

---

## 7. Standard Slide Sequence

| # | Type | Background | Purpose |
|---|---|---|---|
| 1 | Cover | Gradient | Bold hook — a specific, debatable claim. Creator badge. |
| 2 | Problem / Context | INK | Frame the pain or mistake. Mono-rows or strikethrough pills. |
| 3 | Core Argument | CANVAS | Single most important visual — convergence diagram, contrast grid, or stat callout. |
| 4 to N-2 | Content slides | Alternate INK / CANVAS | One idea per slide. Lead with visual component. |
| N-1 | Summary / Recap | INK | Comparison table or 3-5 bullet TL;DR with left-rule. Most-saved slide type. |
| N | CTA | Gradient | Creator badge, CTA button, save prompt. No swipe arrow. |

---

## 8. LinkedIn Preview Frame

Wrap slides in a LinkedIn-style document post frame (540px wide).

```css
.lk-frame { width: 540px; background: #fff; border-radius: 12px; overflow: hidden; box-shadow: 0 1px 2px rgba(0,0,0,0.06), 0 8px 24px rgba(0,0,0,0.06); }
.lk-header { display: flex; align-items: center; gap: 10px; padding: 14px 16px; }
.lk-avatar { width: 40px; height: 40px; border-radius: 50%; background: radial-gradient(circle at 75% 18%, rgba(61,139,138,0.22) 0%, transparent 58%), #0D1421; display: flex; align-items: center; justify-content: center; flex-shrink: 0; }
.lk-avatar span { font-family: var(--font-head); color: #fff; font-weight: 700; font-size: 16px; }
.lk-meta { flex: 1; }
.lk-name { font-size: 13px; font-weight: 600; color: var(--ink); font-family: var(--font-body); }
.lk-name .badge { font-size: 10px; color: #777; font-weight: 400; margin-left: 4px; }
.lk-sub { font-size: 11px; color: #777; font-family: var(--font-body); }
.lk-doc-tag { font-size: 9px; font-weight: 700; letter-spacing: 1px; padding: 3px 7px; background: #eef3fa; color: #0a66c2; border-radius: 3px; }
```

### Viewport & Track:

```css
#viewport { width: 540px; height: 540px; overflow: hidden; position: relative; cursor: grab; user-select: none; background: var(--ink); }
#viewport:active { cursor: grabbing; }
#track { display: flex; transition: transform 0.32s cubic-bezier(0.22,0.61,0.36,1); will-change: transform; }
```

### Dot indicators & pager:

```css
.lk-dots { display: flex; justify-content: center; gap: 6px; padding: 12px 16px 4px; }
.dot { width: 6px; height: 6px; border-radius: 50%; background: rgba(0,0,0,0.18); transition: all 0.2s; cursor: pointer; }
.dot.active { background: var(--core); transform: scale(1.25); }
.lk-pager { text-align: center; font-family: var(--font-body); font-size: 11px; color: #777; padding-bottom: 8px; }
```

### Swipe/drag JavaScript:

```javascript
const track=document.getElementById('track'),vp=document.getElementById('viewport'),dotsEl=document.getElementById('dots'),pager=document.getElementById('pager'),TOTAL={N},W=540;
let cur=0,startX=0,dragging=false;
for(let i=0;i<TOTAL;i++){const d=document.createElement('div');d.className='dot'+(i===0?' active':'');d.addEventListener('click',()=>goTo(i));dotsEl.appendChild(d);}
function goTo(i){cur=Math.max(0,Math.min(TOTAL-1,i));track.style.transform=`translateX(${-cur*W}px)`;document.querySelectorAll('.dot').forEach((d,idx)=>d.classList.toggle('active',idx===cur));pager.textContent=`Slide ${cur+1} of ${TOTAL}`;}
vp.addEventListener('mousedown',e=>{dragging=true;startX=e.clientX;track.style.transition='none';});
vp.addEventListener('touchstart',e=>{dragging=true;startX=e.touches[0].clientX;track.style.transition='none';},{passive:true});
vp.addEventListener('mousemove',e=>{if(!dragging)return;track.style.transform=`translateX(${-cur*W+e.clientX-startX}px)`;});
vp.addEventListener('touchmove',e=>{if(!dragging)return;track.style.transform=`translateX(${-cur*W+e.touches[0].clientX-startX}px)`;},{passive:true});
const end=ex=>{if(!dragging)return;dragging=false;track.style.transition='transform 0.32s cubic-bezier(0.22,0.61,0.36,1)';const dx=ex-startX;if(dx<-50)goTo(cur+1);else if(dx>50)goTo(cur-1);else goTo(cur);};
vp.addEventListener('mouseup',e=>end(e.clientX));vp.addEventListener('mouseleave',e=>end(e.clientX));vp.addEventListener('touchend',e=>end(e.changedTouches[0].clientX));
document.addEventListener('keydown',e=>{if(e.key==='ArrowRight')goTo(cur+1);if(e.key==='ArrowLeft')goTo(cur-1);});
```

---

## 9. PNG & PDF Download Panel

```html
<div id="download-panel" style="width:540px;margin-top:16px;background:#1a1a1e;border-radius:12px;padding:20px 24px;">
  <div style="font-family:var(--font-mono);font-size:11px;font-weight:500;color:rgba(255,255,255,0.5);letter-spacing:0.12em;text-transform:uppercase;margin-bottom:14px;">Download Slides</div>
  <div id="dl-buttons" style="display:flex;flex-wrap:wrap;gap:8px;"></div>
  <div style="font-family:var(--font-body);font-size:11px;color:rgba(255,255,255,0.25);margin-top:14px;line-height:1.5;">
    Downloads each slide as 1080x1080px PNG. Wait 5s after page load for fonts.
  </div>
</div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
```

### Download JavaScript:

```javascript
(function(){
  const W=540,T={N},panel=document.getElementById('dl-buttons');

  async function captureSlide(i){
    const track=document.getElementById('track');
    track.style.transition='none';
    track.style.transform=`translateX(${-i*W}px)`;
    await new Promise(r=>setTimeout(r,350));
    const hide=document.querySelectorAll('.lk-header,.lk-dots,.lk-pager,.lk-actions,.lk-caption,#download-panel');
    hide.forEach(el=>el.style.visibility='hidden');
    const c=await html2canvas(document.getElementById('viewport'),{scale:2,useCORS:true,width:W,height:W,backgroundColor:null,logging:false});
    hide.forEach(el=>el.style.visibility='');
    track.style.transition='transform 0.32s cubic-bezier(0.22,0.61,0.36,1)';
    return c;
  }

  async function dlPng(i){
    const c=await captureSlide(i);
    const a=document.createElement('a');a.download=`slide_${String(i+1).padStart(2,'0')}.png`;a.href=c.toDataURL('image/png');a.click();
  }

  for(let i=0;i<T;i++){const b=document.createElement('button');b.textContent=`Slide ${i+1}`;b.style.cssText='padding:8px 14px;background:rgba(255,255,255,0.08);border:1px solid rgba(255,255,255,0.12);border-radius:8px;color:#fff;font-family:var(--font-body);font-size:12px;font-weight:500;cursor:pointer;';b.onclick=()=>dlPng(i);panel.appendChild(b);}

  const all=document.createElement('button');all.textContent='All PNGs';all.style.cssText+='margin-left:4px;padding:8px 14px;background:rgba(255,255,255,0.08);border:1px solid rgba(255,255,255,0.12);border-radius:8px;color:#fff;font-family:var(--font-body);font-size:12px;font-weight:500;cursor:pointer;';
  all.onclick=async()=>{all.textContent='Downloading...';for(let i=0;i<T;i++){await dlPng(i);await new Promise(r=>setTimeout(r,600));}all.textContent='Done';setTimeout(()=>all.textContent='All PNGs',2000);};
  panel.appendChild(all);

  const pdfBtn=document.createElement('button');
  pdfBtn.textContent='Download PDF';
  pdfBtn.style.cssText='background:var(--core)!important;border-color:var(--core)!important;font-weight:700;margin-left:4px;padding:8px 18px;border-radius:8px;color:#fff;font-family:var(--font-body);font-size:12px;cursor:pointer;';
  pdfBtn.onclick=async()=>{
    pdfBtn.textContent='Building PDF...';
    const {jsPDF}=window.jspdf;
    const size=1080;
    const pdf=new jsPDF({orientation:'portrait',unit:'px',format:[size,size],hotfixes:['px_scaling']});
    for(let i=0;i<T;i++){
      if(i>0) pdf.addPage([size,size],'portrait');
      const c=await captureSlide(i);
      const img=c.toDataURL('image/png');
      pdf.addImage(img,'PNG',0,0,size,size);
      await new Promise(r=>setTimeout(r,200));
    }
    pdf.save('carousel.pdf');
    pdfBtn.textContent='Done';
    setTimeout(()=>pdfBtn.textContent='Download PDF',2000);
    const track=document.getElementById('track');
    track.style.transform='translateX(0)';
    document.querySelectorAll('.dot').forEach((d,idx)=>d.classList.toggle('active',idx===0));
    document.getElementById('pager').textContent='Slide 1 of '+T;
  };
  panel.appendChild(pdfBtn);
})();
```

---

## 10. High-Quality Export via Playwright

Optional — only needed if jsPDF quality isn't sufficient. The inline PDF button works for most cases.

```python
import asyncio
from pathlib import Path
from playwright.async_api import async_playwright

INPUT_HTML  = Path("{html_filename}")
OUTPUT_DIR  = Path("./slides")
OUTPUT_DIR.mkdir(exist_ok=True)

TOTAL  = {N}
VIEW_W = 540
VIEW_H = 540
SCALE  = 2.0

async def export():
    async with async_playwright() as p:
        browser = await p.chromium.launch()
        page = await browser.new_page(
            viewport={"width": VIEW_W, "height": VIEW_H},
            device_scale_factor=SCALE,
        )
        await page.set_content(INPUT_HTML.read_text(encoding="utf-8"), wait_until="networkidle")
        await page.wait_for_timeout(3500)

        await page.evaluate("""() => {
            document.querySelectorAll('.lk-header,.lk-dots,.lk-pager,.lk-actions,.lk-caption,#download-panel')
                .forEach(el => el.style.display = 'none');
            const frame = document.querySelector('.lk-frame');
            frame.style.cssText = 'width:540px;height:540px;max-width:none;border-radius:0;box-shadow:none;overflow:hidden;margin:0;';
            const vp = document.querySelector('#viewport');
            vp.style.cssText = 'width:540px;height:540px;overflow:hidden;cursor:default;';
            document.body.style.cssText = 'padding:0;margin:0;display:block;background:#fff;';
        }""")
        await page.wait_for_timeout(400)

        for i in range(TOTAL):
            await page.evaluate("""(idx) => {
                const t = document.querySelector('#track');
                t.style.transition = 'none';
                t.style.transform  = `translateX(${-idx * 540}px)`;
            }""", i)
            await page.wait_for_timeout(380)
            await page.screenshot(
                path=str(OUTPUT_DIR / f"slide_{str(i+1).zfill(2)}.png"),
                clip={"x":0,"y":0,"width":VIEW_W,"height":VIEW_H}
            )
            print(f"  Exported slide {i+1}/{TOTAL}")

        await browser.close()

    from PIL import Image
    slides = sorted(OUTPUT_DIR.glob("slide_*.png"))
    images = [Image.open(s).convert("RGB") for s in slides]
    pdf_path = INPUT_HTML.stem + ".pdf"
    images[0].save(pdf_path, save_all=True, append_images=images[1:])
    print(f"PDF ready: {pdf_path}")

asyncio.run(export())
```

---

## 11. Common Export Mistakes

| Mistake | What breaks | Fix |
|---|---|---|
| Viewport set to 1080px | Layout reflows, fonts shrink | Keep viewport 540x540, use `device_scale_factor: 2` |
| External image `src` paths | Images missing in headless | Base64-encode all images inline |
| No font wait timeout | Fallback system fonts render | `wait_for_timeout(3500)` after `set_content` |
| Frame chrome not hidden | Export includes header/dots | Hide all `.lk-*` elements |
| Files not zero-padded | Sort order breaks | Use `.zfill(2)` on all filenames |
| Missing jsPDF script tag | PDF button doesn't work | Include both html2canvas and jsPDF CDN scripts |
| Text-heavy slides | Low engagement, few saves | Lead every slide with a visual component |
