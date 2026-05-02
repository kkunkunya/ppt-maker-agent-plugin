# Agent Install Prompt

Copy this into Claude Code, Codex, or another coding agent when you want it to install and use this plugin correctly.

```text
You are installing PPT Maker as a project-scoped agent plugin.

Goal:
- Make ppt-maker available for this project only.
- Do not enable it globally by default.
- Teach future agents that "PPT" is not one output type.

Mental model to preserve:
PPT production is like a print shop with multiple counters. The front desk routes the job. The stage booth makes browser decks. The image studio makes covers and diagrams. The PowerPoint desk makes editable PPTX. The template desk fills locked templates without moving protected regions. The QA desk verifies the result before handoff.

Key rule:
Beauty and editability are different promises. A full-slide image inside PowerPoint can look polished, but it is not an editable PPTX. If the user asks for editable PPTX, keep text, shapes, tables, charts, and images as separate editable objects wherever feasible. If rasterization is unavoidable, label it as partially editable and list the affected slides.

Install for Claude Code:
1. Run:
   claude plugin marketplace add kkunkunya/ppt-maker-agent-plugin
2. In the target project directory, run:
   claude plugin install ppt-maker@ppt-maker-agent-plugin --scope project
3. Verify:
   claude plugin list

Install for Codex:
1. Run:
   codex plugin marketplace add kkunkunya/ppt-maker-agent-plugin
2. Start Codex for the target project with:
   codex -C /path/to/project -c 'plugins."ppt-maker@ppt-maker-agent-plugin".enabled=true'

Fallback if plugin installation is unavailable:
1. Read plugins/ppt-maker/skills/ppt-route/SKILL.md first.
2. Route the request to exactly one primary mode:
   - html-showcase-mode
   - image-asset-mode
   - editable-pptx-mode
   - fixed-template-fill-mode
   - verification
3. Then read the matching sibling SKILL.md and any referenced file under plugins/ppt-maker/_shared/references/.

Operating policy:
- Always route ambiguous PPT requests before producing deck artifacts.
- Always state the editability label for PPTX output.
- Never satisfy an editable PPTX request with full-slide PNGs unless the user explicitly accepts image-based output.
- For fixed school/company templates, inspect template structure and protected regions before editing.
- Before handoff, run or plan deck verification and report evidence honestly.
```

