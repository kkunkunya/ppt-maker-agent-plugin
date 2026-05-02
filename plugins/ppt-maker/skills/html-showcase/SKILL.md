---
name: html-showcase
description: Use for browser-first PPT decks for video, live display, recording, or visual storytelling — high-visual one-off presentations where editability is not required. Not for editable .pptx (→editable-pptx); fixed templates (→fixed-template-fill); cover assets (→image-assets); routing (→ppt-route). 触发关键词：网页 PPT / HTML 演示 / 录屏 PPT / 直播 PPT / browser slides / reveal.js / live talk deck。
---

# HTML Showcase

Use this skill when the deck is primarily a screen experience: live talk, recording, video insertion, interactive browser slides, or a high-visual one-off presentation where editability is not required.

## Method Call

```text
/html-showcase(source_material, audience, duration, visual_style?) -> HTML deck plan + asset plan + verification plan
```

## Fit Check

Use HTML showcase when:

- The user says HTML is acceptable or editability is not required.
- Motion, browser rendering, keyboard navigation, or recording matters.
- The deck is for a talk, demo day, private sharing, product narrative, or video chapter.

Do not use it when:

- The user needs `.pptx` with editable objects.
- A fixed school/company template must be preserved.
- The output will be revised by nontechnical PowerPoint users.

## Workflow

1. Route through `ppt-maker:ppt-route` if editability is unclear.
2. Confirm audience, duration, material source, image availability, and hard constraints.
3. Plan a slide rhythm before writing any page:
   - hook
   - context
   - core points
   - contrast or shift
   - takeaway
4. Choose implementation family:
   - `guizang-style single HTML` for electronic magazine presentation.
   - `Slidev/reveal-style` for Markdown-driven technical talks.
   - static HTML screenshots for video frame pipelines.
5. Plan assets with `ppt-maker:image-assets` if covers, diagrams, or explainer images are needed.
6. Verify with `ppt-maker:deck-verification` using browser screenshots or rendered PDF/PNG.

## Handoff Contract

When finishing a plan or implementation, state:

- artifact type: HTML / PDF / screenshots / video frames
- editability: not editable in PowerPoint
- source folder
- preview command or file path
- screenshot/render evidence

## 本 skill 的 deletion-spec

- **触发删除条件**：When HTML deck creation is fully handled by a more specific frontend or presentation plugin with equivalent PPT routing safeguards, this skill can be removed.
- **禁用方式**：Remove `plugins/ppt-maker/skills/html-showcase/`, bump plugin version, regenerate marketplace files.
- **卸载清单**：Update `ppt-route` routing table, `README.md`, and any references to `html-showcase-mode`.
