# Fixed Template Schema Reference

Use a template schema before modifying any fixed `.pptx` or `.potx` template.

## Required Fields

```yaml
template_id: school-defense-v1
source_file: template.pptx
slide_size:
  width_in: 13.333
  height_in: 7.5
font_manifest:
  zh: "Microsoft YaHei"
  en: "Times New Roman"
layouts:
  content:
    layout_index: 2
    placeholders:
      title:
        idx: 0
        type: title
        max_chars: 48
      body:
        idx: 1
        type: body
        max_chars: 500
    free_zones:
      - id: main_image
        bbox: { x: 6.8, y: 1.4, w: 5.5, h: 4.6 }
        content_types: [image]
    forbidden_regions:
      - id: logo
        bbox: { x: 11.7, y: 0.1, w: 1.3, h: 0.6 }
text_style_constraints:
  min_body_pt: 18
  max_title_pt: 36
image_policy:
  fit: contain
  no_upscale_over: 1.5
allow_new_shapes: false
```

## Safety Rules

- Prefer filling existing placeholders.
- Add new shapes only when `allow_new_shapes: true` or a `free_zone` explicitly allows it.
- Never write into `forbidden_regions`.
- Never modify slide masters or layouts in MVP mode.
- Treat logo, header, footer, page number, and institutional marks as forbidden unless schema says otherwise.
- If content does not fit the allowed box, shrink within constraints, split the slide, or report `blocked`.

## Inspection Evidence

Template inspection should record:

- slide size
- slide masters and layouts
- placeholder idx/type/name
- shape names and bounding boxes
- likely forbidden regions
- theme fonts and colors
- embedded media list
- unsupported or risky objects such as animation, video, SmartArt, and complex charts

