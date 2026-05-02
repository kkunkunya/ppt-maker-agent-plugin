# 安装说明

## 默认项目级启用

`ppt-maker` 的目标是“可分发”，但不是“每个 Agent 会话都默认加载”。

建议拆成两层：

1. **注册 marketplace**：可以做一次。它只是告诉 Claude Code 或 Codex 这个 plugin 在哪里。
2. **启用 plugin**：只在需要 PPT 生产的项目里做。

这样普通代码会话不会额外加载 PPT 规则，但需要做演示文稿时又能稳定启用。

## API Key

`ppt-maker` 本身不需要 API key。如果你的项目另行使用大模型、图片生成或文档转换后端，请在本地配置自己的 key。见 [API_KEYS_AND_LOCAL_CONFIG.zh-CN.md](API_KEYS_AND_LOCAL_CONFIG.zh-CN.md)。

## Claude Code

```bash
claude plugin marketplace add kkunkunya/ppt-maker-agent-plugin
cd /path/to/project
claude plugin install ppt-maker@ppt-maker-agent-plugin --scope project
claude plugin list
```

升级新版：

```bash
claude plugin update ppt-maker@ppt-maker-agent-plugin
```

## Codex

```bash
codex plugin marketplace add kkunkunya/ppt-maker-agent-plugin
codex -C /path/to/project \
  -c 'plugins."ppt-maker@ppt-maker-agent-plugin".enabled=true'
```

如果你曾经把它写进 `~/.codex/config.toml` 全局启用，建议改回：

```toml
[plugins."ppt-maker@ppt-maker-agent-plugin"]
enabled = false
```

然后只在需要做 PPT 的项目启动命令里临时启用。

## 手动兜底

如果 Agent 不支持 plugin：

1. 将本仓库 clone 或 vendor 到目标项目。
2. 让 Agent 先读 `plugins/ppt-maker/skills/ppt-route/SKILL.md`。
3. 路由后，再读取对应模式 skill。
4. 使用 `plugins/ppt-maker/_shared/references/` 下的输出模式、模板 schema 和验证规则。

OpenClaw、Hermes 和其他 crawler-style agent 参考 [AGENT_CRAWLER_GUIDE.zh-CN.md](AGENT_CRAWLER_GUIDE.zh-CN.md)。
