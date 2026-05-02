# Deck Verification Gates

Use this before claiming a deck artifact is ready.

## PPTX Structural Checks

- PPTX opens without repair.
- Declared editability label is accurate.
- Slide count matches plan.
- Shapes stay inside slide bounds.
- No generated shape overlaps template forbidden regions.
- Required placeholders remain present.
- Fonts are in the approved or reported fallback list.
- Images meet minimum resolution and max size policy.
- Tables/charts are editable when promised.

## Render Checks

Render at least one preview path:

- PowerPoint export when available for final fidelity.
- LibreOffice headless or another renderer as fallback.
- HTML decks through browser screenshots.

Check rendered pages for:

- text overflow
- clipped images
- covered logos/header/footer
- missing fonts
- unreadable chart labels
- blank or broken media

## Report Status

Use one of:

- `pass`: all required checks passed.
- `pass_with_warnings`: usable, but warnings are listed.
- `partial`: artifact exists but some promised behavior is not verified.
- `blocked`: a required route cannot be completed safely.
- `failed`: generated artifact violates hard constraints.

Do not mark a fixed-template deck as `pass` if no template schema was used.

