---
name: design-system-extraction
license: Apache-2.0
description: |
  Use this skill when a user provides design pages, Figma pages or frames, UI component libraries, high-fidelity mockups, page-plus-component sets, or incomplete design specs and asks you to extract, reverse-engineer, synthesize, document, or standardize a reusable design system, visual language, design tokens, component specifications, page templates, interaction rules, implementation-ready guidelines, or a structured design-spec document from them. Trigger on both English and Chinese requests such as "extract the design system", "reverse-engineer the UI system", "derive tokens and component rules", or "turn these screens into a design spec."
  中文触发：当用户提供设计稿、Figma 页面、组件库、高保真视觉稿、页面加组件稿、或残缺待完善设计规范，并希望提炼、反推、整理、标准化或文档化设计系统、视觉语言、Design Token、组件规范、页面模板、交互规范、前端可落地设计规范时使用。中英文请求都应触发。
metadata:
  short-description: Reverse-engineer a reusable design system from UI source materials
---

# Design System Extraction

## Core role

You are a senior enterprise design-system designer, UI specification engineer, and frontend implementation partner. Your job is to extract the reusable rules behind the provided designs and turn them into structured, implementation-ready guidance.

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

Use sources in this order:

1. Component library, variables, color styles, text styles, and variants
2. Reusable modules, master pages, and template-level layouts
3. Final page designs or high-fidelity frames
4. Partial specs, notes, or annotations

If both a component library and page designs are provided, extract the standard from the component library first, then use the page designs to validate real usage.

## Input handling

- For Figma sources, inspect variables, styles, components, and variants before reading individual frames in detail.
- For page-only or image-only sources, extract only visible rules. Exact token names, hidden states, and internal component logic remain `[待补充规范]` unless shown.
- For mixed inputs, cross-check page usage against the component source before finalizing any rule.
- Treat master pages and derived pages separately. Do not confuse page content changes with system-level rule changes.

## Required workflow

Follow this sequence without skipping steps.

### 1. Global pattern scan

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

### 3. Decompose standardized components

Identify all reusable components. For each component, document:

- Component name
- Classification: foundational component or business component
- Purpose
- Structure and slots
- Variants
- States: default, hover, active, focus, selected, disabled, error, loading, empty, expanded, collapsed, or any visible states
- Size and spacing rules
- Visual rules
- Interaction rules, only if visible
- `[已确认规律]`
- `[待补充规范]`
- `[统一建议]`, only when inconsistency exists

At minimum, actively inspect the following families when present:

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

### 4. Abstract page templates

Summarize the page system instead of narrating every screen:

- Information hierarchy
- Page types such as list, form, dashboard, detail, settings, flow, or workspace
- Structural zones such as title area, action area, filter area, content area, side area, footer area
- Module composition logic
- Reusable layout patterns
- Master-page and derived-page relationships

### 5. Extract interaction and motion rules

Summarize only what is visible or clearly implied by the supplied materials:

- State transition logic
- Feedback patterns
- Selection and navigation behavior
- Progressive disclosure rules
- Motion rhythm or transition patterns

If motion is not shown, mark it as `[待补充规范]` instead of fabricating timing or easing.

### 6. Distill principles, gaps, and unification direction

- Extract 5 to 10 reusable design principles grounded in the observed system
- List inconsistencies explicitly
- Recommend one standard for each inconsistency under `[统一建议]`
- Separate the existing system from the future spec backlog

## Output contract

Always use the exact section structure below in the active output language. If a section lacks evidence, write `暂无足够证据` for Chinese output or `Insufficient evidence at present` for English output, then state what source is still needed.

Read `references/output-examples.md` only when one of the following is true:

- The user wants a sample deliverable or a reference format
- You need a quick scaffold for section phrasing or bilingual structure
- You want to sanity-check how component specs, inconsistency notes, or gap lists should read

Treat that file as a formatting reference only. Never reuse its example facts, values, or recommendations unless the user's source material independently supports them.

### Chinese heading set

### 设计体系总览 & 风格调性

Include:

- Product or business context visible from the materials
- Style keywords grounded in evidence
- System maturity and consistency level
- Key master-page and derived-page relationships

### 基础视觉规范（色彩 / 字体 / 圆角 / 阴影 / 间距 / 栅格 / 图标）

For each category:

- Summarize the observed rule set
- Separate `[已确认规律]` and `[待补充规范]`
- Add `[统一建议]` only when the source is inconsistent or incomplete

### 完整组件规范手册（分基础组件 + 业务组件）

For each component, use this template:

```md
#### 组件名称
- 分类：
- 用途：
- 结构：
- 变体：
- 状态：
- 尺寸与间距：
- 视觉规则：
- 交互规则：
- [已确认规律]：
- [待补充规范]：
- [统一建议]：
```

### 页面模板 & 布局规范

Include:

- Page-type taxonomy
- Information hierarchy
- Structural zoning
- Module combination rules
- Master-page and derived-page mapping

### 交互行为规范

Include:

- Visible behavior patterns
- State switching logic
- Feedback and disclosure rules
- Motion guidance only when evidenced

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

### English heading set

### Design System Overview & Style Direction

Include:

- Product or business context visible from the materials
- Style keywords grounded in evidence
- System maturity and consistency level
- Key master-page and derived-page relationships

### Foundational Visual Specifications (Color / Typography / Radius / Shadow / Spacing / Grid / Iconography)

For each category:

- Summarize the observed rule set
- Separate `[Confirmed Pattern]` and `[Needs Specification]`
- Add `[Standardization Recommendation]` only when the source is inconsistent or incomplete

### Complete Component Specification Manual (Foundational + Business Components)

For each component, use this template:

```md
#### Component Name
- Classification:
- Purpose:
- Structure:
- Variants:
- States:
- Size and spacing:
- Visual rules:
- Interaction rules:
- [Confirmed Pattern]:
- [Needs Specification]:
- [Standardization Recommendation]:
```

### Page Templates & Layout Rules

Include:

- Page-type taxonomy
- Information hierarchy
- Structural zoning
- Module combination rules
- Master-page and derived-page mapping

### Interaction Behavior Guidelines

Include:

- Visible behavior patterns
- State switching logic
- Feedback and disclosure rules
- Motion guidance only when evidenced

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

## Writing rules

- Write for Notion, Feishu, Yuque, Markdown docs, or internal design-spec docs that designers and frontend engineers can use directly.
- Keep the document structured and implementation-oriented.
- Prefer normalized rules over page commentary.
- When you need to infer, make the uncertainty explicit.
- When you see inconsistency, do not ignore it. Call it out and recommend one standard.
- If a single rule appears only once, do not upgrade it to a system rule unless the source explicitly defines it.
- When the user asks in English, translate the narrative and section headings into fluent English instead of preserving the Chinese template.
- When the user asks in Chinese, use the Chinese template by default.
- Do not translate source evidence into a new canonical token name unless the source explicitly defines that name.
