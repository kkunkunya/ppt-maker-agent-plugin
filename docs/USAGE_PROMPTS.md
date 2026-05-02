# Usage Prompts

## Route An Ambiguous PPT Request

```text
Use ppt-maker:ppt-route.
I need a PPT/deck, but the output mode is not fixed yet.
Ask only for missing constraints that change the route.
Then return:
- Mode
- Editability label
- Next skill
- Reason
- Forbidden shortcut
```

## Editable PPTX

```text
Use ppt-maker:editable-pptx.
I need an object-level editable PowerPoint file.
Keep text, images, shapes, tables, and charts editable where feasible.
If any slide or element must be rasterized, label it as partially editable and list the exceptions.
Run or plan ppt-maker:deck-verification before handoff.
```

## Fixed Template Fill

```text
Use ppt-maker:fixed-template-fill.
The template layout, logo, header, footer, and institutional marks are protected.
Inspect placeholders, shape names, bounding boxes, and forbidden regions before filling.
If content does not fit the allowed slot, report blocked or split the slide. Do not move protected regions.
```

## HTML Showcase

```text
Use ppt-maker:html-showcase.
This deck is for live display, recording, or a video segment.
HTML is acceptable and PowerPoint editability is not required.
Plan the slide rhythm, visual direction, preview command, and verification screenshots.
Do not claim the output is an editable PPTX.
```

## Image Assets

```text
Use ppt-maker:image-assets.
Create slide visual assets such as covers, section dividers, concept diagrams, backgrounds, or handdrawn explainers.
Keep final slide text outside the image unless the user explicitly wants a raster page.
State the ratio, safe text zone, prompt, output path, and whether text is baked in.
```

## Verification

```text
Use ppt-maker:deck-verification.
Verify this deck before handoff.
Check editability label, slide count, render preview, text overflow, missing fonts, broken media, template forbidden regions, and whether the promised output mode is honest.
Return pass, pass_with_warnings, partial, blocked, or failed with evidence paths.
```

