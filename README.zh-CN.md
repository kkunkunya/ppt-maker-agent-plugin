# PPT Maker Agent Plugin

[English](README.md) | [简体中文](README.zh-CN.md)

面向 Claude Code、Codex 和其他 Coding Agent 的项目级 PPT 生产路由插件。

很多 Agent 做 PPT 会翻车，不是因为不会写页面，而是因为它把所有 “PPT” 都当成同一种产物。这个插件让 Agent 先问最关键的问题：**这次到底要交付哪一种演示文稿？**

## 认知比喻

把 PPT 生产想成一家小型印刷店，里面有不同柜台：

| 柜台 | 负责什么 | Plugin skill |
|---|---|---|
| 前台 | 判断这单该去哪个柜台 | `ppt-maker:ppt-route` |
| 舞台间 | 做录屏、直播、演讲用的网页演示 | `ppt-maker:html-showcase` |
| 图片工作室 | 做封面、背景、概念图、手绘说明图 | `ppt-maker:image-assets` |
| PowerPoint 柜台 | 做对象级可编辑 `.pptx` | `ppt-maker:editable-pptx` |
| 模板柜台 | 填学校/公司/答辩模板，logo 和版式不能乱动 | `ppt-maker:fixed-template-fill` |
| 质检柜台 | 交付前检查可编辑性、渲染、模板安全和证据 | `ppt-maker:deck-verification` |

核心区别是“能不能编辑”。整页 PNG 放进 PowerPoint，就像一张贴在玻璃后的海报：可以很好看，但用户改不了里面的文字和对象。真正可编辑的 PPTX 更像积木：文本框、形状、表格、图表、图片都还是独立零件。

## 它是什么

`ppt-maker` 是一个 skill-only plugin，用来做 PPT 任务的路由和边界约束。它适合让 Agent 在以下交付物之间做正确选择：

- HTML 展示型 deck
- PPT 用图片资产
- 栅格图/图片型 deck
- 对象级可编辑 PPTX
- 固定模板 PPTX 填充
- 交付前验证报告

它刻意设计为 **项目级启用**。Marketplace 可以注册一次，但 plugin 不应该默认进每个 Agent 会话；只有当前项目确实要做 PPT 时再启用。

## 安装

### Claude Code

```bash
claude plugin marketplace add kkunkunya/ppt-maker-agent-plugin
cd /path/to/your-presentation-project
claude plugin install ppt-maker@ppt-maker-agent-plugin --scope project
```

如果你只想在本机当前 checkout 使用，可以把 `--scope project` 换成 `--scope local`。

### Codex

```bash
codex plugin marketplace add kkunkunya/ppt-maker-agent-plugin
codex -C /path/to/your-presentation-project \
  -c 'plugins."ppt-maker@ppt-maker-agent-plugin".enabled=true'
```

第一条命令只是注册 marketplace。第二条命令是在指定项目会话里启用 `ppt-maker`。

### 其他 Agent

如果你的 Agent 不支持 Claude/Codex plugin manifest，可以复制 [docs/AGENT_INSTALL_PROMPT.zh-CN.md](docs/AGENT_INSTALL_PROMPT.zh-CN.md) 里的 prompt。兜底方式很简单：先让 Agent 读 `plugins/ppt-maker/skills/ppt-route/SKILL.md`，再按路由结果读取对应 sibling skill。

## 常见用法

让 Agent 先路由：

```text
Use ppt-maker. 我需要根据这些材料做一份 12 页答辩 PPT。
学校模板必须保持不变，logo/header/footer 不能移动。
先 route，再给安全填充方案；除非模板 schema 已清楚，否则不要直接改模板。
```

做录屏展示 deck：

```text
Use ppt-maker. 我需要一份 6 分钟视频片段用的网页演示。
HTML 可以接受，不要求 PowerPoint 可编辑。
先 route，再规划 html-showcase deck 和需要的图片资产。
```

做客户可编辑交付：

```text
Use ppt-maker. 我需要交付一份客户后续能修改的可编辑 PPTX。
文字保持文本框，图表/表格尽量保持可编辑；交付前跑 deck verification。
```

## 仓库结构

```text
plugins/ppt-maker/                 # plugin 源码
plugins/ppt-maker/skills/          # 六个路由/模式/验证 skill
plugins/ppt-maker/_shared/         # 模式、模板、验证规则
.claude-plugin/marketplace.json    # Claude marketplace manifest
.agents/plugins/marketplace.json   # Codex marketplace manifest
docs/                              # 安装 prompt 与认知模型文档
```

## 边界

- 不把 HTML deck 伪装成可编辑 PPTX。
- 不把整页 PNG 型 PPTX 说成可编辑 PPTX。
- 固定模板任务必须先检查模板结构和安全区域。
- 验证结果必须如实报告 `pass`、`pass_with_warnings`、`partial`、`blocked` 或 `failed`。
- v0.1.0 还没有确定性 PPTX 生成后端。当前版本提供的是路由、边界、检查清单和 Agent 交付契约。

## License

MIT

