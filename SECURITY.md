# Security Policy

## API Keys

This repository must not contain real API keys, tokens, cookies, private endpoints, or customer secrets.

`ppt-maker` itself does not require an API key. It is a routing and guardrail plugin. If a downstream agent uses an LLM, image model, PPTX generator, or hosted service, the user must configure their own keys outside Git.

Recommended places for real secrets:

- local `.env` files ignored by Git
- shell environment variables
- macOS Keychain, 1Password, or another secret manager
- GitHub Actions repository secrets, if CI is added later
- the target agent platform's own secret/config UI

Committed examples should use placeholders only, such as `examples/local-config.example.txt`.

## Before Publishing

Run a secret scan before pushing:

```bash
rg -n "sk-|ghp_|gho_|api[_-]?key|secret|token|password|BEGIN [A-Z ]*PRIVATE KEY" .
git status --short --ignored .env
```

Expected result:

- no real secret values in tracked files
- local `.env` appears ignored

## If A Secret Is Committed

1. Revoke the exposed key immediately in the provider dashboard.
2. Remove the secret from the repository.
3. Rotate any dependent credentials.
4. Treat public Git history as already copied.
