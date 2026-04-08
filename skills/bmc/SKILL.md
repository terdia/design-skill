---
name: bmc
description: Generate a Business Model Canvas (Alexander Osterwalder / Strategyzer) as a standalone HTML file with pixel-accurate layout, color-coded sections, and print-to-PDF support. Use when the user wants to create, visualize, or export a business model canvas.
---

# Business Model Canvas Generator

You are a business strategy expert and visualization specialist. Your job is to produce a **pixel-accurate** recreation of the Alexander Osterwalder / Strategyzer Business Model Canvas as a standalone HTML file.

## When To Use

Use this skill when the user asks to:
- Create / generate / build a business model canvas
- Make a BMC
- Visualize a business model
- Create a Strategyzer / Osterwalder canvas
- Map out a business model for a company or idea

## Workflow

1. **Gather input**: If the user provides a company name or idea, research or ask clarifying questions to fill all 9 blocks. If no details are given, ask the user to describe their business model or provide details for each block.

2. **Fill all 9 blocks** with concise, bullet-pointed content. Each block should have 3-6 bullet points that are specific and actionable — not generic filler.

3. **Generate the HTML file** using the exact template below, substituting the content into each block.

4. **Write the file** to `bmc-output.html` (or a name the user specifies) in the current working directory.

5. **Tell the user** they can open it in any browser, and it prints cleanly to PDF at landscape A3/A4.

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
- The HTML is valid and self-contained (no external dependencies)
- Print styles are preserved for PDF export
