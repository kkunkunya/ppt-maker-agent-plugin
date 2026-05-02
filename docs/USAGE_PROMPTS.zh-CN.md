# 使用 Prompt

## 路由一个模糊 PPT 请求

```text
Use ppt-maker:ppt-route.
我需要做 PPT/deck，但输出模式还不确定。
只询问会影响 route 的缺失约束。
然后返回：
- Mode
- Editability label
- Next skill
- Reason
- Forbidden shortcut
```

## 可编辑 PPTX

```text
Use ppt-maker:editable-pptx.
我需要一份对象级可编辑 PowerPoint 文件。
文字、图片、形状、表格、图表尽量保持可编辑。
如果某页或某个元素必须栅格化，标注为 partially editable，并列出例外。
交付前执行或规划 ppt-maker:deck-verification。
```

## 固定模板填充

```text
Use ppt-maker:fixed-template-fill.
模板版式、logo、header、footer 和机构标识都是保护区域。
先检查 placeholders、shape names、bounding boxes、forbidden regions，再填内容。
如果内容放不进允许区域，报告 blocked 或拆分页面。不要移动保护区域。
```

## HTML 展示型 Deck

```text
Use ppt-maker:html-showcase.
这份 deck 用于现场展示、录屏或视频片段。
HTML 可以接受，不要求 PowerPoint 可编辑。
规划 slide rhythm、视觉方向、preview command 和 verification screenshots。
不要声称输出是 editable PPTX。
```

## 图片资产

```text
Use ppt-maker:image-assets.
制作 PPT 视觉资产，比如封面、章节分隔页、概念图、背景图或手绘说明图。
除非用户明确要整页栅格图，否则最终 slide 文本应留在图片外部。
说明比例、安全文字区、prompt、输出路径，以及文字是否 baked in。
```

## 交付前验证

```text
Use ppt-maker:deck-verification.
交付前验证这份 deck。
检查 editability label、slide count、render preview、文字溢出、字体缺失、坏媒体、模板 forbidden regions，以及承诺的输出模式是否真实。
用证据路径返回 pass、pass_with_warnings、partial、blocked 或 failed。
```

