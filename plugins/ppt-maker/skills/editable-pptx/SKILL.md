---
name: editable-pptx
description: Use when the user needs an object-level editable .pptx where text/shapes/tables/charts stay editable after handoff. Not for fixed templates (→fixed-template-fill); browser-first decks (→html-showcase); cover assets (→image-assets); verification (→deck-verification). 触发关键词：editable pptx / 可编辑 PPT / 给我源文件 / .pptx 交付 / 客户要可改的 PPT。
---

# Editable PPTX

Use this skill when the user needs a real PowerPoint deliverable where text, images, shapes, tables, or charts remain editable after handoff.

## Method Call

```text
/editable-pptx(source_material, deck_goal, editability_requirements, template?) -> PPTX production plan
```

## Non-Negotiable Boundary

Do not satisfy an editable PPTX request with full-slide PNGs, a browser deck, or a PDF. If any slide must be rasterized, label the result as `partially editable` and list the affected slides.

Read `../../_shared/references/output-modes.md` when route or editability is unclear.

## Production Workflow

1. Define the editability promise:
   - `object-level editable`
   - `partially editable`
   - `image-based` only if explicitly accepted
2. Convert source material into a slide JSON outline:
   - slide type
   - title
   - body blocks
   - tables/charts
   - image assets
   - speaker notes when needed
3. Choose an implementation backend:
   - Prefer `python-pptx` for first MVP and Python-heavy workflows.
   - Consider `PptxGenJS` for Node-first from-scratch generation.
   - Do not use `pptx-automizer` as the default unless an existing template must be modified.
4. Keep text as text boxes/placeholders.
5. Keep images as image objects, not baked into whole-slide screenshots.
6. Keep charts/tables editable where the backend supports it; otherwise mark exceptions.
7. Run `ppt-maker:deck-verification` before handoff.

## Required Warnings

Warn or block when:

- The user asks for advanced animation, SmartArt, complex formulas, or chart types the backend cannot create editably.
- The requested font is unavailable locally.
- A template is fixed/locked; route to `ppt-maker:fixed-template-fill` instead.
- Render verification is unavailable.

## Minimal Acceptance

An editable PPTX handoff should include:

- `.pptx`
- preview PDF or rendered slide images when possible
- verification report
- editability label
- list of rasterized exceptions, if any

## 本 skill 的 deletion-spec

- **触发删除条件**：When a deterministic PPTX generator in `scripts/` fully owns editable deck generation with equivalent route safety, this skill can shrink to a wrapper or be merged into that generator skill.
- **禁用方式**：Remove `plugins/ppt-maker/skills/editable-pptx/`, bump plugin version, regenerate marketplace files.
- **卸载清单**：Update `ppt-route`, `deck-verification`, `README.md`, and any mode docs referencing `editable-pptx-mode`.
