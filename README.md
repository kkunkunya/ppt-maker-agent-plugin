# PPT Maker Agent Plugin

Project-scoped PPT production routing for Claude Code, Codex, and other coding agents.

Most agent-made decks fail for a simple reason: the agent treats every "PPT" request as the same artifact. This plugin makes the agent ask the first important question: **what kind of deck are we delivering?**

## The Mental Model

Think of PPT production like a small print shop with different counters:

| Counter | What it makes | Plugin skill |
|---|---|---|
| Front desk | Decides which counter should handle the job | `ppt-maker:ppt-route` |
| Stage booth | Browser decks for recording, live talks, and visual storytelling | `ppt-maker:html-showcase` |
| Image studio | Covers, backgrounds, diagrams, handdrawn explainers | `ppt-maker:image-assets` |
| PowerPoint desk | Object-level editable `.pptx` files | `ppt-maker:editable-pptx` |
| Template desk | School/company/defense templates where logos and layout cannot move | `ppt-maker:fixed-template-fill` |
| QA desk | Checks editability, rendering, template safety, and evidence | `ppt-maker:deck-verification` |

The key distinction is editability. A full-slide PNG inside PowerPoint is like a poster behind glass: it can look good, but the user cannot edit the text and objects. An editable PPTX is more like a Lego model: text boxes, shapes, tables, charts, and images remain separate pieces.

## What This Is

`ppt-maker` is a skill-only plugin for routing and enforcing PPT delivery boundaries. It is useful when an agent needs to decide between:

- an HTML showcase deck
- image assets for slides
- a raster/image-based deck
- an object-level editable PPTX
- a fixed-template PPTX fill
- a pre-handoff verification report

It is intentionally **project-scoped**. Register the marketplace globally if your tool requires it, but enable the plugin only in projects where presentation work is part of the job.

## Install

### Claude Code

```bash
claude plugin marketplace add kkunkunya/ppt-maker-agent-plugin
cd /path/to/your-presentation-project
claude plugin install ppt-maker@ppt-maker-agent-plugin --scope project
```

Use `--scope local` if you want the plugin only for the current checkout on this machine.

### Codex

```bash
codex plugin marketplace add kkunkunya/ppt-maker-agent-plugin
codex -C /path/to/your-presentation-project \
  -c 'plugins."ppt-maker@ppt-maker-agent-plugin".enabled=true'
```

The first command registers the marketplace. The second starts Codex with `ppt-maker` enabled for that project session.

### Other Agents

If your agent does not support Claude/Codex plugin manifests, copy the prompt in [docs/AGENT_INSTALL_PROMPT.md](docs/AGENT_INSTALL_PROMPT.md). The fallback is simple: make the agent read `plugins/ppt-maker/skills/ppt-route/SKILL.md` first, then read the sibling skill that matches the output mode.

## Typical Use

Ask your agent:

```text
Use ppt-maker. I need a 12-slide defense deck from this material.
The school template must stay intact, and the logo/header/footer cannot move.
Route the request first, then produce only a safe fill plan unless the template schema is clear.
```

For a visually rich recording deck:

```text
Use ppt-maker. I need browser-first slides for a 6-minute video segment.
HTML is acceptable. Do not claim this is an editable PPTX.
Route first, then plan the HTML showcase deck and any image assets.
```

For customer handoff:

```text
Use ppt-maker. I need an editable PPTX that the client can revise later.
Keep text as text, charts/tables editable where feasible, and run deck verification before handoff.
```

## Repository Layout

```text
plugins/ppt-maker/                 # plugin source
plugins/ppt-maker/skills/          # six route/mode/verification skills
plugins/ppt-maker/_shared/         # mode, template, and verification references
.claude-plugin/marketplace.json    # Claude marketplace manifest
.agents/plugins/marketplace.json   # Codex marketplace manifest
docs/                              # install prompts and mental model docs
```

## Boundaries

- This plugin does not pretend HTML decks are editable PPTX files.
- This plugin does not claim full-slide PNG decks are editable.
- Fixed-template work must inspect the template and define safe zones before filling.
- Verification must report `pass`, `pass_with_warnings`, `partial`, `blocked`, or `failed` honestly.
- There is no deterministic PPTX generation backend in v0.1.0. The plugin provides routing, guardrails, and handoff contracts for agents.

## License

MIT

