# Infographic Engine - HTML/CSS/JS Generation Reference

Complete technical spec for generating LinkedIn infographic HTML files. Follow precisely when building any infographic.

---

## 1. Design Tokens

Every infographic HTML file must include these CSS custom properties in its `<style>` tag. These are the single source of truth for all colors, fonts, and shared values.

**To customize:** Change `--core` to your brand color and re-derive the palette:
- `--core-soft`: your core color at 12% opacity
- `--core-light`: 40% lighter, for secondary accents on dark backgrounds
- `--core-deep`: 40% darker, for gradients and high-contrast text on light backgrounds
- `--canvas`: cool off-white (light background)
- `--canvas-rule`: subtle gray for dividers on light backgrounds
- `--ink`: cool near-black (dark background)

```css
:root {
  /* === COLOR TOKENS === */
  --core:        #3d8b8a;
  --core-soft:   rgba(61, 139, 138, 0.12);
  --core-light:  #6abfbe;
  --core-deep:   #1a5c5b;
  --canvas:      #F3F6FA;
  --canvas-rule: #E0E6EE;
  --ink:         #0D1421;

  /* === BRAND GRADIENT === */
  --brand-gradient: linear-gradient(135deg, #1a5c5b 0%, #3d8b8a 50%, #6abfbe 100%);

  /* === FONT STACKS === */
  --font-head: 'Newsreader', Georgia, 'Times New Roman', serif;
  --font-body: 'Public Sans', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
  --font-mono: 'JetBrains Mono', 'SF Mono', 'Fira Code', 'Cascadia Code', monospace;
}
```

### Eyebrow Classes

```css
.eyebrow {
  font-family: var(--font-mono);
  font-size: 10px;
  font-weight: 600;
  letter-spacing: 0.18em;
  text-transform: uppercase;
}
.eyebrow-dark {
  color: var(--core);
}
.eyebrow-light {
  color: var(--core-deep);
}
```

### Google Fonts Import

Copy this into each infographic's `<style>` tag, before the `:root` block:

```css
@import url('https://fonts.googleapis.com/css2?family=Newsreader:ital,opsz,wght@0,6..72,400;0,6..72,600;0,6..72,700;0,6..72,800;1,6..72,400&family=Public+Sans:ital,wght@0,400;0,500;0,600;0,700;1,400&family=JetBrains+Mono:wght@400;500;600&display=swap');
```

---

## 2. Infographic-Specific Typography

These classes are sized for single-image infographics. They are larger than carousel equivalents because the infographic is the ONLY visual (not one of 10 slides), so text needs more presence to stop scrolls.

```css
/* INFOGRAPHIC-SPECIFIC OVERRIDES */

/* Headline: larger than carousel (38px) for single-image impact */
.h-infographic { font-family: var(--font-head); font-size: 42px; font-weight: 800; line-height: 1.08; position: relative; z-index: 2; font-variation-settings: 'opsz' 60; letter-spacing: -0.015em; }

/* Secondary heading */
.h-secondary { font-family: var(--font-head); font-size: 26px; font-weight: 700; line-height: 1.14; position: relative; z-index: 2; font-variation-settings: 'opsz' 36; letter-spacing: -0.005em; }

/* Body: 16px (carousel uses 14px) for single-image readability */
.t-body { font-family: var(--font-body); font-size: 16px; line-height: 1.55; position: relative; z-index: 2; }

/* Small: 13px (carousel uses 11.5px) */
.t-small { font-family: var(--font-body); font-size: 13px; line-height: 1.45; position: relative; z-index: 2; }

/* Caption */
.t-caption { font-family: var(--font-body); font-size: 11px; font-weight: 500; position: relative; z-index: 2; }
```

---

## 3. Infographic Layout

**Aspect ratio:** 4:5 portrait (highest-reach single-image ratio on LinkedIn 2026)
**Preview size:** 540 x 675px
**Export size:** 1080 x 1350px (via html2canvas `scale: 2`)

```css
.infographic { width: 540px; height: 675px; position: relative; overflow: hidden; padding: 48px 44px 64px; display: flex; flex-direction: column; }
.infographic-ink { background: var(--ink); color: #fff; }
.infographic-canvas { background: var(--canvas); color: var(--ink); }
```

**Layout zones (top to bottom):**

```
+------------------------------------------+
| EYEBROW (top, 48px from top)             |  ~28px
| HEADLINE ZONE                            |  ~120-160px
| VISUAL DIVIDER or SPACER                 |  ~24-40px
| BODY ZONE                                |  ~200-300px
| BOTTOM LINE                              |  ~40px
| CREATOR BADGE (bottom, 64px from bottom) |  ~48px
+------------------------------------------+
```

**Layout rules:**

1. Text must never overlap the creator badge area. Reserve bottom 64px.
2. Decorative elements are mandatory - no flat backgrounds.
3. Headline must be readable at phone thumbnail size (42px at 540w = ~21px at 270w thumbnail).
4. Maximum text density: 60 words total across the entire infographic. If you're over 60 words, cut.
5. Default background is INK (dark). Use CANVAS (light) only for X vs Y comparisons where column readability matters more than drama.

---

## 4. Template A: Myth-Busting Reframe

**Visual structure:** Bold myth on top, accent divider with arrow, reframe below.

```html
<div class="infographic infographic-ink" id="infographic">
  <!-- Decorative elements (see Section 8) -->

  <span class="eyebrow eyebrow-dark" style="display:block;margin-bottom:14px;position:relative;z-index:2;">THE MYTH</span>

  <h1 class="h-infographic" style="color:#fff; margin-bottom:0;">
    {Myth claim, 8-12 words}
  </h1>

  <!-- Accent divider with downward arrow -->
  <div style="display:flex;align-items:center;gap:12px;margin:28px 0;position:relative;z-index:2;">
    <div style="flex:1;height:1px;background:linear-gradient(to right,var(--core),transparent);"></div>
    <svg width="24" height="24" viewBox="0 0 24 24" fill="none">
      <path d="M12 4v16m0 0l-6-6m6 6l6-6" stroke="var(--core)" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
    </svg>
    <div style="flex:1;height:1px;background:linear-gradient(to left,var(--core),transparent);"></div>
  </div>

  <span class="eyebrow eyebrow-dark" style="display:block;margin-bottom:14px;position:relative;z-index:2;">WHAT ACTUALLY WORKS</span>

  <p class="h-secondary" style="color:var(--core-light); margin-bottom:auto;">
    {Reframe, 15-25 words}
  </p>

  <!-- Bottom thesis line -->
  <p class="t-small" style="color:rgba(255,255,255,0.40); margin-bottom:16px; position:relative; z-index:2;">
    {One-line thesis anchor}
  </p>

  <!-- Creator badge (see Section 7) -->
</div>
```

**Customization points:**

- Eyebrow labels can vary: "THE MYTH" / "WHAT MOST BUILDERS BELIEVE" / "THE ASSUMPTION" for top; "THE REALITY" / "WHAT ACTUALLY WORKS" / "THE REFRAME" for bottom
- Bottom thesis line is optional but recommended
- The accent divider arrow can be replaced with a simple line for subtler designs

---

## 5. Template B: One Insight

**Visual structure:** One bold number or statement, supporting context below.

```html
<div class="infographic infographic-ink" id="infographic">
  <!-- Decorative elements -->

  <span class="eyebrow eyebrow-dark" style="display:block;margin-bottom:14px;position:relative;z-index:2;">{TOPIC LABEL}</span>

  <!-- The number or statement - THE scroll-stopper -->
  <h1 class="h-infographic" style="color:var(--core); margin-bottom:24px; font-size:56px;">
    {Bold number or short claim}
  </h1>

  <!-- Context that makes the number meaningful -->
  <p class="t-body" style="color:rgba(255,255,255,0.65); max-width:420px; margin-bottom:auto;">
    {2-3 lines explaining WHY this number matters. Not restating it - explaining the mechanism.}
  </p>

  <!-- Thesis anchor -->
  <p class="t-small" style="color:rgba(255,255,255,0.35); margin-bottom:16px; position:relative; z-index:2;">
    {One-line thesis or CTA}
  </p>

  <!-- Creator badge -->
</div>
```

**Customization points:**

- If the scroll-stopper is a number, set it in `var(--core)` at 56px for maximum impact
- If it is a statement (not a number), keep at 42px in white
- Aim for under 40 words total for this format

---

## 6. Template C: X vs Y Comparison

**Visual structure:** Two columns side by side. Left = common approach, Right = better approach. Bottom insight line explains the gap.

**Default background:** CANVAS (light) for readability of two-column layout.

```html
<div class="infographic infographic-canvas" id="infographic">
  <!-- Decorative elements (canvas variant, see Section 8) -->

  <span class="eyebrow eyebrow-light" style="display:block;margin-bottom:14px;position:relative;z-index:2;">{TOPIC LABEL}</span>

  <h2 class="h-secondary" style="color:var(--ink); margin-bottom:24px;">
    {Comparison hook, e.g. "How most teams segment users vs how the best teams do it"}
  </h2>

  <!-- Two-column comparison -->
  <div style="display:flex;gap:16px;flex:1;position:relative;z-index:2;">

    <!-- Left column: COMMON APPROACH -->
    <div style="flex:1;padding:20px;background:#fff;border:1.5px solid var(--canvas-rule);border-radius:12px;">
      <div style="font-family:var(--font-mono);font-size:9px;font-weight:600;letter-spacing:0.14em;text-transform:uppercase;color:#888;margin-bottom:14px;">MOST TEAMS</div>
      <div style="display:flex;flex-direction:column;gap:10px;">
        <div style="display:flex;align-items:flex-start;gap:8px;">
          <div style="width:6px;height:6px;border-radius:50%;background:var(--canvas-rule);margin-top:6px;flex-shrink:0;"></div>
          <span class="t-small" style="color:#888;">{Behavior 1}</span>
        </div>
        <!-- Repeat for behaviors 2-4 -->
      </div>
    </div>

    <!-- Right column: BETTER APPROACH -->
    <div style="flex:1;padding:20px;background:var(--core-soft);border:1.5px solid var(--core);border-radius:12px;">
      <div style="font-family:var(--font-mono);font-size:9px;font-weight:600;letter-spacing:0.14em;text-transform:uppercase;color:var(--core-deep);margin-bottom:14px;">TOP TEAMS</div>
      <div style="display:flex;flex-direction:column;gap:10px;">
        <div style="display:flex;align-items:flex-start;gap:8px;">
          <div style="width:6px;height:6px;border-radius:50%;background:var(--core);margin-top:6px;flex-shrink:0;"></div>
          <span class="t-small" style="color:var(--ink);">{Behavior 1}</span>
        </div>
        <!-- Repeat for behaviors 2-4 -->
      </div>
    </div>
  </div>

  <!-- Bottom insight line -->
  <div style="margin-top:20px;padding:14px 18px;background:rgba(61,139,138,0.08);border-left:3px solid var(--core);border-radius:0 8px 8px 0;position:relative;z-index:2;">
    <p class="t-small" style="color:var(--ink);font-weight:500;margin:0;">
      {The WHY behind the gap - the mechanism insight, 1-2 sentences}
    </p>
  </div>

  <!-- Creator badge (canvas variant) -->
</div>
```

**Customization points:**

- Left column: neutral bullets (gray dots), white background, subtle border
- Right column: accent bullets, tinted background, accent border - visual weight signals "better path"
- The bottom insight line is the most important element
- Can use INK background for a more dramatic look, but requires inverting all text and border colors

---

## 7. Creator Badge

Positioned absolute bottom-left within the 675px frame.

**On INK (dark) background:**

```html
<div style="display:flex;align-items:center;gap:10px;position:absolute;bottom:24px;left:44px;z-index:2;">
  <div style="width:34px;height:34px;border-radius:50%;background:rgba(255,255,255,0.10);border:1.5px solid rgba(255,255,255,0.18);display:flex;align-items:center;justify-content:center;flex-shrink:0;">
    <span style="font-family:var(--font-head);color:#fff;font-weight:700;font-size:13px;">YN</span>
  </div>
  <div>
    <div style="font-family:var(--font-head);font-size:12px;font-weight:400;color:rgba(255,255,255,0.70);letter-spacing:0.2px;">Your Name</div>
    <div style="font-family:var(--font-body);font-size:9px;color:rgba(255,255,255,0.35);">Your Topic</div>
  </div>
</div>
```

**On CANVAS (light) background:**

```html
<div style="display:flex;align-items:center;gap:10px;position:absolute;bottom:24px;left:44px;z-index:2;">
  <div style="width:34px;height:34px;border-radius:50%;background:var(--core-soft);border:1.5px solid var(--core);display:flex;align-items:center;justify-content:center;flex-shrink:0;">
    <span style="font-family:var(--font-head);color:var(--core-deep);font-weight:700;font-size:13px;">YN</span>
  </div>
  <div>
    <div style="font-family:var(--font-head);font-size:12px;font-weight:400;color:var(--ink);letter-spacing:0.2px;">Your Name</div>
    <div style="font-family:var(--font-body);font-size:9px;color:#888;">Your Topic</div>
  </div>
</div>
```

---

## 8. Decorative Elements

Infographics must not have flat backgrounds. These create depth and editorial presence.

### On INK (dark) backgrounds:

```html
<!-- Radial glow (top-right) -->
<div style="position:absolute;top:-80px;right:-60px;width:320px;height:320px;background:radial-gradient(circle,rgba(61,139,138,0.10) 0%,transparent 70%);pointer-events:none;z-index:0;"></div>

<!-- Secondary glow (bottom-left) -->
<div style="position:absolute;bottom:-40px;left:-40px;width:200px;height:200px;background:radial-gradient(circle,rgba(61,139,138,0.06) 0%,transparent 65%);pointer-events:none;z-index:0;"></div>

<!-- Noise texture (MUST be inline div, not pseudo-element, for html2canvas) -->
<div style="position:absolute;inset:0;background-image:url(&quot;data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.85' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.03'/%3E%3C/svg%3E&quot;);pointer-events:none;z-index:1;"></div>
```

### On CANVAS (light) backgrounds:

```html
<!-- Dot pattern (top-right corner) -->
<svg style="position:absolute;top:32px;right:32px;z-index:0;opacity:0.12;" width="60" height="60" viewBox="0 0 60 60" fill="none">
  <circle cx="6" cy="6" r="1.5" fill="var(--core)"/>
  <circle cx="6" cy="18" r="1.5" fill="var(--core)"/>
  <circle cx="6" cy="30" r="1.5" fill="var(--core)"/>
  <circle cx="18" cy="6" r="1.5" fill="var(--core)"/>
  <circle cx="18" cy="18" r="1.5" fill="var(--core)"/>
  <circle cx="18" cy="30" r="1.5" fill="var(--core)"/>
  <circle cx="30" cy="6" r="1.5" fill="var(--core)"/>
  <circle cx="30" cy="18" r="1.5" fill="var(--core)"/>
  <circle cx="30" cy="30" r="1.5" fill="var(--core)"/>
</svg>

<!-- Soft accent line (left edge) -->
<div style="position:absolute;left:0;top:20%;height:30%;width:3px;background:linear-gradient(to bottom,transparent,var(--core),transparent);opacity:0.25;z-index:0;"></div>
```

---

## 9. PNG Export System

Each infographic HTML file includes a "Download PNG" button that uses html2canvas to export at 2x resolution (1080x1350).

### Export Script

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
<script>
async function downloadPNG() {
  const btn = document.getElementById('dl-btn');
  btn.textContent = 'Exporting...';
  btn.disabled = true;

  await document.fonts.ready;
  await new Promise(r => setTimeout(r, 400));

  const el = document.getElementById('infographic');
  const canvas = await html2canvas(el, {
    scale: 2,
    useCORS: true,
    backgroundColor: null,
    logging: false,
    width: 540,
    height: 675
  });

  const link = document.createElement('a');
  link.download = '{filename}.png';
  link.href = canvas.toDataURL('image/png');
  link.click();

  btn.textContent = 'Download PNG';
  btn.disabled = false;
}
</script>
```

### Download Button

```html
<div style="margin-top:16px;text-align:center;">
  <button id="dl-btn" onclick="downloadPNG()"
    style="font-family:var(--font-body);font-size:13px;font-weight:600;
           padding:10px 28px;background:var(--core);color:var(--ink);
           border:none;border-radius:6px;cursor:pointer;letter-spacing:0.02em;">
    Download PNG
  </button>
</div>
```

### Export Gotchas

1. **Font loading:** The 400ms delay after `document.fonts.ready` is essential. Without it, html2canvas captures fallback fonts.
2. **Scale factor:** Always use `scale: 2` for crisp text at 1080x1350.
3. **Background color:** Set `backgroundColor: null` and let CSS handle backgrounds. This preserves gradients and noise textures.
4. **Pseudo-elements:** html2canvas does NOT render `::before` and `::after`. The noise texture must be an inline div (as shown in Section 8), not a pseudo-element.
5. **SVG in exports:** Inline SVGs render correctly. External SVG references do not. All decorative SVGs must be inline.

---

## 10. Full HTML Skeleton

Every infographic HTML file follows this structure. Replace `{filename}` with the infographic's slug (e.g., `myth-talk-to-users`, `insight-90-day-dropoff`, `xvy-segmentation`).

**How to assemble:**
1. Copy the Google Fonts `@import` (from Section 1)
2. Copy the `:root` block (from Section 1)
3. Copy the `.eyebrow`, `.eyebrow-dark`, `.eyebrow-light` classes (from Section 1)
4. Add the infographic-specific classes (from Section 2)
5. Add layout classes (from Section 3)
6. Insert the chosen template HTML (from Sections 4-6)

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>{Infographic Title}</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Newsreader:ital,opsz,wght@0,6..72,400;0,6..72,600;0,6..72,700;0,6..72,800;1,6..72,400&family=Public+Sans:ital,wght@0,400;0,500;0,600;0,700;1,400&family=JetBrains+Mono:wght@400;500;600&display=swap');

  :root {
    --core:        #3d8b8a;
    --core-soft:   rgba(61, 139, 138, 0.12);
    --core-light:  #6abfbe;
    --core-deep:   #1a5c5b;
    --canvas:      #F3F6FA;
    --canvas-rule: #E0E6EE;
    --ink:         #0D1421;
    --brand-gradient: linear-gradient(135deg, #1a5c5b 0%, #3d8b8a 50%, #6abfbe 100%);
    --font-head: 'Newsreader', Georgia, 'Times New Roman', serif;
    --font-body: 'Public Sans', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
    --font-mono: 'JetBrains Mono', 'SF Mono', 'Fira Code', 'Cascadia Code', monospace;
  }

  .eyebrow { font-family: var(--font-mono); font-size: 10px; font-weight: 600; letter-spacing: 0.18em; text-transform: uppercase; }
  .eyebrow-dark { color: var(--core); }
  .eyebrow-light { color: var(--core-deep); }

  * { margin: 0; padding: 0; box-sizing: border-box; }
  body { background: #1a1a1a; display: flex; flex-direction: column; align-items: center; padding: 40px 20px; min-height: 100vh; font-family: var(--font-body); }

  .h-infographic { font-family: var(--font-head); font-size: 42px; font-weight: 800; line-height: 1.08; position: relative; z-index: 2; font-variation-settings: 'opsz' 60; letter-spacing: -0.015em; }
  .h-secondary { font-family: var(--font-head); font-size: 26px; font-weight: 700; line-height: 1.14; position: relative; z-index: 2; font-variation-settings: 'opsz' 36; letter-spacing: -0.005em; }
  .t-body { font-family: var(--font-body); font-size: 16px; line-height: 1.55; position: relative; z-index: 2; }
  .t-small { font-family: var(--font-body); font-size: 13px; line-height: 1.45; position: relative; z-index: 2; }

  .infographic { width: 540px; height: 675px; position: relative; overflow: hidden; padding: 48px 44px 64px; display: flex; flex-direction: column; }
  .infographic-ink { background: var(--ink); color: #fff; }
  .infographic-canvas { background: var(--canvas); color: var(--ink); }
</style>
</head>
<body>

  <!-- === INFOGRAPHIC === -->
  <div class="infographic infographic-ink" id="infographic">
    <!-- Decorative elements (inline divs, not pseudo-elements) -->
    <div style="position:absolute;top:-80px;right:-60px;width:320px;height:320px;background:radial-gradient(circle,rgba(61,139,138,0.10) 0%,transparent 70%);pointer-events:none;z-index:0;"></div>
    <div style="position:absolute;bottom:-40px;left:-40px;width:200px;height:200px;background:radial-gradient(circle,rgba(61,139,138,0.06) 0%,transparent 65%);pointer-events:none;z-index:0;"></div>
    <div style="position:absolute;inset:0;background-image:url(&quot;data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.85' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.03'/%3E%3C/svg%3E&quot;);pointer-events:none;z-index:1;"></div>

    <!-- CONTENT (insert template HTML here) -->

    <!-- Creator badge -->
    <div style="display:flex;align-items:center;gap:10px;position:absolute;bottom:24px;left:44px;z-index:2;">
      <div style="width:34px;height:34px;border-radius:50%;background:rgba(255,255,255,0.10);border:1.5px solid rgba(255,255,255,0.18);display:flex;align-items:center;justify-content:center;flex-shrink:0;">
        <span style="font-family:var(--font-head);color:#fff;font-weight:700;font-size:13px;">YN</span>
      </div>
      <div>
        <div style="font-family:var(--font-head);font-size:12px;font-weight:400;color:rgba(255,255,255,0.70);letter-spacing:0.2px;">Your Name</div>
        <div style="font-family:var(--font-body);font-size:9px;color:rgba(255,255,255,0.35);">Your Topic</div>
      </div>
    </div>
  </div>

  <!-- === DOWNLOAD BUTTON === -->
  <div style="margin-top:16px;text-align:center;">
    <button id="dl-btn" onclick="downloadPNG()"
      style="font-family:var(--font-body);font-size:13px;font-weight:600;padding:10px 28px;background:var(--core);color:var(--ink);border:none;border-radius:6px;cursor:pointer;letter-spacing:0.02em;">
      Download PNG
    </button>
  </div>

  <script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
  <script>
  async function downloadPNG() {
    const btn = document.getElementById('dl-btn');
    btn.textContent = 'Exporting...';
    btn.disabled = true;
    await document.fonts.ready;
    await new Promise(r => setTimeout(r, 400));
    const el = document.getElementById('infographic');
    const canvas = await html2canvas(el, {
      scale: 2, useCORS: true, backgroundColor: null, logging: false,
      width: 540, height: 675
    });
    const link = document.createElement('a');
    link.download = '{filename}.png';
    link.href = canvas.toDataURL('image/png');
    link.click();
    btn.textContent = 'Download PNG';
    btn.disabled = false;
  }
  </script>
</body>
</html>
```
