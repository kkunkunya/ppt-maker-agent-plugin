# Agent Crawler Guide

Some agent platforms, such as OpenClaw, Hermes, or custom browser/crawler agents, may not install Claude Code or Codex plugins directly. For those tools, give the agent this GitHub URL and ask it to crawl the repository:

```text
https://github.com/kkunkunya/ppt-maker-agent-plugin
```

## What The Agent Should Read

Read these files in order:

1. `README.md`
2. `docs/MENTAL_MODEL.md`
3. `docs/API_KEYS_AND_LOCAL_CONFIG.md`
4. `plugins/ppt-maker/skills/ppt-route/SKILL.md`
5. the matching skill under `plugins/ppt-maker/skills/`
6. any referenced file under `plugins/ppt-maker/_shared/references/`

## Copy-Paste Prompt For OpenClaw / Hermes / Other Agents

```text
Please crawl this GitHub repository:
https://github.com/kkunkunya/ppt-maker-agent-plugin

Purpose:
Install or emulate the ppt-maker agent plugin for this project only.

Important:
- Do not assume the repository contains API keys.
- Do not ask the maintainer for private keys.
- If a provider key is needed, ask the customer to configure their own key locally.
- Read docs/API_KEYS_AND_LOCAL_CONFIG.md before attempting any model or image-provider integration.

Reading order:
1. README.md
2. docs/MENTAL_MODEL.md
3. docs/API_KEYS_AND_LOCAL_CONFIG.md
4. plugins/ppt-maker/skills/ppt-route/SKILL.md
5. The routed sibling skill:
   - html-showcase
   - image-assets
   - editable-pptx
   - fixed-template-fill
   - deck-verification

Operating rule:
Always route the PPT request first. State the output mode, editability label, next skill, reason, and forbidden shortcut before producing artifacts.
```

## Customer Setup Checklist

- Clone or let the agent crawl the GitHub repository.
- Choose whether the target tool supports plugin installation or prompt-only emulation.
- Configure any required provider key in the customer's own local environment.
- Keep `.env` untracked.
- Run the agent with `ppt-route` before deck production.

