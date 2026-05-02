# Agent 爬取指南

OpenClaw、Hermes 或一些自定义浏览器/爬虫 Agent 可能不能直接安装 Claude Code 或 Codex plugin。遇到这类工具时，把下面这个 GitHub 链接给 Agent，让它自己爬取仓库：

```text
https://github.com/kkunkunya/ppt-maker-agent-plugin
```

## Agent 应该读什么

按顺序读取：

1. `README.zh-CN.md`
2. `docs/MENTAL_MODEL.zh-CN.md`
3. `docs/API_KEYS_AND_LOCAL_CONFIG.zh-CN.md`
4. `plugins/ppt-maker/skills/ppt-route/SKILL.md`
5. `plugins/ppt-maker/skills/` 下路由到的对应 skill
6. `plugins/ppt-maker/_shared/references/` 下被引用的规则文件

## 给 OpenClaw / Hermes / 其他 Agent 的复制 Prompt

```text
请爬取这个 GitHub 仓库：
https://github.com/kkunkunya/ppt-maker-agent-plugin

目标：
在当前项目中安装或模拟 ppt-maker agent plugin。

重要边界：
- 不要假设仓库里有 API key。
- 不要向维护者索要私有 key。
- 如果需要服务商 key，请让客户自己在本地配置自己的 key。
- 尝试接入任何模型或图片服务前，先读 docs/API_KEYS_AND_LOCAL_CONFIG.zh-CN.md。

读取顺序：
1. README.zh-CN.md
2. docs/MENTAL_MODEL.zh-CN.md
3. docs/API_KEYS_AND_LOCAL_CONFIG.zh-CN.md
4. plugins/ppt-maker/skills/ppt-route/SKILL.md
5. 根据 route 结果读取 sibling skill：
   - html-showcase
   - image-assets
   - editable-pptx
   - fixed-template-fill
   - deck-verification

执行规则：
任何 PPT 请求都必须先 route。生成产物前，先说明 output mode、editability label、next skill、reason 和 forbidden shortcut。
```

## 客户配置清单

- clone 仓库，或让 Agent 爬取 GitHub 链接。
- 判断目标工具支持 plugin 安装，还是只能 prompt-only 模拟。
- 如需服务商 key，让客户在自己的本地环境配置。
- `.env` 保持 untracked。
- 做 deck 前先跑 `ppt-route`。

