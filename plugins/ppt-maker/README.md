# ppt-maker

PPT production toolkit for separating display decks, image assets, editable PPTX deliverables, fixed-template filling, and verification.

## Activation

`ppt-maker` is a local, on-demand plugin. Keep it registered in the marketplace and Codex cache, but do not enable it globally by default. Project bootstrap or a presentation-specific workspace should opt it in when PPT production is part of the current job.

## Skills

| Skill | Purpose |
|---|---|
| `ppt-maker:ppt-route` | Route a PPT request to the correct output mode and enforce editability boundaries. |
| `ppt-maker:html-showcase` | Plan browser-first decks for recording, live display, and visual presentation. |
| `ppt-maker:image-assets` | Plan slide image assets without treating them as editable decks. |
| `ppt-maker:editable-pptx` | Plan object-level editable PowerPoint generation. |
| `ppt-maker:fixed-template-fill` | Plan schema-bound safe filling for locked templates. |
| `ppt-maker:deck-verification` | Verify deck artifacts before handoff. |

## Boundary

This plugin is mode-first. It must not turn an HTML deck, full-page PNG set, or image-based PPTX into a claimed editable PPTX deliverable unless the user explicitly accepts non-editability.
