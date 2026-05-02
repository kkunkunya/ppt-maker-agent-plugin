# Mental Model

Most bad AI-made PPTs come from one confusion: the agent optimizes for visual appearance while the user needed a specific delivery artifact.

Use this metaphor with users and agents:

> PPT production is a print shop, not a single printer.

The front desk asks what the job is. A stage booth makes browser slides for live talks. An image studio makes covers and diagrams. A PowerPoint desk makes editable files. A template desk fills locked school or company templates. A QA desk checks the result.

The user does not need to know every backend. They need to know which promise they are accepting.

## The Three Common Promises

### Display Promise

"This should look good on screen."

Best routes:

- HTML showcase
- raster image deck
- video frames

Risk:

- Not editable in PowerPoint.

### Editability Promise

"Someone else must revise this later."

Best route:

- editable PPTX

Risk:

- Some high-end visual effects may need to become separate image assets.
- If any slide is rasterized, label the deck as partially editable.

### Template Safety Promise

"The school/company template cannot move."

Best route:

- fixed-template fill

Risk:

- The agent must inspect placeholders, logos, headers, footers, and forbidden regions before editing.

## One Sentence Rule

Before making slides, say:

```text
Mode: <html-showcase | image-assets | editable-pptx | fixed-template-fill | verification>
Editability: <not PowerPoint-editable | image-based | partially editable | object-level editable>
Forbidden shortcut: <what must not be faked>
```

