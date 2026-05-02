# PPT Output Modes

Use this file when choosing or reviewing a PPT output mode.

## Mode Map

| Mode | Use When | Output | Hard Boundary |
|---|---|---|---|
| `html-showcase-mode` | User needs live display, recording, web slides, motion, or visual storytelling and accepts non-editability. | HTML deck, screenshots, PDF, video frames. | Do not claim editable PowerPoint output. |
| `raster-image-deck-mode` | User wants handdrawn pages, visual essay pages, covers, or slides as final images. | PNG pages, contact sheet, optional image-based PPTX. | Image-based PPTX is not editable PPTX. |
| `image-asset-mode` | User needs slide backgrounds, covers, concept visuals, or diagram assets. | PNG/SVG assets and prompts. | Assets are inputs to a deck, not the deck itself. |
| `editable-pptx-mode` | User needs `.pptx`, editability, customer/teacher/team delivery, or object-level future edits. | Object-level PPTX with editable text/images/shapes/tables/charts where feasible. | Do not use full-slide images as the default. |
| `fixed-template-fill-mode` | User provides or references a fixed school/company/defense template. | PPTX based on the template, modified only inside allowed areas. | Inspect template and define a schema before filling. |
| `verification` | Any deck artifact is about to be handed off. | Report, preview render, structural checks, warnings. | Report failed checks honestly. |

## Editability Labels

Every PPTX handoff must label one of:

- `object-level editable`: text and major objects remain editable.
- `partially editable`: some assets are rasterized, clearly listed.
- `image-based`: pages are full-slide images; this is for display only.

If the user did not explicitly accept non-editability, treat `image-based` as a failed route for PPTX delivery.

## Routing Phrases

| User Phrase | Route |
|---|---|
| "视频里展示", "录屏", "web slides", "可以不可编辑" | `html-showcase-mode` or `raster-image-deck-mode` |
| "交付 PPTX", "可编辑", "老师要改", "客户要改", "PowerPoint 文件" | `editable-pptx-mode` |
| "固定模板", "答辩模板", "单位模板", "logo 不能动", "只能填" | `fixed-template-fill-mode` |
| "封面图", "背景图", "手绘说明图", "概念图" | `image-asset-mode` |

