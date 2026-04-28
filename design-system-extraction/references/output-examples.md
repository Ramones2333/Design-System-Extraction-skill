# Output Examples

This file is a formatting reference for `design-system-extraction`. It helps with section structure, tone, and evidence labeling. In real use, place these sections inside the HTML deliverable required by `SKILL.md`; do not return these examples as a plain Markdown report unless the user explicitly asks for Markdown.

Do not treat any example below as factual design guidance. All example tokens, components, numbers, and recommendations are placeholders. Replace them with source-backed findings from the user's materials.

## When to read this file

Read this reference only when:

- The user asks for an example deliverable
- You want a scaffold for the final document shape
- You need to check how Chinese and English versions should differ
- You want a sample of how to write visual evidence, inconsistency notes, or spec gaps

## Core writing pattern

- Start with system-level conclusions, not page-by-page narration
- Attach evidence labels to conclusions
- Separate observation from recommendation
- Keep the wording implementation-oriented
- If evidence is weak, say so directly
- For the final deliverable, convert the relevant section structure into semantic HTML sections, visual boards, contextual evidence blocks, tables, and code blocks.
- Do not include standalone component-manual or interaction-behavior sections unless the user explicitly asks for them.

## Chinese example

The following example shows the expected Chinese output style.

```md
### 设计体系总览 & 风格调性

- 系统定位：从页面结构与组件覆盖范围判断，该体系更接近中后台运营平台，强调高信息密度与高操作效率。
- 风格关键词：克制、理性、模块化、数据导向。
- [已确认规律]：列表页、详情页、表单页共享相同的标题区与操作区结构，说明页面骨架已具备稳定母版。
- [待补充规范]：未见明确的品牌表达层规范，无法确认品牌色在营销场景下的延展方式。

### 基础视觉规范（色彩 / 字体 / 圆角 / 阴影 / 间距 / 栅格 / 图标）

#### 色彩
- [已确认规律]：主操作按钮、选中态标签、分页当前态均复用同一主色，说明主品牌色已用于关键操作强调。
- [已确认规律]：中性色覆盖标题、正文、辅助说明、分割线四个层级，层次关系较清晰。
- [待补充规范]：未观察到完整语义色阶，成功、警告、危险状态在不同页面中存在表达缺口。
- [统一建议]：补齐 success / warning / error 的文字色、底色、描边色三级 token，并统一用于通知、Tag、表单校验与结果反馈。

#### 间距
- [已确认规律]：卡片内边距、表单项垂直间距、筛选区控件间距呈现有限档位复用。
- [待补充规范]：缺少明确的 spacing scale 命名与对应场景说明。

### 页面模板 & 布局规范

- 页面类型：列表页、详情页、编辑页、仪表盘页
- 信息层级：标题区 > 操作区 > 筛选区 > 内容主体 > 辅助说明
- [已确认规律]：列表页采用“标题区 + 筛选区 + 表格区 + 分页区”的稳定骨架。
- [统一建议]：详情页统一采用“两栏信息分组 + 底部操作区”，减少不同业务线的结构分歧。

### 核心设计原则

1. 优先保证高频任务路径的操作效率。
2. 用有限的视觉层级表达复杂信息，而不是增加装饰。
3. 同类模块保持同构布局，降低学习成本。
4. 组件状态优先标准化，再扩展业务差异。
5. 品牌表达让位于任务完成效率，但关键操作必须有明确强调。

### 设计不一致问题 & 统一优化建议

#### 问题 1：列表筛选区按钮对齐方式不一致
- 出现位置：列表页 A、列表页 B、弹窗内嵌列表
- 影响：前端难以复用统一容器，页面观感松散
- [统一建议]：统一操作按钮组右对齐，统计信息固定在左侧

#### 问题 2：Tag 语义色使用混乱
- 出现位置：状态 Tag、审批结果 Tag、风险等级 Tag
- 影响：同色不同义，削弱识别效率
- [统一建议]：建立语义色映射表，并限制业务色自定义范围

### 现有规范缺口 & 后续补齐方向

- 缺少响应式断点规则
- 缺少表单校验状态全量规范
- 缺少空状态与异常状态插图/文案规范
- 缺少动效时长、缓动曲线、出入场规则
- 缺少可访问性约束，如对比度、焦点顺序、键盘操作
```

## English example

The following example shows the expected English output style.

```md
### Design System Overview & Style Direction

- System type: Based on layout repetition and component coverage, this appears to be an enterprise operations platform optimized for dense information and fast task completion.
- Style keywords: restrained, rational, modular, data-forward.
- [Confirmed Pattern]: List, detail, and form pages share the same header and action-zone structure, which indicates a stable page master.
- [Needs Specification]: Brand-expression rules are not sufficiently visible, so the extension of brand color into non-functional surfaces remains unclear.

### Foundational Visual Specifications (Color / Typography / Radius / Shadow / Spacing / Grid / Iconography)

#### Color
- [Confirmed Pattern]: Primary actions, selected tags, and active pagination all reuse the same accent color, suggesting a consistent primary-action token.
- [Confirmed Pattern]: The neutral palette covers at least four text and divider levels, which creates a readable content hierarchy.
- [Needs Specification]: The semantic color system is incomplete; success, warning, and destructive states are not consistently defined across modules.
- [Standardization Recommendation]: Add a three-tier semantic token set for success / warning / error covering text, background, and border usage.

#### Spacing
- [Confirmed Pattern]: Card padding, form-item gaps, and filter-bar spacing reuse a limited number of spacing steps.
- [Needs Specification]: The spacing scale lacks visible naming and usage boundaries.

### Page Templates & Layout Rules

- Page types: list, detail, edit, dashboard
- Information hierarchy: title zone > action zone > filter zone > main content > supporting notes
- [Confirmed Pattern]: List pages consistently follow a header + filter + table + pagination structure.
- [Standardization Recommendation]: Standardize detail pages around a two-column grouped information layout with a persistent bottom action zone.

### Core Design Principles

1. Optimize for operational efficiency in high-frequency task paths.
2. Use limited visual layers to clarify complexity rather than decorating it.
3. Keep similar modules structurally isomorphic to reduce relearning cost.
4. Standardize component states before allowing business-specific divergence.
5. Let task completion efficiency lead, while preserving strong emphasis for critical actions.

### Inconsistencies & Standardization Recommendations

#### Issue 1: Filter-bar action alignment is inconsistent
- Where it appears: List page A, List page B, modal-embedded table
- Impact: Reduces container reusability and weakens visual discipline
- [Standardization Recommendation]: Right-align the action group and reserve the left side for filters and result summary

#### Issue 2: Semantic Tag colors are overloaded
- Where it appears: Status tags, approval-result tags, risk-level tags
- Impact: The same color carries different meanings, which reduces recognition speed
- [Standardization Recommendation]: Define a semantic mapping table and limit custom business color usage

### Specification Gaps & Next Completion Priorities

- Missing responsive breakpoint rules
- Missing full validation-state rules for form controls
- Missing empty-state and exception-state illustration/copy rules
- Missing motion duration, easing, and transition standards
- Missing accessibility constraints such as contrast, focus order, and keyboard support
```

## Quick reminder for real use

- Replace every placeholder with source-backed observations
- Keep only the section set that matches the active output language
- Do not output both Chinese and English versions unless the user asks for bilingual delivery
- Recommendation sections should solve observed inconsistency, not introduce arbitrary redesign
