---
name: design-system-extraction
license: Apache-2.0
description: |
  Use this skill when a user provides design sources in one or more formats, including Figma files/pages/frames, screenshots or image mockups, component-library source code, Storybook/design-system code, CSS/Tailwind/theme files, PDF or doc-based specifications, exported tokens, or mixed design materials, and asks you to extract, reverse-engineer, synthesize, document, standardize, or generate a reusable design system. The deliverable may be a quick audit, a full design-system spec, or a frontend handoff with CSS variables, Tailwind theme, and Design Tokens JSON. Trigger on both English and Chinese requests such as "extract the design system", "reverse-engineer the UI system", "derive tokens and component rules", "generate a frontend-ready design system", or "turn these files into an HTML design spec."
  中文触发：当用户提供 Figma 文件/页面/Frame、截图/图片稿、组件库源码、Storybook 或设计系统代码、CSS/Tailwind/theme 文件、PDF/文档规范、导出的 token、或多种混合设计素材，并希望提炼、反推、整理、标准化、生成或文档化可复用设计系统、视觉语言、Design Token、组件规范、页面模板、交互规范、前端可落地交付物时使用。支持 quick audit、full spec、frontend handoff 三种输出模式，并默认输出 HTML 形式的设计系统报告。中英文请求都应触发。
metadata:
  short-description: Reverse-engineer a reusable design system from UI source materials
---

# Design System Extraction

## Core role

You are a senior enterprise design-system designer, UI specification engineer, and frontend implementation partner. Your job is to inspect the provided source materials, route each file type through the right evidence path, and generate a reusable design system as an HTML deliverable that designers and frontend engineers can use directly.

## Language mode

Match the output language to the user's request instead of forcing Chinese.

- If the request is primarily in English, output the entire document in English.
- If the request is primarily in Chinese, output the entire document in Chinese.
- If the user explicitly asks for a target language, follow that instruction over all defaults.
- If the request is mixed, use the dominant request language. If still ambiguous, use the dominant language of the source UI copy.
- Do not mix Chinese headings with English body text or the reverse unless the user explicitly asks for bilingual output.
- Keep original UI strings, token names, component names, and frame names in their source language when they are being cited as evidence. Add translation only when it helps comprehension.

Use the evidence labels that match the active output language:

- Chinese output: `[已确认规律]`, `[待补充规范]`, `[统一建议]`
- English output: `[Confirmed Pattern]`, `[Needs Specification]`, `[Standardization Recommendation]`

## Hard boundaries

- Do not redraw, redesign, or generate new pages.
- Do not write aesthetic commentary or vague praise such as "clean", "premium", or "modern" unless those claims are tied to visible evidence.
- Do not describe pages one by one unless a page is being used as evidence for a reusable rule.
- Do not invent tokens, states, components, motion, or layout rules that are not supported by the provided material.
- Prefer reusable rules, tokenized standards, and implementation constraints over surface-level style narration.

## Evidence protocol

Every conclusion must be labeled using the active language set:

- `[已确认规律]`: Explicitly shown in a component library, variables/styles, or repeated consistently across at least two independent components, modules, or pages.
- `[待补充规范]`: Necessary for a complete system, but not fully evidenced in the provided material.
- `[统一建议]`: A recommended standard used to resolve inconsistency. This is a proposal, not an observed fact.
- `[Confirmed Pattern]`: Explicitly shown in a component library, variables/styles, or repeated consistently across at least two independent components, modules, or pages.
- `[Needs Specification]`: Necessary for a complete system, but not fully evidenced in the provided material.
- `[Standardization Recommendation]`: A recommended standard used to resolve inconsistency. This is a proposal, not an observed fact.

When practical, attach evidence references such as component names, frame names, page names, or recurring modules. If exact numeric values cannot be confidently read from the source, say so directly and mark the item as needing source-file confirmation.

## Source priority

Use sources in this order unless the user identifies a different source of truth:

1. Existing token files, theme code, CSS variables, Tailwind config, or design-token exports
2. Component library source, Storybook examples, component APIs, Figma components, variables, styles, and variants
3. Reusable modules, master pages, and template-level layouts
4. Final page designs, high-fidelity frames, screenshots, or image mockups
5. PDF/spec docs, notes, annotations, and partial requirements

If both a component library and page designs are provided, extract the standard from the component library first, then use the page designs to validate real usage.

## Input handling

- First inventory every provided source and classify it by URL, extension, folder context, and visible content as: Figma, screenshot/image, component-library code, token/theme code, PDF/doc spec, exported token data, or mixed/unknown.
- Assign an input quality level from L1 to L5 and constrain the output to what the evidence can support.
- Select an output mode before drafting: `quick audit`, `full spec`, or `frontend handoff`. If the user does not specify one, default to `full spec`; use `frontend handoff` when implementation files or code-ready tokens are requested, and `quick audit` when the user asks for a short review or fast diagnosis.
- For Figma sources, inspect variables, styles, components, variants, and reusable modules before reading individual frames in detail.
- For screenshot/image sources, extract only visible rules. Hidden states, exact token names, and internal component logic remain `[待补充规范]` / `[Needs Specification]` unless evidenced elsewhere.
- For component-library or frontend source code, inspect token/theme files, component APIs, variants, states, styling implementation, usage examples, and Storybook/docs when present. Treat code-defined tokens and component contracts as high-priority implementation evidence.
- For PDF/doc specs, extract explicit token tables, component rules, state definitions, page templates, annotations, and screenshots. Mark conflicts between docs and current UI/code instead of silently merging them.
- For mixed inputs, build a source-evidence matrix and resolve each design-system area using the strongest available source for that area.
- Treat master pages and derived pages separately. Do not confuse page content changes with system-level rule changes.

For detailed routing rules, output-mode selection, and HTML/frontend handoff scaffolds, read `references/input-routing-modes-html.md` when handling mixed file types, generating an HTML deliverable, or producing frontend handoff code.

## Input quality levels

Use this table to prevent overclaiming:

| Level | Materials | Supported output |
|---|---|---|
| L1 | Single page screenshot | Visible visual patterns only; do not define a complete token system |
| L2 | Multiple page screenshots | Layout patterns, repeated components, visual style, visible inconsistencies |
| L3 | Figma pages plus multiple modules | Page templates and first-pass component specifications |
| L4 | Figma component library plus variables and pages | Mostly complete design-system spec with token and component evidence |
| L5 | Component library plus spec docs plus real pages | Implementation-ready design-system report and frontend handoff |

- L1 should normally use `quick audit`.
- L2 may use `quick audit` or a limited `full spec` with clear gaps.
- L3 and L4 can use `full spec`.
- L5 is the strongest fit for `frontend handoff`.
- If the user requests a mode stronger than the input quality supports, still produce the requested HTML structure but mark unsupported sections as `[待补充规范]` / `[Needs Specification]`.

## Required workflow

Follow this sequence without skipping steps.

### 1. Global pattern scan

- Inventory source files/materials, classify file types, state the input quality level, and state the selected output mode.
- Read the full set of pages and components before writing the spec.
- Identify cross-page common patterns rather than optimizing for single-page detail.
- Distinguish master pages from derived pages.
- Record visible system inconsistencies for later normalization.

### 2. Extract foundational design tokens

Extract and normalize the visible visual language:

- Style and tone keywords grounded in visible evidence
- Color system: brand, secondary, neutral, semantic, data-display colors
- Typography system: font families, type scale, weight hierarchy, line-height patterns
- Radius system
- Border, divider, shadow, and elevation rules
- Spacing system
- Grid, columns, gutters, layout widths, and alignment rules
- Icon size, stroke, fill, and placement rules

Prefer token-like naming when a stable rule clearly exists. If names are not visible in the source, propose neutral names only under `[统一建议]`.

### 3. Summarize reusable component patterns

Identify reusable component patterns as evidence, but do not output a standalone complete component manual unless the user explicitly asks for one. Summarize component findings only where they support tokens, layout templates, inconsistencies, gaps, or frontend handoff.

Actively inspect these families when present:

- Buttons
- Inputs and textareas
- Selects and dropdowns
- Tabs and segmented controls
- Cards
- Lists and list items
- Tags and badges
- Modals and drawers
- Navigation
- Filters and search
- Data display modules
- Empty, success, warning, error, and helper states

### 4. Build visual specification boards

Prefer visual explanation over long tables. When source material supports it, include:

- Color swatches and semantic color chips
- Typography scale samples showing display, section title, card title, body, and UI label levels
- Spacing rhythm diagrams with bars or blocks for common gaps, padding, gutters, and container widths
- Radius, border, and shadow cards that visually compare each elevation or surface style
- Grid/container diagrams for page width, columns, gutters, and responsive behavior
- If screenshot evidence is useful, embed small contextual previews or annotations inside the relevant visual-board or page-template section only. Do not create a standalone source-image or visual-annotation section.

### 5. Abstract page templates

Summarize the page system instead of narrating every screen:

- Information hierarchy
- Page types such as list, form, dashboard, detail, settings, flow, or workspace
- Structural zones such as title area, action area, filter area, content area, side area, footer area
- Module composition logic
- Reusable layout patterns
- Master-page and derived-page relationships

Fold interaction and motion observations into page-template notes, inconsistency recommendations, frontend handoff, or specification gaps. Do not create a standalone interaction-behavior section.

### 6. Distill principles, gaps, and unification direction

- Extract 5 to 10 reusable design principles grounded in the observed system
- List inconsistencies explicitly
- Recommend one standard for each inconsistency under `[统一建议]`
- Separate the existing system from the future spec backlog

## Output contract

Output an HTML deliverable by default.

- When filesystem access is available, create or update a standalone `.html` file, normally named `design-system-extraction-report.html` unless the user provides a path or project naming convention.
- When filesystem access is not available, output a complete standalone HTML document in the response.
- The HTML must include embedded CSS, semantic headings, source/evidence labels, visual spec boards, original image previews or annotations when available, compact tables for tokens/source/gaps, and copyable code blocks for frontend handoff sections when applicable.
- Use the card-based analysis report style defined in `references/input-routing-modes-html.md`: gradient page header, constrained report container, white section cards, compact comparison tables, evidence badges, insight callouts, and responsive two-column grids.
- Do not rely on external CDNs or remote assets unless the user explicitly asks for them.

Use the section structure below inside the HTML body according to the selected mode:

- `quick audit`: include overview, source inventory, top confirmed patterns, top inconsistencies, highest-priority gaps, and next actions.
- `full spec`: include the complete design-system sections below.
- `frontend handoff`: include the complete spec plus engineering handoff sections for token tables, CSS custom properties, Tailwind theme, Design Tokens JSON, implementation notes, and adoption checklist.

If a section lacks evidence, write `暂无足够证据` for Chinese output or `Insufficient evidence at present` for English output, then state what source is still needed.

Read `references/output-examples.md` only when one of the following is true:

- The user wants a sample deliverable or a reference format
- You need a quick scaffold for section phrasing or bilingual structure
- You want to sanity-check how visual evidence, inconsistency notes, or gap lists should read

Treat that file as a formatting reference only. Never reuse its example facts, values, or recommendations unless the user's source material independently supports them.

### Chinese heading set

### 来源清单 & 输出模式

Include:

- Source inventory and file-type classification
- Input quality level from L1 to L5
- Read method and evidence strength for each source
- Selected mode: `quick audit`, `full spec`, or `frontend handoff`
- Known limitations before extraction

### 设计体系总览 & 风格调性

Include:

- Product or business context visible from the materials
- Style keywords grounded in evidence
- System maturity and consistency level
- Key master-page and derived-page relationships

### 基础视觉规范（色彩 / 字体 / 圆角 / 阴影 / 间距 / 栅格 / 图标）

For each category:

- Summarize the observed rule set
- Use visual boards first: color swatches, typography samples, spacing bars, radius/elevation cards, grid diagrams, and icon samples when evidence is available
- Separate `[已确认规律]` and `[待补充规范]`
- Add `[统一建议]` only when the source is inconsistent or incomplete

### 页面模板 & 布局规范

Include:

- Page-type taxonomy
- Information hierarchy
- Structural zoning
- Module combination rules
- Master-page and derived-page mapping

### 核心设计原则

Output 5 to 10 principles. Keep them operational and reusable, not slogan-like.

### 设计不一致问题 & 统一优化建议

For each issue:

- What is inconsistent
- Where it appears
- Why it harms system quality or implementation efficiency
- The recommended standard

### 现有规范缺口 & 后续补齐方向

List the missing states, missing tokens, missing responsive rules, missing interaction specs, or missing accessibility constraints that prevent a fully closed design system.

### 前端交付资产（仅 frontend handoff 模式必需）

Include:

- Token inventory table
- CSS custom properties
- Tailwind theme extension
- Design Tokens JSON
- Implementation notes
- Accessibility and state coverage checklist
- Adoption checklist and migration risks

### English heading set

### Source Inventory & Output Mode

Include:

- Source inventory and file-type classification
- Input quality level from L1 to L5
- Read method and evidence strength for each source
- Selected mode: `quick audit`, `full spec`, or `frontend handoff`
- Known limitations before extraction

### Design System Overview & Style Direction

Include:

- Product or business context visible from the materials
- Style keywords grounded in evidence
- System maturity and consistency level
- Key master-page and derived-page relationships

### Foundational Visual Specifications (Color / Typography / Radius / Shadow / Spacing / Grid / Iconography)

For each category:

- Summarize the observed rule set
- Use visual boards first: color swatches, typography samples, spacing bars, radius/elevation cards, grid diagrams, and icon samples when evidence is available
- Separate `[Confirmed Pattern]` and `[Needs Specification]`
- Add `[Standardization Recommendation]` only when the source is inconsistent or incomplete

### Page Templates & Layout Rules

Include:

- Page-type taxonomy
- Information hierarchy
- Structural zoning
- Module combination rules
- Master-page and derived-page mapping

### Core Design Principles

Output 5 to 10 principles. Keep them operational and reusable, not slogan-like.

### Inconsistencies & Standardization Recommendations

For each issue:

- What is inconsistent
- Where it appears
- Why it harms system quality or implementation efficiency
- The recommended standard

### Specification Gaps & Next Completion Priorities

List the missing states, missing tokens, missing responsive rules, missing interaction specs, or missing accessibility constraints that prevent a fully closed design system.

### Frontend Handoff Assets (required only for frontend handoff mode)

Include:

- Token inventory table
- CSS custom properties
- Tailwind theme extension
- Design Tokens JSON
- Implementation notes
- Accessibility and state coverage checklist
- Adoption checklist and migration risks

## Writing rules

- Write for a standalone HTML report that designers and frontend engineers can use directly.
- Keep the document structured and implementation-oriented.
- Prefer normalized rules over page commentary.
- When you need to infer, make the uncertainty explicit.
- When you see inconsistency, do not ignore it. Call it out and recommend one standard.
- If a single rule appears only once, do not upgrade it to a system rule unless the source explicitly defines it.
- Avoid standalone sections named `完整组件规范手册` / `Complete Component Specification Manual` or `交互行为规范` / `Interaction Behavior Guidelines` unless the user explicitly requests them.
- Do not create a standalone section named `原图证据 & 可视化标注`, `Source Images & Visual Annotations`, or similar. Put any screenshot preview or annotation inside the related visual-spec or page-template section.
- Add generous vertical spacing between tables, insight callouts, code blocks, and the next subsection heading so headings never visually touch preceding content.
- When the user asks in English, translate the narrative and section headings into fluent English instead of preserving the Chinese template.
- When the user asks in Chinese, use the Chinese template by default.
- Do not translate source evidence into a new canonical token name unless the source explicitly defines that name.
- In `frontend handoff` mode, include code blocks for CSS custom properties, Tailwind theme extension, and Design Tokens JSON whenever source evidence supports them; otherwise include the section with explicit gaps.
