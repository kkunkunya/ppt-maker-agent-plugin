---
name: deck-verification
description: Use before handing off PPTX, HTML, image-based decks, or slide assets. Verify editability, rendering, template safety, and evidence. Not for actual deck production (those are editable-pptx / fixed-template-fill / html-showcase / image-assets); not for routing the request (that is ppt-route). 触发关键词：deck verification / PPT 自查 / PPT 验收 / PPTX 可编辑性检查 / 模板安全检查 / 交付前自查 / pre-handoff QA / slide evidence。
---

# Deck Verification

Use this skill before claiming a PPT, HTML deck, image-based deck, or slide asset set is ready.

## Method Call

```text
/deck-verification(artifact_paths, promised_mode, constraints?) -> status + evidence
```

## Verification Source

Read `../../_shared/references/verification-gates.md` for detailed checks.

## Verification Flow

1. Identify the promised mode and editability label.
2. Confirm all expected files exist.
3. Run structural checks where possible:
   - PPTX shape bounds
   - placeholder use
   - forbidden region overlap
   - object editability
   - image dimensions
4. Render or preview:
   - PowerPoint export when available.
   - LibreOffice/headless renderer as fallback for PPTX.
   - Browser screenshots for HTML decks.
   - Contact sheet for image decks.
5. Inspect output for clipping, overflow, missing fonts, covered logos, broken media, and blank slides.
6. Write a report with one of: `pass`, `pass_with_warnings`, `partial`, `blocked`, `failed`.

## Hard Fails

Mark failed or blocked when:

- User requested editable PPTX but artifact is image-based.
- Fixed-template fill was done without a template schema.
- Any generated object overlaps a forbidden region.
- PPTX opens only after repair.
- Verification render cannot be produced and no alternative evidence exists.

## Final Report Shape

```markdown
status: pass_with_warnings
artifact: out.pptx
promised_mode: editable-pptx-mode
editability: object-level editable
checks:
- structure: pass
- render: pass
- font: warning
- template safety: not applicable
warnings:
- Font PingFang SC not found in fallback renderer.
evidence:
- preview: verification/rendered/slide-001.png
- command: "render command and verifier command used for this artifact"
```

## 本 skill 的 deletion-spec

- **触发删除条件**：When deterministic verification scripts cover all mode checks and are automatically invoked by the plugin, this skill can shrink to a report-format reference.
- **禁用方式**：Remove `plugins/ppt-maker/skills/deck-verification/`, bump plugin version, regenerate marketplace files.
- **卸载清单**：Update `ppt-route`, all mode skills, shared `verification-gates.md`, and any handoff templates requiring deck verification.
