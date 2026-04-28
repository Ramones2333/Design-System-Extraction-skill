# Input Routing, Output Modes, and HTML Handoff

Use this reference when the task involves multiple source types, an HTML deliverable, or frontend-ready design-system output.

## 1. Source Inventory And Routing

Before extraction, create a source inventory table:

| Source | Type | Read Method | Evidence Strength | Limitations |
|---|---|---|---|---|
| `source-name` | Figma / image / code / PDF / token data / mixed | How it was inspected | High / medium / low | What cannot be verified |

Use extension, URL, and content hints to classify files:

| Hint | Route As | Notes |
|---|---|---|
| Figma URL, `.fig`, exported Figma metadata | Figma | Prefer variables, styles, components, and variants before frames |
| `.png`, `.jpg`, `.jpeg`, `.webp`, `.gif`, screenshot folders | Screenshot/image | Extract visible rules only |
| `.svg` | Image or source code | Treat as vector visual evidence unless it is part of an icon/component source library |
| `.tsx`, `.jsx`, `.vue`, `.svelte`, `.html`, `.css`, `.scss`, `.less` | Component-library/source code | Inspect component API, variants, states, and styling |
| `tailwind.config.*`, `theme.*`, `tokens.*`, `*.tokens.json`, `variables.css` | Token/theme code | Treat as high-priority token evidence |
| `.json`, `.yaml`, `.yml` with token-like keys | Exported token data | Preserve original token names and alias structure |
| `.stories.*`, Storybook folders, docs examples | Component-library docs | Use for variants, state coverage, and usage examples |
| `.pdf`, `.docx`, `.md`, `.mdx`, `.txt` specs | PDF/doc spec | Extract explicit written rules and embedded visual evidence |

Route each source type as follows.

### Figma files, pages, frames

Prioritize:

1. Variables, local styles, text styles, effects, grids
2. Components, variants, component properties, interactive states
3. Reusable modules and master pages
4. Final screens and page instances

Extract:

- Token candidates and explicit token names
- Component anatomy, variants, properties, and states
- Page templates, layout grids, breakpoints if visible
- Usage consistency between library definitions and page instances

Mark as needing specification:

- Hidden states not present in variants
- Motion timing not shown in prototypes
- Responsive behavior not represented by frames

### Screenshots and image mockups

Prioritize visible evidence only:

- Repeated colors, typography hierarchy, spacing rhythms, radius, elevation
- Component families and visible states
- Page-template structure and information hierarchy

Do not invent:

- Exact token names
- Hidden component states
- Internal component API
- Breakpoints not shown by multiple viewport screenshots

When numeric values are estimated from pixels, label them as estimates and recommend source-file confirmation.

### Component-library source code

Inspect:

- Token files, theme files, CSS variables, Tailwind config, design-token JSON
- Component props, variants, size maps, state classes, accessibility attributes
- Stories, examples, docs, tests, and usage sites
- Package exports and naming conventions

Extract:

- Canonical token names and values
- Component API and implementation constraints
- State coverage and missing states
- Frontend adoption guidance

If code conflicts with visual design, separate:

- `Implemented standard`
- `Designed standard`
- `Recommended reconciliation`

### PDF, DOCX, or written specs

Extract:

- Explicit token tables
- Component rules and state definitions
- Page templates and layout annotations
- Accessibility, responsive, and interaction requirements
- Embedded screenshots as supporting visual evidence

Treat old or partial docs as weaker evidence than current source code or current Figma libraries unless the user says the spec is authoritative.

### Exported token data

Inspect JSON, CSS, SCSS, YAML, XML, or design-token exports for:

- Token taxonomy
- Primitive vs semantic token relationships
- Mode/theme support
- Alias/reference structure
- Platform targets

Preserve original token names. Only propose renamed tokens under the recommendation label.

### Mixed-source projects

Build a source-evidence matrix:

| Design-system area | Strongest source | Supporting source | Conflict | Decision |
|---|---|---|---|---|
| Color tokens | Token JSON | Figma variables | Screenshot uses old blue | Use token JSON; flag screenshot drift |

Resolve by domain:

- Token values: token exports, theme files, Figma variables
- Component contracts: component source, Storybook, Figma components
- Visual usage: production screens, high-fidelity Figma screens, screenshots
- Written policy: explicit specs, PDF/docs, annotations

## 2. Output Mode Selection

Use one of three modes.

### Quick audit

Use when the user asks for a short analysis, fast diagnosis, or prioritization.

HTML sections:

1. Title, scope, source inventory
2. Executive summary
3. Confirmed system patterns
4. Top inconsistencies
5. Highest-priority specification gaps
6. Recommended next actions

Keep it compact. Do not include full component manuals unless the user asks.

### Full spec

Use by default when the user asks to extract or generate a design system.

HTML sections:

1. Title, scope, source inventory, output mode
2. Design system overview and style direction
3. Foundational visual specifications
4. Page templates and layout rules
5. Core design principles
6. Inconsistencies and standardization recommendations
7. Specification gaps and next completion priorities

### Frontend handoff

Use when the user asks for implementation-ready output, frontend handoff, code, tokens, CSS variables, Tailwind, or engineering adoption.

Include every `full spec` section plus:

1. Token inventory table
2. CSS custom properties
3. Tailwind theme extension
4. Design Tokens JSON
5. Implementation notes
6. Accessibility and state coverage checklist
7. Adoption checklist and migration risks

## 3. HTML Deliverable Requirements

Create a standalone HTML file when possible.

Minimum document requirements:

- `<!doctype html>` and valid `<html lang="">`
- Embedded `<style>`; no remote CSS or script dependencies by default
- Semantic structure: `header`, `main`, `section`, `table`, `pre`, `code`
- Sticky or top navigation when the document is long
- Evidence labels styled distinctly
- Visual boards for typography, spacing, radius, border, shadow, color, and grid
- Tables for token, source, recommendation, and gap inventories
- Copyable code blocks as plain `<pre><code>` blocks
- Print-friendly styling

Visual style:

- Use a polished analysis-report layout inspired by the referenced competitive-analysis page: pale slate background, max-width centered container, dark indigo/blue gradient header, white cards with subtle shadows, section titles with a bottom divider, compact tables, two-column comparison grids, pill badges, and left-border insight callouts.
- Keep the style embedded in the HTML file. Do not require Tailwind CDN or external scripts.
- Use accent color pairs for comparison or status-heavy sections: indigo for confirmed/system evidence, sky blue for source or implementation evidence, amber for recommendations, violet for gaps.
- When screenshots are included, place them in `.image-grid` and `.image-card` blocks with short captions. Do not add hotspot overlays unless the source evidence is clear.
- Add clear vertical breathing room between a table/callout/code block and the next subsection heading. A subsection title should never visually touch the previous block.

HTML shell:

```html
<!doctype html>
<html lang="zh-CN">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Design System Extraction Report</title>
  <style>
    :root {
      --bg: #f8fafc;
      --surface: #ffffff;
      --text: #1e293b;
      --muted: #64748b;
      --border: #e2e8f0;
      --soft-border: #f1f5f9;
      --indigo: #6366f1;
      --indigo-dark: #4338ca;
      --sky: #0ea5e9;
      --sky-dark: #0369a1;
      --amber: #d97706;
      --violet: #7c3aed;
      --radius: 10px;
      --shadow: 0 4px 12px -2px rgba(15, 23, 42, 0.08);
    }
    * { box-sizing: border-box; }
    body { margin: 0; font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, "PingFang SC", sans-serif; color: var(--text); background: var(--bg); line-height: 1.65; }
    .report-shell { max-width: 1180px; margin: 0 auto; padding: 32px 16px 64px; }
    .page-header { padding: 38px 28px; border-radius: 14px; margin-bottom: 28px; color: #fff; background: linear-gradient(135deg, #1e1b4b 0%, #312e81 52%, #1d4ed8 100%); }
    .eyebrow { margin: 0 0 8px; color: #c7d2fe; font-size: 12px; font-weight: 700; letter-spacing: 0.12em; text-transform: uppercase; }
    .subtitle { margin: 0; max-width: 760px; color: #dbeafe; font-size: 14px; }
    .badge-row { display: flex; flex-wrap: wrap; gap: 8px; margin-top: 18px; }
    .badge { display: inline-flex; align-items: center; gap: 6px; padding: 4px 10px; border-radius: 999px; font-size: 11px; font-weight: 700; border: 1px solid rgba(255,255,255,0.24); background: rgba(255,255,255,0.12); color: #eef2ff; }
    .report-nav { position: sticky; top: 0; z-index: 5; display: flex; gap: 8px; overflow-x: auto; margin: -8px 0 24px; padding: 10px 0; background: rgba(248,250,252,0.92); backdrop-filter: blur(8px); }
    .report-nav a { white-space: nowrap; text-decoration: none; color: #475569; font-size: 12px; font-weight: 700; padding: 7px 10px; border: 1px solid var(--border); border-radius: 999px; background: #fff; }
    section.card { margin: 0 0 28px; padding: 28px; background: var(--surface); border: 1px solid var(--border); border-radius: var(--radius); box-shadow: var(--shadow); }
    h1, h2, h3, h4 { line-height: 1.25; margin: 0 0 12px; }
    h1 { font-size: clamp(28px, 4vw, 40px); letter-spacing: -0.01em; }
    .section-title { display: flex; align-items: center; gap: 8px; padding-bottom: 10px; margin-bottom: 16px; border-bottom: 2px solid var(--border); color: var(--text); font-size: 22px; font-weight: 800; }
    .section-index { color: var(--indigo); font-weight: 900; }
    .section-note { margin: -6px 0 18px; color: #94a3b8; font-size: 12px; font-weight: 700; letter-spacing: 0.08em; text-transform: uppercase; }
    .subsection-title { margin: 34px 0 14px; color: #0f172a; font-size: 18px; font-weight: 800; }
    .subsection-title:first-child { margin-top: 0; }
    p { margin: 8px 0; }
    .table-wrap { overflow-x: auto; margin: 16px 0 28px; border: 1px solid var(--border); border-radius: 10px; background: #fff; }
    table { width: 100%; border-collapse: collapse; font-size: 13px; }
    th { background: #f8fafc; color: #334155; font-weight: 800; text-align: left; padding: 11px 14px; border-bottom: 1px solid var(--border); }
    td { padding: 11px 14px; border-bottom: 1px solid var(--soft-border); color: #475569; vertical-align: top; }
    tr:last-child td { border-bottom: none; }
    .col-dim { width: 22%; color: #374151; background: #f8fafc; font-weight: 800; }
    .col-primary { border-left: 3px solid var(--indigo); background: #fafafe; }
    .col-secondary { border-left: 3px solid var(--sky); background: #f8fcff; }
    .grid-2 { display: grid; grid-template-columns: repeat(2, minmax(0, 1fr)); gap: 20px; }
    .grid-3 { display: grid; grid-template-columns: repeat(3, minmax(0, 1fr)); gap: 16px; }
    .mini-card { border: 1px solid var(--border); border-radius: 10px; overflow: hidden; background: #fff; }
    .mini-card-header { display: flex; align-items: center; gap: 8px; padding: 10px 14px; font-size: 12px; font-weight: 800; letter-spacing: 0.04em; text-transform: uppercase; border-bottom: 1px solid var(--border); }
    .mini-card-header.primary { color: var(--indigo-dark); background: #eef2ff; }
    .mini-card-header.secondary { color: var(--sky-dark); background: #e0f2fe; }
    .dot { width: 8px; height: 8px; border-radius: 50%; background: currentColor; }
    .mini-card-body { padding: 14px; color: #475569; font-size: 13px; }
    .visual-board { display: grid; grid-template-columns: repeat(3, minmax(0, 1fr)); gap: 16px; margin: 18px 0 28px; }
    .visual-tile { min-height: 132px; padding: 16px; border: 1px solid var(--border); border-radius: 12px; background: #fff; }
    .visual-tile h4 { margin-bottom: 10px; color: #334155; font-size: 13px; font-weight: 800; }
    .swatch-row { display: flex; flex-wrap: wrap; gap: 10px; }
    .swatch { width: 72px; overflow: hidden; border: 1px solid var(--border); border-radius: 9px; background: #fff; font-size: 11px; color: #475569; }
    .swatch-chip { height: 42px; border-bottom: 1px solid var(--border); }
    .swatch span { display: block; padding: 6px; overflow-wrap: anywhere; }
    .type-sample { display: grid; gap: 8px; }
    .type-display { font-size: 34px; line-height: 1.08; font-weight: 700; }
    .type-title { font-size: 22px; line-height: 1.18; font-weight: 700; }
    .type-body { color: #475569; font-size: 14px; }
    .spacing-rhythm { display: grid; gap: 10px; }
    .space-row { display: grid; grid-template-columns: 52px 1fr; align-items: center; gap: 10px; color: #64748b; font-size: 12px; }
    .space-bar { height: 12px; border-radius: 999px; background: linear-gradient(90deg, #6366f1, #0ea5e9); }
    .radius-grid { display: flex; flex-wrap: wrap; gap: 12px; align-items: end; }
    .radius-demo { width: 72px; height: 54px; border: 1px solid #cbd5e1; background: #f8fafc; box-shadow: 0 8px 20px rgba(15,23,42,0.08); }
    .image-grid { display: grid; grid-template-columns: repeat(2, minmax(0, 1fr)); gap: 20px; margin-top: 18px; }
    .image-card { overflow: hidden; border: 1px solid var(--border); border-radius: 10px; background: #fff; }
    .image-stage { position: relative; background: #f8fafc; }
    .image-card img { display: block; width: 100%; height: auto; background: #f8fafc; }
    .annotation-box { position: absolute; border: 2px solid rgba(99,102,241,0.88); background: rgba(99,102,241,0.08); border-radius: 4px; pointer-events: none; }
    .annotation-label { position: absolute; left: 0; top: -24px; padding: 3px 7px; border-radius: 4px; background: #6366f1; color: #fff; font-size: 10px; font-weight: 800; white-space: nowrap; }
    .image-caption { padding: 9px 12px; color: var(--muted); background: #f8fafc; border-top: 1px solid var(--soft-border); font-size: 12px; }
    .insight { margin: 22px 0 28px; padding: 14px 16px; border-left: 4px solid #94a3b8; border-radius: 0 8px 8px 0; background: #f8fafc; color: #374151; font-size: 13px; }
    .insight strong { color: var(--text); }
    pre { overflow: auto; margin: 16px 0 28px; padding: 16px; background: #0f172a; color: #e2e8f0; border-radius: 10px; }
    code { font-family: ui-monospace, SFMono-Regular, Menlo, Consolas, monospace; }
    .label { display: inline-block; margin-right: 6px; padding: 2px 8px; border-radius: 999px; font-size: 12px; font-weight: 700; }
    .confirmed { color: var(--indigo-dark); background: #eef2ff; }
    .needed { color: var(--violet); background: #f3e8ff; }
    .recommendation { color: var(--amber); background: #fff7ed; }
    @media (max-width: 820px) { .grid-2, .grid-3, .visual-board, .image-grid { grid-template-columns: 1fr; } section.card { padding: 22px; } .page-header { padding: 30px 22px; } }
    @media print { body { background: #fff; } .report-nav { display: none; } section.card { box-shadow: none; break-inside: avoid; } }
  </style>
</head>
<body>
  <div class="report-shell">
    <header class="page-header">
      <p class="eyebrow">Design System Extraction Report</p>
      <h1>设计系统提炼报告</h1>
      <p class="subtitle">基于输入材料的 token、视觉规范、页面模板、不一致问题与前端交付资产分析。</p>
      <div class="badge-row">
        <span class="badge">Mode: full spec</span>
        <span class="badge">Input quality: L4</span>
        <span class="badge">Output: standalone HTML</span>
      </div>
    </header>

    <nav class="report-nav" aria-label="Report sections">
      <a href="#sources">来源清单</a>
      <a href="#tokens">基础视觉规范</a>
      <a href="#templates">页面模板</a>
      <a href="#handoff">前端交付</a>
    </nav>

    <main>
      <section class="card" id="sources">
        <h2 class="section-title"><span class="section-index">01</span> 来源清单 &amp; 输出模式</h2>
        <p class="section-note">Source inventory · Quality level · Evidence limits</p>
        <!-- Insert source inventory table and evidence notes here. -->
      </section>

      <section class="card" id="tokens">
        <h2 class="section-title"><span class="section-index">02</span> 基础视觉规范</h2>
        <p class="section-note">Color · Typography · Spacing · Radius · Shadow · Grid</p>
        <div class="visual-board">
          <div class="visual-tile">
            <h4>色彩 Swatches</h4>
            <div class="swatch-row">
              <div class="swatch"><div class="swatch-chip" style="background:#635bff"></div><span>brand / #635BFF</span></div>
              <div class="swatch"><div class="swatch-chip" style="background:#0a2540"></div><span>text / #0A2540</span></div>
            </div>
          </div>
          <div class="visual-tile">
            <h4>字体层级 Typography</h4>
            <div class="type-sample">
              <div class="type-display">Display</div>
              <div class="type-title">Section title</div>
              <div class="type-body">Body text and UI explanation sample.</div>
            </div>
          </div>
          <div class="visual-tile">
            <h4>间距 Spacing</h4>
            <div class="spacing-rhythm">
              <div class="space-row"><span>8px</span><div class="space-bar" style="width:24px"></div></div>
              <div class="space-row"><span>16px</span><div class="space-bar" style="width:48px"></div></div>
              <div class="space-row"><span>32px</span><div class="space-bar" style="width:96px"></div></div>
            </div>
          </div>
          <div class="visual-tile">
            <h4>圆角 / 阴影 Radius &amp; Elevation</h4>
            <div class="radius-grid">
              <div><div class="radius-demo" style="border-radius:4px"></div><p>4px</p></div>
              <div><div class="radius-demo" style="border-radius:12px"></div><p>12px</p></div>
            </div>
          </div>
        </div>
      </section>
    </main>
  </div>
</body>
</html>
```

## 4. Frontend Handoff Formats

Only include exact values when they are supported by source evidence. Otherwise mark values as recommendations or placeholders needing confirmation.

### Token inventory table

| Token | Category | Value | Source | Status | Usage |
|---|---|---|---|---|---|
| `color.primary.500` | Color | `#2457D6` | Figma variable / theme file | Confirmed | Primary actions |

### CSS custom properties

```css
:root {
  --color-primary-500: #2457d6;
  --color-text-primary: #172033;
  --radius-control: 8px;
  --space-4: 16px;
}
```

### Tailwind theme extension

```js
export default {
  theme: {
    extend: {
      colors: {
        primary: {
          500: "#2457d6"
        }
      },
      borderRadius: {
        control: "8px"
      },
      spacing: {
        4: "16px"
      }
    }
  }
};
```

### Design Tokens JSON

```json
{
  "color": {
    "primary": {
      "500": {
        "$type": "color",
        "$value": "#2457d6",
        "$description": "Primary action color"
      }
    }
  },
  "radius": {
    "control": {
      "$type": "dimension",
      "$value": "8px"
    }
  }
}
```

### Implementation notes

For each implementation-relevant pattern, include:

- Source evidence
- Required variants or states when visible
- Token dependencies
- Accessibility requirements
- Known gaps
- Migration notes
