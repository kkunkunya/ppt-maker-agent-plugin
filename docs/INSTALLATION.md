# Installation

## Project-Scoped By Default

`ppt-maker` is designed to be available as a distributable marketplace plugin, but not loaded into every agent session.

Use this split:

1. **Marketplace registration**: safe to do once. This tells Claude Code or Codex where the plugin lives.
2. **Plugin enablement**: do this only inside a project that needs PPT production.

That keeps normal coding sessions lighter while preserving a repeatable install path.

## API Keys

`ppt-maker` itself does not require any API key. If your project uses a separate LLM, image generation, or document conversion backend, configure your own key locally. See [API_KEYS_AND_LOCAL_CONFIG.md](API_KEYS_AND_LOCAL_CONFIG.md).

## Claude Code

```bash
claude plugin marketplace add kkunkunya/ppt-maker-agent-plugin
cd /path/to/project
claude plugin install ppt-maker@ppt-maker-agent-plugin --scope project
claude plugin list
```

Use:

```bash
claude plugin update ppt-maker@ppt-maker-agent-plugin
```

when a newer release is available.

## Codex

```bash
codex plugin marketplace add kkunkunya/ppt-maker-agent-plugin
codex -C /path/to/project \
  -c 'plugins."ppt-maker@ppt-maker-agent-plugin".enabled=true'
```

If you temporarily enabled it globally in `~/.codex/config.toml`, set it back to:

```toml
[plugins."ppt-maker@ppt-maker-agent-plugin"]
enabled = false
```

Then enable it only for presentation work with the command-line override above.

## Manual Fallback

For agents without plugin support:

1. Vendor or clone this repository into the target project.
2. Tell the agent to read `plugins/ppt-maker/skills/ppt-route/SKILL.md`.
3. After routing, tell it to read the selected mode skill.
4. Use `plugins/ppt-maker/_shared/references/` for output mode, template schema, and verification rules.

For OpenClaw, Hermes, and other crawler-style agents, use [AGENT_CRAWLER_GUIDE.md](AGENT_CRAWLER_GUIDE.md).
