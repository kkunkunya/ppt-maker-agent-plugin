---
name: fixed-template-fill
description: Use for filling school/company/defense PPTX templates without moving protected layout, logo, header, footer, or decoration. Not for free-form editable decks (→editable-pptx); browser showcase (→html-showcase); cover/diagram assets (→image-assets); verification (→deck-verification). 触发关键词：模板填充 / 学校模板 / 答辩模板 / 校徽不能动 / 占位符替换 / fixed template fill。
---

# Fixed Template Fill

Use this skill when the user provides, references, or is constrained by a fixed PowerPoint template.

## Method Call

```text
/fixed-template-fill(template_pptx, content, constraints?) -> schema + safe fill plan
```

## Core Rule

A fixed template task is not free-form slide design. Treat it as constrained writing into a known layout. Inspect first, write second.

Read `../../_shared/references/template-schema.md` before defining or reviewing a schema.

## Workflow

1. Confirm the template file exists.
2. Inspect the template:
   - slide size
   - masters and layouts
   - placeholder idx/type/name
   - shape names and bounding boxes
   - protected regions such as logo/header/footer
   - risky objects such as animation, video, SmartArt, complex charts
3. Create or update a template schema.
4. Map user content to allowed placeholders or free zones.
5. Refuse or split content that does not fit.
6. Write only inside allowed placeholders or allowed free zones.
7. Do not edit slide master/layout in MVP mode.
8. Run `ppt-maker:deck-verification`.

## Safe Fill Policy

Priority order:

1. Fill existing placeholders.
2. Replace media in explicitly named image placeholders.
3. Update explicitly allowed chart/table data.
4. Add new text/image shapes only inside schema `free_zones`.
5. If none fit, report `blocked` with the missing slot.

## Block Conditions

Return `blocked` instead of improvising when:

- No template file is available.
- No schema can be derived or approved.
- Content requires moving protected template elements.
- Required content exceeds the allowed region and cannot be shortened or split.
- The template uses unsupported objects that affect the target slide.

## Handoff Contract

Report:

- template file
- schema path
- modified slides and allowed slots used
- forbidden regions checked
- editability label
- preview/render evidence
- warnings

## 本 skill 的 deletion-spec

- **触发删除条件**：When a deterministic fixed-template filler and schema inspector fully enforce the same safety rules, this skill can become a thin instruction wrapper.
- **禁用方式**：Remove `plugins/ppt-maker/skills/fixed-template-fill/`, bump plugin version, regenerate marketplace files.
- **卸载清单**：Update `ppt-route`, `deck-verification`, shared `template-schema.md`, and docs referencing `fixed-template-fill-mode`.
