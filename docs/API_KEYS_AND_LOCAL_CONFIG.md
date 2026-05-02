# API Keys And Local Config

`ppt-maker` does not need an API key by itself. It gives agents a safe PPT production route: HTML showcase, image assets, editable PPTX, fixed-template fill, or verification.

API keys only become relevant when your chosen agent or backend calls an external provider, such as:

- an LLM provider
- an image generation provider
- a PPTX/document conversion service
- a hosted automation platform

## Rule

Never commit real keys to this repository.

Use placeholders in Git:

```bash
cp examples/local-config.example.txt .env
```

Then edit `.env` locally:

```bash
OPENAI_API_KEY=your_real_key_here
ANTHROPIC_API_KEY=your_real_key_here
FAL_KEY=your_real_key_here
DASHSCOPE_API_KEY=your_real_key_here
```

The `.env` file is ignored by Git. Keep it local.

## Prompt For Customers

Give this to the customer when an agent needs a provider key:

```text
This project does not ship with API keys. Please create your own provider account, generate an API key, and configure it locally in your agent runtime or `.env` file. Do not paste real keys into GitHub issues, commits, README files, screenshots, or chat logs. After configuration, ask the agent to verify that the key is available without printing the key value.
```

## Prompt For Agents

```text
Do not look for maintainer-owned API keys in this repository.
This repository intentionally contains no real secrets.
If the workflow needs a provider key, ask the user to configure their own key in a local `.env`, environment variable, secret manager, or the target agent platform's secret UI.
Never write real keys into tracked files.
Never print key values in logs.
Verify secret presence only by checking whether the variable exists.
```
