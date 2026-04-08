# Business Model Canvas AI Skills Repo

This repo contains structured SKILL.md files that teach AI coding assistants how to generate professional Business Model Canvas (Osterwalder/Strategyzer) visualizations as self-contained HTML files.

## Repo Structure

- `skills/` — Per-canvas-type skill directories
- `SKILL_TREE.md` — Master index of all available skills
- `.claude-plugin/` — Claude Code plugin manifest
- `.cursor-plugin/` — Cursor plugin configuration
- `.agents/plugins/` — Codex plugin configuration

## Skill Format

Skills follow the Agent Skills open standard (agentskills.io):

- **Frontmatter:** YAML with `name` (required) and `description` (required)
- **Body:** Markdown following the gather input -> fill blocks -> generate HTML pattern
- **Code blocks:** Complete, self-contained HTML template with CSS grid layout

## Naming Conventions

- Canvas skills: `bmc` (Business Model Canvas), future: `vpc` (Value Proposition Canvas), `lean` (Lean Canvas)
- All skills live under `skills/{skill-name}/SKILL.md`

## Non-Negotiable Rules

1. **Never generate partial canvases** — all 9 blocks must have content.
2. **HTML must be self-contained** — zero external dependencies (no CDNs, no external CSS/JS).
3. **Never modify the CSS grid layout** — positions match the official Strategyzer template.
4. **Always include print styles** for landscape PDF export.

## Working in This Repo

When adding or modifying skills:

1. Each skill is a standalone directory under `skills/`
2. Update `SKILL_TREE.md` when adding new skills
3. Test that YAML frontmatter parses correctly
4. Ensure all HTML templates are complete and render correctly in a browser
5. Cross-reference related skills where relevant
