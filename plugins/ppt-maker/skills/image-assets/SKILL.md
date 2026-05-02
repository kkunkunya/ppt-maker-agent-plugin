---
name: image-assets
description: Use for PPT covers, backgrounds, section dividers, concept diagrams, handdrawn explainer pages, and brand-style slide visuals. Not for editable .pptx delivery (use editable-pptx); not for fixed templates (use fixed-template-fill); not for browser-first showcase (use html-showcase); not for verification (use deck-verification). 触发关键词：PPT 封面 / 章节图 / 概念图 / 手绘讲解页 / 背景图 / slide cover / brand visual。
---

# Image Assets

Use this skill when the presentation needs visual assets: cover images, section images, concept diagrams, background plates, handdrawn explainer pages, or brand-style slide visuals.

## Method Call

```text
/image-assets(deck_context, asset_role, style_reference?, target_slot?) -> prompt + asset plan
```

## Boundary

An image asset is not a deck. A full-slide image inside `.pptx` is image-based and not object-level editable.

## Asset Roles

Choose one asset role before writing prompts:

- cover image
- section divider image
- concept visualization
- comparison plate
- workflow/system diagram
- data backdrop
- handdrawn explainer page
- UI/screenshot redesign
- background image with text-safe zone

## Prompt Rules

- Match the final placement ratio before generating.
- Leave editable text outside the image when the target is editable PPTX.
- Avoid baked-in titles, page numbers, footers, watermarks, and decorative slide chrome unless the asset itself is a final raster page.
- Reserve text-safe space when the image will sit behind editable slide text.
- For Chinese text inside images, keep `Required text only` short and exact.
- If text fidelity fails, prefer blank label spaces plus deterministic text overlay.

## Source Patterns

Use prior research as pattern sources:

- `PPT-Design-Prompt`: brand-style image prompts and safe zones.
- `guizang-ppt-skill`: electronic magazine asset proportions and no-slide-chrome image prompts.
- `ian-handdrawn-ppt`: raster handdrawn explainer page style locks.

Read `../../_shared/references/research-basis.md` when you need the local research path.

## Handoff Contract

Report:

- asset role and ratio
- prompt or generation brief
- output path if generated
- whether text is baked in
- how it will be used in HTML, raster, editable PPTX, or fixed-template mode

## 本 skill 的 deletion-spec

- **触发删除条件**：When image asset generation is fully owned by a media plugin with PPT-specific safe-zone and editability rules, this skill can be removed.
- **禁用方式**：Remove `plugins/ppt-maker/skills/image-assets/`, bump plugin version, regenerate marketplace files.
- **卸载清单**：Update `ppt-route`, `html-showcase`, `editable-pptx`, and docs referencing `image-asset-mode`.
