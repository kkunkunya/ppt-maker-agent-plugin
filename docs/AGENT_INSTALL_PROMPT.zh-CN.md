# Agent 安装 Prompt

把下面这段复制给 Claude Code、Codex 或其他 Coding Agent，用来正确安装和使用这个 plugin。

```text
你正在安装 PPT Maker，要求是项目级 agent plugin。

目标：
- 让 ppt-maker 只在当前项目可用。
- 不要默认全局启用。
- 让后续 Agent 明白：“PPT”不是单一产物。
- 不要期望仓库里有维护者自己的 API key。

必须保留的认知模型：
PPT 生产像一家印刷店，有多个柜台。前台负责路由；舞台间做网页演示；图片工作室做封面和图解；PowerPoint 柜台做可编辑 PPTX；模板柜台填固定模板且不能移动保护区域；质检柜台在交付前验证结果。

关键规则：
好看和可编辑是两个不同承诺。整页图片放进 PowerPoint 可以很精致，但它不是可编辑 PPTX。如果用户要可编辑 PPTX，文字、形状、表格、图表、图片应尽量保持独立对象。若必须栅格化，必须标注 partially editable，并列出受影响页面。

Claude Code 安装：
1. 执行：
   claude plugin marketplace add kkunkunya/ppt-maker-agent-plugin
2. 在目标项目目录执行：
   claude plugin install ppt-maker@ppt-maker-agent-plugin --scope project
3. 验证：
   claude plugin list

Codex 安装：
1. 执行：
   codex plugin marketplace add kkunkunya/ppt-maker-agent-plugin
2. 为目标项目启动 Codex：
   codex -C /path/to/project -c 'plugins."ppt-maker@ppt-maker-agent-plugin".enabled=true'

API key 策略：
- ppt-maker 本身不需要 API key。
- 如果下游模型/图片/后端服务需要 key，请让客户自己在本地配置自己的 key。
- 使用本地 `.env`、环境变量、密钥管理器或目标 Agent 平台的 secret UI。
- 不要把真实 key 写进 Git、README、issue、截图或日志。
- 先读 docs/API_KEYS_AND_LOCAL_CONFIG.zh-CN.md。

OpenClaw、Hermes 或 crawler-style agent：
- 爬取 https://github.com/kkunkunya/ppt-maker-agent-plugin
- 阅读 docs/AGENT_CRAWLER_GUIDE.zh-CN.md。
- 遵守上面的 API key 策略。

如果不能安装 plugin，则走兜底：
1. 先读 plugins/ppt-maker/skills/ppt-route/SKILL.md。
2. 将请求路由到一个主模式：
   - html-showcase-mode
   - image-asset-mode
   - editable-pptx-mode
   - fixed-template-fill-mode
   - verification
3. 再读取匹配的 sibling SKILL.md，以及 plugins/ppt-maker/_shared/references/ 下的相关规则。

执行策略：
- 模糊 PPT 请求必须先 route。
- PPTX 输出必须声明 editability label。
- 除非用户明确接受 image-based output，否则不能用整页 PNG 满足可编辑 PPTX 请求。
- 学校/公司固定模板必须先检查 placeholders、shape names、bounding boxes、forbidden regions。
- 交付前必须执行或规划 deck verification，并如实报告证据。
```
