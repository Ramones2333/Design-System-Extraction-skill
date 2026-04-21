# Design System Extraction Skill

`design-system-extraction` is a reusable Codex skill for turning design source materials into structured, implementation-ready design system documentation.

It is designed for cases where a user provides one or more of the following:

- Figma pages or frames
- UI component libraries
- High-fidelity screens or mockups
- Page-plus-component sets
- Partial or incomplete design specifications

Instead of redesigning the UI, this skill extracts the underlying system:

- visual language and design tokens
- foundational and business component rules
- page templates and layout patterns
- interaction guidance
- inconsistencies and standardization recommendations
- specification gaps and next completion priorities

## Repository structure

```text
.
├── README.md
├── LICENSE
└── design-system-extraction/
    ├── SKILL.md
    ├── LICENSE.txt
    ├── agents/
    │   └── openai.yaml
    └── references/
        └── output-examples.md
```

## What makes this skill useful

- It supports both Chinese and English triggers
- It automatically matches the output language to the user's request
- It distinguishes observed facts from recommended standardization
- It is optimized for implementation-ready output rather than page-by-page critique
- It includes a reference file with Chinese and English output examples

## Install in Codex

This repository is ready to install from GitHub by pointing Codex at the skill folder path inside the repo.

Example:

```text
$skill-installer install https://github.com/Ramones2333/Design-System-Extraction-skill/tree/main/design-system-extraction
```

Or install from a repo/path pair:

```text
scripts/install-skill-from-github.py --repo Ramones2333/Design-System-Extraction-skill --path design-system-extraction
```

After installing, restart Codex so the new skill is picked up.

## Example prompts

Chinese:

```text
用这些 Figma 页面帮我提炼完整设计系统，输出组件规范、页面模板、统一建议和规范缺口。
```

```text
请从这套后台页面和组件库里反推 design token、页面布局规则和业务组件规范。
```

English:

```text
Use these Figma frames to extract a reusable design system with tokens, component specs, page templates, and standardization recommendations.
```

```text
Reverse-engineer the UI system behind these screens and turn it into an implementation-ready design spec.
```

## Output shape

The skill produces a structured document that covers:

- design system overview and style direction
- foundational visual specifications
- complete component specification manual
- page templates and layout rules
- interaction behavior guidelines
- core design principles
- inconsistencies and standardization recommendations
- specification gaps and next completion priorities

## Notes for maintainers

- Keep `SKILL.md` focused on workflow and decision rules
- Put examples and format scaffolds in `references/`
- If you add more reference files, link them directly from `SKILL.md`
- Avoid turning the skill into a generic UI review skill; it is specifically for system extraction and specification

## License

This repository is licensed under Apache-2.0. The skill directory also includes a `LICENSE.txt` copy so the license stays attached when the skill is installed independently.
