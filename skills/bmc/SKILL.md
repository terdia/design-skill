---
name: bmc
description: Generate a Business Model Canvas (Alexander Osterwalder / Strategyzer) as HTML or PowerPoint (.pptx) with pixel-accurate layout, color-coded sections, and print-to-PDF support. Use when the user wants to create, visualize, or export a business model canvas.
---

# Business Model Canvas Generator

You are a business strategy expert and visualization specialist. Your job is to produce a **pixel-accurate** recreation of the Alexander Osterwalder / Strategyzer Business Model Canvas.

## Supported Output Formats

| Format | Output | How |
|--------|--------|-----|
| **HTML** (default) | `bmc-output.html` | Self-contained HTML file, open in browser or print to PDF |
| **PowerPoint** | `bmc-output.pptx` | Generated via Python script using `python-pptx` |

If the user asks for PowerPoint / pptx / slides, use the PowerPoint template. Otherwise default to HTML.

## When To Use

Use this skill when the user asks to:
- Create / generate / build a business model canvas
- Make a BMC
- Visualize a business model
- Create a Strategyzer / Osterwalder canvas
- Map out a business model for a company or idea
- Export a business model as PowerPoint / pptx / slides

## Workflow

1. **Gather input**: If the user provides a company name or idea, research or ask clarifying questions to fill all 9 blocks. If no details are given, ask the user to describe their business model or provide details for each block.

2. **Fill all 9 blocks** with concise, bullet-pointed content. Each block should have 3-6 bullet points that are specific and actionable — not generic filler.

3. **Determine output format**: Use PowerPoint if the user mentions pptx/powerpoint/slides, otherwise default to HTML.

4. **Generate the file** using the appropriate template below, substituting the content into each block.

5. **Write the file(s)** to the current working directory. For PowerPoint, write the Python script and run it.

6. **Tell the user** where the output file is and how to open it.

---

## The 9 Building Blocks

| # | Block | Key Question |
|---|-------|-------------|
| 1 | Key Partners | Who are our key partners and suppliers? What resources/activities do they provide? |
| 2 | Key Activities | What key activities does our value proposition require? |
| 3 | Key Resources | What key resources does our value proposition require? |
| 4 | Value Propositions | What value do we deliver? Which customer problems do we solve? |
| 5 | Customer Relationships | What type of relationship does each segment expect? |
| 6 | Channels | How do we reach our customer segments? |
| 7 | Customer Segments | Who are our most important customers? |
| 8 | Cost Structure | What are the most important costs in our business model? |
| 9 | Revenue Streams | For what value are customers willing to pay? |

---

## HTML Template

Generate a **single, self-contained HTML file** (no external dependencies) using this structure. Replace the placeholder bullet points with real content.

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Business Model Canvas — COMPANY_NAME</title>
<style>
  /* ========== RESET & BASE ========== */
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
    background: #f0f2f5;
    padding: 24px;
    color: #1a1a2e;
  }

  /* ========== CANVAS WRAPPER ========== */
  .canvas-wrapper {
    max-width: 1400px;
    margin: 0 auto;
  }

  .canvas-title {
    text-align: center;
    font-size: 28px;
    font-weight: 700;
    margin-bottom: 8px;
    color: #1a1a2e;
    letter-spacing: -0.5px;
  }

  .canvas-subtitle {
    text-align: center;
    font-size: 14px;
    color: #6b7280;
    margin-bottom: 24px;
  }

  /* ========== GRID LAYOUT ========== */
  .canvas {
    display: grid;
    grid-template-columns: repeat(10, 1fr);
    grid-template-rows: repeat(6, 1fr);
    gap: 0;
    border: 2px solid #374151;
    border-radius: 12px;
    overflow: hidden;
    background: #ffffff;
    aspect-ratio: 5 / 3;
    min-height: 600px;
  }

  /* ========== BLOCK BASE ========== */
  .block {
    padding: 16px 14px;
    border: 1px solid #e5e7eb;
    display: flex;
    flex-direction: column;
    overflow: hidden;
  }

  .block-header {
    display: flex;
    align-items: center;
    gap: 8px;
    margin-bottom: 10px;
    flex-shrink: 0;
  }

  .block-icon {
    width: 28px;
    height: 28px;
    border-radius: 8px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 14px;
    flex-shrink: 0;
  }

  .block-label {
    font-size: 11px;
    font-weight: 700;
    text-transform: uppercase;
    letter-spacing: 0.8px;
    color: #374151;
  }

  .block-content {
    flex: 1;
    overflow-y: auto;
  }

  .block-content ul {
    list-style: none;
    padding: 0;
  }

  .block-content li {
    font-size: 12px;
    line-height: 1.5;
    padding: 4px 0;
    padding-left: 14px;
    position: relative;
    color: #4b5563;
  }

  .block-content li::before {
    content: "";
    position: absolute;
    left: 0;
    top: 10px;
    width: 6px;
    height: 6px;
    border-radius: 50%;
  }

  /* ========== GRID POSITIONS (Osterwalder Layout) ========== */
  .block--kp  { grid-column: 1 / 3;   grid-row: 1 / 5; }
  .block--ka  { grid-column: 3 / 5;   grid-row: 1 / 3; }
  .block--kr  { grid-column: 3 / 5;   grid-row: 3 / 5; }
  .block--vp  { grid-column: 5 / 7;   grid-row: 1 / 5; }
  .block--cr  { grid-column: 7 / 9;   grid-row: 1 / 3; }
  .block--ch  { grid-column: 7 / 9;   grid-row: 3 / 5; }
  .block--cs  { grid-column: 9 / 11;  grid-row: 1 / 5; }
  .block--cost { grid-column: 1 / 6;  grid-row: 5 / 7; }
  .block--rev  { grid-column: 6 / 11; grid-row: 5 / 7; }

  /* ========== COLOR CODING ========== */
  /* Infrastructure (left) — Blue tones */
  .block--kp .block-icon  { background: #dbeafe; color: #2563eb; }
  .block--ka .block-icon  { background: #dbeafe; color: #2563eb; }
  .block--kr .block-icon  { background: #dbeafe; color: #2563eb; }
  .block--kp li::before   { background: #93c5fd; }
  .block--ka li::before   { background: #93c5fd; }
  .block--kr li::before   { background: #93c5fd; }

  /* Offering (center) — Purple */
  .block--vp .block-icon  { background: #ede9fe; color: #7c3aed; }
  .block--vp li::before   { background: #c4b5fd; }

  /* Customer (right) — Green tones */
  .block--cr .block-icon  { background: #d1fae5; color: #059669; }
  .block--ch .block-icon  { background: #d1fae5; color: #059669; }
  .block--cs .block-icon  { background: #d1fae5; color: #059669; }
  .block--cr li::before   { background: #6ee7b7; }
  .block--ch li::before   { background: #6ee7b7; }
  .block--cs li::before   { background: #6ee7b7; }

  /* Financials (bottom) */
  .block--cost .block-icon { background: #fee2e2; color: #dc2626; }
  .block--rev .block-icon  { background: #fef3c7; color: #d97706; }
  .block--cost li::before  { background: #fca5a5; }
  .block--rev li::before   { background: #fcd34d; }

  /* ========== FOOTER ========== */
  .canvas-footer {
    text-align: center;
    margin-top: 16px;
    font-size: 11px;
    color: #9ca3af;
  }

  /* ========== PRINT ========== */
  @media print {
    body { background: #fff; padding: 0; }
    .canvas { border-radius: 0; min-height: auto; }
    .canvas-wrapper { max-width: 100%; }
    @page { size: landscape; margin: 1cm; }
  }
</style>
</head>
<body>

<div class="canvas-wrapper">
  <div class="canvas-title">COMPANY_NAME</div>
  <div class="canvas-subtitle">Business Model Canvas</div>

  <div class="canvas">

    <!-- KEY PARTNERS -->
    <div class="block block--kp">
      <div class="block-header">
        <div class="block-icon">&#129309;</div>
        <div class="block-label">Key Partners</div>
      </div>
      <div class="block-content">
        <ul>
          <li>Partner item 1</li>
          <li>Partner item 2</li>
          <li>Partner item 3</li>
        </ul>
      </div>
    </div>

    <!-- KEY ACTIVITIES -->
    <div class="block block--ka">
      <div class="block-header">
        <div class="block-icon">&#9881;</div>
        <div class="block-label">Key Activities</div>
      </div>
      <div class="block-content">
        <ul>
          <li>Activity item 1</li>
          <li>Activity item 2</li>
          <li>Activity item 3</li>
        </ul>
      </div>
    </div>

    <!-- KEY RESOURCES -->
    <div class="block block--kr">
      <div class="block-header">
        <div class="block-icon">&#128273;</div>
        <div class="block-label">Key Resources</div>
      </div>
      <div class="block-content">
        <ul>
          <li>Resource item 1</li>
          <li>Resource item 2</li>
          <li>Resource item 3</li>
        </ul>
      </div>
    </div>

    <!-- VALUE PROPOSITIONS -->
    <div class="block block--vp">
      <div class="block-header">
        <div class="block-icon">&#127873;</div>
        <div class="block-label">Value Propositions</div>
      </div>
      <div class="block-content">
        <ul>
          <li>Value prop item 1</li>
          <li>Value prop item 2</li>
          <li>Value prop item 3</li>
        </ul>
      </div>
    </div>

    <!-- CUSTOMER RELATIONSHIPS -->
    <div class="block block--cr">
      <div class="block-header">
        <div class="block-icon">&#10084;</div>
        <div class="block-label">Customer Relationships</div>
      </div>
      <div class="block-content">
        <ul>
          <li>Relationship item 1</li>
          <li>Relationship item 2</li>
          <li>Relationship item 3</li>
        </ul>
      </div>
    </div>

    <!-- CHANNELS -->
    <div class="block block--ch">
      <div class="block-header">
        <div class="block-icon">&#128666;</div>
        <div class="block-label">Channels</div>
      </div>
      <div class="block-content">
        <ul>
          <li>Channel item 1</li>
          <li>Channel item 2</li>
          <li>Channel item 3</li>
        </ul>
      </div>
    </div>

    <!-- CUSTOMER SEGMENTS -->
    <div class="block block--cs">
      <div class="block-header">
        <div class="block-icon">&#128101;</div>
        <div class="block-label">Customer Segments</div>
      </div>
      <div class="block-content">
        <ul>
          <li>Segment item 1</li>
          <li>Segment item 2</li>
          <li>Segment item 3</li>
        </ul>
      </div>
    </div>

    <!-- COST STRUCTURE -->
    <div class="block block--cost">
      <div class="block-header">
        <div class="block-icon">&#128176;</div>
        <div class="block-label">Cost Structure</div>
      </div>
      <div class="block-content">
        <ul>
          <li>Cost item 1</li>
          <li>Cost item 2</li>
          <li>Cost item 3</li>
        </ul>
      </div>
    </div>

    <!-- REVENUE STREAMS -->
    <div class="block block--rev">
      <div class="block-header">
        <div class="block-icon">&#128178;</div>
        <div class="block-label">Revenue Streams</div>
      </div>
      <div class="block-content">
        <ul>
          <li>Revenue item 1</li>
          <li>Revenue item 2</li>
          <li>Revenue item 3</li>
        </ul>
      </div>
    </div>

  </div>

  <div class="canvas-footer">
    Business Model Canvas template based on Strategyzer AG &mdash; strategyzer.com
  </div>
</div>

</body>
</html>
```

---

## Instructions for Generating

When generating the canvas:

1. **Replace `COMPANY_NAME`** with the actual company or project name (in both the `<title>` and `.canvas-title`).

2. **Replace every placeholder `<li>` item** with real, specific bullet points. Each bullet should be concise (under 15 words). Use 3-6 bullets per block.

3. **Do NOT change the CSS grid layout, colors, class names, or structure.** The layout precisely matches the Osterwalder/Strategyzer template.

4. **Write the complete HTML file** to disk. Default filename: `bmc-output.html` (or let the user choose).

5. **If the user provides partial information**, fill what you can and mark unknowns with `[To be defined]` so they can iterate.

6. **For multiple business models or comparisons**, generate separate HTML files (e.g., `bmc-model-a.html`, `bmc-model-b.html`).

## Non-Negotiable Rules

1. **All 9 blocks must have content** — never leave a block empty.
2. **Bullet points must be specific** to the business, not generic filler.
3. **The HTML must be self-contained** — zero external dependencies.
4. **Print styles must be preserved** for landscape PDF export.
5. **Never modify the CSS grid layout** — the positions match the official Strategyzer template exactly.

## Quality Checklist

Before writing the file, verify:
- All 9 blocks have content (no empty blocks)
- Bullet points are specific to the business, not generic
- Company name appears in title and heading
- For HTML: valid and self-contained (no external dependencies), print styles preserved
- For PowerPoint: script runs without errors, .pptx opens in PowerPoint/Google Slides/Keynote

---

## PowerPoint Template

When the user requests PowerPoint / pptx / slides output, generate a Python script that uses `python-pptx` to create the canvas. Write the script to `generate_bmc.py`, then run it.

**First, ensure python-pptx is installed:**

```bash
pip install python-pptx
```

**Then generate and run this script** (replacing COMPANY_NAME and all placeholder bullets with real content):

```python
from pptx import Presentation
from pptx.util import Inches, Pt, Emu
from pptx.dml.color import RGBColor
from pptx.enum.text import PP_ALIGN, MSO_ANCHOR

prs = Presentation()
prs.slide_width = Inches(16)
prs.slide_height = Inches(9)

slide = prs.slides.add_slide(prs.slide_layouts[6])  # Blank layout

# ========== COLORS ==========
COLORS = {
    "infrastructure": {"bg": RGBColor(0xDB, 0xEA, 0xFE), "icon_bg": RGBColor(0x25, 0x63, 0xEB), "bullet": RGBColor(0x93, 0xC5, 0xFD)},
    "offering":       {"bg": RGBColor(0xED, 0xE9, 0xFE), "icon_bg": RGBColor(0x7C, 0x3A, 0xED), "bullet": RGBColor(0xC4, 0xB5, 0xFD)},
    "customer":       {"bg": RGBColor(0xD1, 0xFA, 0xE5), "icon_bg": RGBColor(0x05, 0x96, 0x69), "bullet": RGBColor(0x6E, 0xE7, 0xB7)},
    "cost":           {"bg": RGBColor(0xFE, 0xE2, 0xE2), "icon_bg": RGBColor(0xDC, 0x26, 0x26), "bullet": RGBColor(0xFC, 0xA5, 0xA5)},
    "revenue":        {"bg": RGBColor(0xFE, 0xF3, 0xC7), "icon_bg": RGBColor(0xD9, 0x77, 0x06), "bullet": RGBColor(0xFC, 0xD3, 0x4D)},
}
WHITE = RGBColor(0xFF, 0xFF, 0xFF)
DARK = RGBColor(0x1A, 0x1A, 0x2E)
GRAY = RGBColor(0x4B, 0x55, 0x63)
BORDER = RGBColor(0xE5, 0xE7, 0xEB)

# ========== LAYOUT GRID ==========
# Canvas area: leave margins for title
MARGIN_LEFT = Inches(0.5)
MARGIN_TOP = Inches(1.2)
CANVAS_W = Inches(15.0)
CANVAS_H = Inches(7.3)

# 10 columns, 6 rows
COL_W = CANVAS_W / 10
ROW_H = CANVAS_H / 6

# Block positions: (col_start, row_start, col_span, row_span, color_key)
BLOCKS = {
    "Key Partners":            (0, 0, 2, 4, "infrastructure"),
    "Key Activities":          (2, 0, 2, 2, "infrastructure"),
    "Key Resources":           (2, 2, 2, 2, "infrastructure"),
    "Value Propositions":      (4, 0, 2, 4, "offering"),
    "Customer Relationships":  (6, 0, 2, 2, "customer"),
    "Channels":                (6, 2, 2, 2, "customer"),
    "Customer Segments":       (8, 0, 2, 4, "customer"),
    "Cost Structure":          (0, 4, 5, 2, "cost"),
    "Revenue Streams":         (5, 4, 5, 2, "revenue"),
}

# ========== CONTENT — REPLACE THESE ==========
CONTENT = {
    "Key Partners": [
        "Partner item 1",
        "Partner item 2",
        "Partner item 3",
    ],
    "Key Activities": [
        "Activity item 1",
        "Activity item 2",
        "Activity item 3",
    ],
    "Key Resources": [
        "Resource item 1",
        "Resource item 2",
        "Resource item 3",
    ],
    "Value Propositions": [
        "Value prop item 1",
        "Value prop item 2",
        "Value prop item 3",
    ],
    "Customer Relationships": [
        "Relationship item 1",
        "Relationship item 2",
        "Relationship item 3",
    ],
    "Channels": [
        "Channel item 1",
        "Channel item 2",
        "Channel item 3",
    ],
    "Customer Segments": [
        "Segment item 1",
        "Segment item 2",
        "Segment item 3",
    ],
    "Cost Structure": [
        "Cost item 1",
        "Cost item 2",
        "Cost item 3",
    ],
    "Revenue Streams": [
        "Revenue item 1",
        "Revenue item 2",
        "Revenue item 3",
    ],
}

# ========== TITLE ==========
txBox = slide.shapes.add_textbox(MARGIN_LEFT, Inches(0.3), CANVAS_W, Inches(0.5))
tf = txBox.text_frame
tf.word_wrap = True
p = tf.paragraphs[0]
p.text = "COMPANY_NAME"
p.font.size = Pt(28)
p.font.bold = True
p.font.color.rgb = DARK
p.alignment = PP_ALIGN.CENTER

txBox2 = slide.shapes.add_textbox(MARGIN_LEFT, Inches(0.75), CANVAS_W, Inches(0.3))
tf2 = txBox2.text_frame
p2 = tf2.paragraphs[0]
p2.text = "Business Model Canvas"
p2.font.size = Pt(14)
p2.font.color.rgb = RGBColor(0x6B, 0x72, 0x80)
p2.alignment = PP_ALIGN.CENTER


def add_block(name, col, row, col_span, row_span, color_key, items):
    """Add a single BMC block as a shape with text."""
    left = MARGIN_LEFT + int(col * COL_W)
    top = MARGIN_TOP + int(row * ROW_H)
    width = int(col_span * COL_W)
    height = int(row_span * ROW_H)

    colors = COLORS[color_key]

    # Background rectangle
    shape = slide.shapes.add_shape(1, left, top, width, height)  # 1 = rectangle
    shape.fill.solid()
    shape.fill.fore_color.rgb = WHITE
    shape.line.color.rgb = BORDER
    shape.line.width = Pt(1)

    # Color accent bar at top
    accent = slide.shapes.add_shape(1, left, top, width, Inches(0.06))
    accent.fill.solid()
    accent.fill.fore_color.rgb = colors["icon_bg"]
    accent.line.fill.background()

    # Text frame
    txBox = slide.shapes.add_textbox(
        left + Inches(0.15),
        top + Inches(0.15),
        width - Inches(0.3),
        height - Inches(0.3),
    )
    tf = txBox.text_frame
    tf.word_wrap = True

    # Block label
    p = tf.paragraphs[0]
    p.text = name.upper()
    p.font.size = Pt(8)
    p.font.bold = True
    p.font.color.rgb = RGBColor(0x37, 0x41, 0x51)
    p.space_after = Pt(6)

    # Bullet items
    for item in items:
        p = tf.add_paragraph()
        p.text = f"  {item}"
        p.font.size = Pt(9)
        p.font.color.rgb = GRAY
        p.space_before = Pt(2)
        p.space_after = Pt(2)
        p.level = 0


# ========== BUILD BLOCKS ==========
for name, (col, row, col_span, row_span, color_key) in BLOCKS.items():
    add_block(name, col, row, col_span, row_span, color_key, CONTENT[name])

# ========== FOOTER ==========
footer = slide.shapes.add_textbox(MARGIN_LEFT, Inches(8.6), CANVAS_W, Inches(0.3))
ft = footer.text_frame
fp = ft.paragraphs[0]
fp.text = "Business Model Canvas template based on Strategyzer AG - strategyzer.com"
fp.font.size = Pt(8)
fp.font.color.rgb = RGBColor(0x9C, 0xA3, 0xAF)
fp.alignment = PP_ALIGN.CENTER

# ========== SAVE ==========
prs.save("bmc-output.pptx")
print("Created bmc-output.pptx")
```

### PowerPoint Generation Instructions

When generating PowerPoint output:

1. **Replace `COMPANY_NAME`** in the title with the actual company/project name.

2. **Replace all items in the `CONTENT` dictionary** with real, specific bullet points for the business.

3. **Write the script** to `generate_bmc.py` in the current working directory.

4. **Run `pip install python-pptx`** if not already installed, then **run the script** with `python generate_bmc.py`.

5. **Tell the user** the file is at `bmc-output.pptx` and can be opened in PowerPoint, Google Slides, or Keynote.

6. **Do NOT modify the layout constants, color scheme, or block positions** — they match the Osterwalder/Strategyzer grid.

7. **If generating both formats**, produce both `bmc-output.html` and `bmc-output.pptx`.
