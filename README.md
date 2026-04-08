# Business Model Canvas for AI

AI skills that teach your coding assistant how to generate professional Business Model Canvas (Osterwalder/Strategyzer) visualizations as self-contained HTML files.

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Skills](https://img.shields.io/badge/skills-1-green.svg)](skills/)

## What is this?

Structured skill files that AI coding assistants read to generate pixel-accurate Business Model Canvas visualizations. Each skill contains the full HTML/CSS template and step-by-step instructions your AI assistant uses to produce a self-contained HTML file you can open in any browser or print to PDF.

Supports Claude Code, Cursor, Codex, and 38+ other AI tools via `npx skills add`.

## Compatibility

This repo is the shared source for Business Model Canvas AI integrations. The `skills/` content is reused across assistants, but each tool reads a different plugin or marketplace format.

| Tool | Skills install | Uses shared `skills/` | Metadata source |
|------|----------------|-----------------------|-----------------|
| npx-compatible tools | `npx skills add terdia/design-skill` | Yes | repo skills layout |
| Claude Code | `/install-plugin https://github.com/terdia/design-skill` | Yes | `.claude-plugin/plugin.json` |
| Cursor | Add `terdia/design-skill` as a plugin source | Yes | `.cursor-plugin/plugin.json` |
| Codex | Load `.agents/plugins/marketplace.json` and install `bmc` | Yes | `.agents/plugins/marketplace.json` |

Short version: one repo, one shared skill set, multiple assistant-specific install paths.

## Quick Start

### npx (works with 38+ AI tools)

```bash
npx skills add terdia/design-skill
```

### Claude Code

```
/install-plugin https://github.com/terdia/design-skill
```

### Cursor

Add `terdia/design-skill` as a plugin source in Cursor settings.

### Codex

Clone this repo and point Codex at `.agents/plugins/marketplace.json`, then install the `bmc` plugin from that local marketplace.

## Usage

After installing, ask your AI assistant:

- "Create a business model canvas for Airbnb"
- "Generate a BMC for my SaaS startup"
- "Build a Strategyzer canvas for [company name]"

In Claude Code you can also use the slash command:
```
/bmc Airbnb
```

Your assistant reads the skill, gathers your business model details, and writes a complete HTML file.

## What You Get

A single self-contained HTML file (`bmc-output.html`) with:

- Pixel-accurate Osterwalder 9-block grid layout
- Color-coded sections (blue = infrastructure, purple = value prop, green = customer, red/amber = financials)
- Icons for each block
- Print-optimized CSS (landscape A3/A4 PDF)
- Zero external dependencies

## Available Skills

| Skill | Directory | Description | Status |
|-------|-----------|-------------|--------|
| Business Model Canvas | `skills/bmc/` | Generate a pixel-accurate Osterwalder/Strategyzer BMC as self-contained HTML | Available |

## How Skills Work

Each skill follows a three-step pattern:

1. **Gather** — collects business model details from the user (or researches a known company)
2. **Generate** — fills all 9 blocks with specific, actionable bullet points and produces the HTML
3. **Verify** — confirms the output has all blocks filled, valid HTML, and working print styles

## Links

- [Strategyzer Business Model Canvas](https://www.strategyzer.com/business-model-canvas)
- [Business Model Generation (book)](https://www.strategyzer.com/books/business-model-generation)

## License

MIT
