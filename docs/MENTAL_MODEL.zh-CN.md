# 认知模型

大多数 AI 做 PPT 翻车，不是因为它不会排版，而是因为它把“看起来像 PPT”和“交付某种 PPT 产物”混为一谈。

可以这样向用户和 Agent 解释：

> PPT 生产是一家印刷店，不是一台万能打印机。

前台先问这单是什么。舞台间做现场演示和录屏网页。图片工作室做封面、背景和图解。PowerPoint 柜台做可编辑文件。模板柜台填学校或公司模板。质检柜台检查结果能不能交。

用户不需要理解每个技术后端，但必须知道自己接受的是哪一种承诺。

## 三种常见承诺

### 展示承诺

“这东西要在屏幕上好看。”

适合路线：

- HTML showcase
- raster image deck
- video frames

风险：

- PowerPoint 里不可编辑。

### 可编辑承诺

“别人之后还要改。”

适合路线：

- editable PPTX

风险：

- 某些复杂视觉可能需要作为单独图片资产处理。
- 如果某些页面必须栅格化，必须标注 partially editable。

### 模板安全承诺

“学校/公司模板不能乱动。”

适合路线：

- fixed-template fill

风险：

- Agent 必须先检查 placeholders、logo、header、footer、forbidden regions，再开始填内容。

## 一句话规则

制作之前先输出：

```text
Mode: <html-showcase | image-assets | editable-pptx | fixed-template-fill | verification>
Editability: <not PowerPoint-editable | image-based | partially editable | object-level editable>
Forbidden shortcut: <不能偷换成什么>
```

