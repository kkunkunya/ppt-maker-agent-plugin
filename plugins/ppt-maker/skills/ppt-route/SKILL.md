---
name: ppt-route
description: Route ambiguous PPT requests to html-showcase / image-assets / editable-pptx / fixed-template-fill / deck-verification by output mode and editability. Use first when the user says "做 PPT / slides / deck / 演示文稿 / 答辩 / PPTX" and target mode is not fixed. Not for deck production (→ four sibling skills); not for handoff QA (→deck-verification). 触发关键词：做 PPT / 帮我做个 deck / 准备演示文稿 / 做答辩 / PPT 该用哪种。
---

# PPT Route

Use this skill first when the user says "做 PPT", "slides", "deck", "演示文稿", "答辩", or "PPTX" and the output mode is not already mechanically fixed.

## Method Call

```text
/ppt-route(request, inputs?, delivery_context?) -> mode + editability_label + required_next_skill
```

## Core Rule

Separate display value from editability. A good-looking HTML deck, PNG page set, or image-based PPTX is not an editable PPTX deliverable unless the user explicitly accepts non-editability.

Read `../../_shared/references/output-modes.md` when you need the full mode table.

## Routing Order

Apply the first matching route:

1. User provided `.pptx` or `.potx`, or says fixed template / defense template / company template / logo cannot move:
   - Route to `ppt-maker:fixed-template-fill`.
   - Require template schema before filling.
2. User says editable, customer/teacher/team delivery, `.pptx`, PowerPoint file, someone needs to revise it:
   - Route to `ppt-maker:editable-pptx`.
   - Require `object-level editable` or `partially editable` label.
3. User says video, recording, live talk, browser presentation, HTML is fine, not editable is fine:
   - Route to `ppt-maker:html-showcase`.
4. User asks for cover image, background image, handdrawn explainer, concept visual, or slide asset:
   - Route to `ppt-maker:image-assets`.
5. User is about to receive any deck artifact:
   - Route to `ppt-maker:deck-verification`.

If none match, default to `ppt-maker:editable-pptx` for safety because editable output is harder to recover after the wrong route.

## Required Output

Return a short routing block before doing downstream work:

```text
Mode: editable-pptx-mode
Editability: object-level editable
Next skill: ppt-maker:editable-pptx
Reason: user asked for a PPTX deliverable that others can revise.
Forbidden shortcut: do not use full-slide PNG pages unless user accepts image-based PPTX.
```

## Boundary Checks

- If a route would output image-based PPTX, say so explicitly.
- If a fixed template is mentioned but no template file exists, ask for the template or mark blocked.
- If a user asks for both "best visual effect" and "editable PPTX", keep editable as the hard constraint and move complex visuals into separate editable-friendly assets.
- If the request mixes video showcase and formal PPTX delivery, split into two artifacts instead of compromising both.

## 本 skill 的 deletion-spec

- **触发删除条件**：当 PPT plugin 的 top-level router can reliably infer editability and template constraints without a dedicated skill, this routing skill can be folded into the plugin root.
- **禁用方式**：Remove `plugins/ppt-maker/skills/ppt-route/`, bump `ppt-maker` version, regenerate marketplace files.
- **卸载清单**：Update `plugins/ppt-maker/README.md`, marketplace outputs, and any skill descriptions that reference `ppt-maker:ppt-route`.
