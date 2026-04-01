# Obsidian Excalidraw — Claude Skill

A Claude skill for creating Excalidraw diagrams that open natively in Obsidian. Claude generates `.excalidraw` files directly in your vault — no copy-paste, no import, just open and draw.

---

## What It Does

When active, Claude can produce fully-formed `.excalidraw` files saved to the current working directory. Open them in Obsidian and they render immediately in the Excalidraw plugin.

- **9 diagram types** — flowcharts, sequence diagrams, state machines, mind maps, architecture diagrams, comparisons, causal chains, trees, and freeform sketches
- **Design philosophy built in** — diagrams argue visually, not just label boxes; each concept gets a distinct visual pattern
- **Semantic color palette** — 10 role-based color pairs (start, end, process, decision, data, error, AI, etc.) for consistent, readable diagrams
- **Correct JSON from the start** — proper element bindings, no forbidden fields, arrow connections that hold when you move shapes
- **Large diagram strategy** — section-by-section generation prevents token-limit truncation on complex diagrams
- **Container discipline** — free-floating text by default; shapes only when they carry meaning

### Trigger examples

- *"Draw a flowchart of the user signup flow"*
- *"Create an architecture diagram for my backend services"*
- *"Make a mind map of project ideas"*
- *"Sketch a decision tree for feature prioritization"*
- *"Visualize the states in this order lifecycle"*
- *"Draw a sequence diagram showing the OAuth flow"*
- *"Create a comparison diagram of Option A vs Option B"*

---

## Requirements

- [Obsidian](https://obsidian.md/) with the [Excalidraw plugin](https://github.com/zsviczian/obsidian-excalidraw-plugin) installed and enabled
- A Claude environment that supports skills (Claude Code, or any environment with skill loading)
- Claude Code pointed at your vault directory (so files save into the vault)

---

## Installation

### Method 1 — `.skill` file

Download `obsidian-excalidraw.skill` and install it through your Claude skill manager.

### Method 2 — Claude Code (CLI)

```bash
cp -r /path/to/obsidian-excalidraw-skill ~/.claude/plugins/marketplaces/anthropic-agent-skills/skills/obsidian-excalidraw
```

### Method 3 — Copy the directory

Clone this repo and copy `SKILL.md` and `references/` into a folder named `obsidian-excalidraw` inside your Claude skills directory.

---

## Usage

Open Claude Code with your Obsidian vault as the working directory, then ask Claude to draw something:

```
"Draw a flowchart of the authentication flow"
```

Claude will generate the diagram and save it as `auth-flow.excalidraw` (or a similar descriptive name) directly in your vault. Open it in Obsidian — it renders immediately in Excalidraw view.

---

## File Structure

```
obsidian-excalidraw-skill/
├── SKILL.md                          ← Skill entry point: workflow, diagram types, element rules, checklist
└── references/
    ├── color-palette.md              ← Semantic color pairs for all element roles
    ├── element-templates.md          ← Copy-paste JSON for every element type + complete example
    └── design-patterns.md           ← Visual patterns, multi-zoom architecture, section-by-section strategy
```

`SKILL.md` is always loaded when the skill triggers. The three reference files are loaded on demand — only the relevant one enters context for a given task.

---

## Output Format

Files are plain JSON with a `.excalidraw` extension — the native format the Obsidian Excalidraw plugin opens directly. No markdown wrapper, no frontmatter, no import step.

```json
{
  "type": "excalidraw",
  "version": 2,
  "source": "https://github.com/zsviczian/obsidian-excalidraw-plugin",
  "elements": [ ... ],
  "appState": { "gridSize": null, "viewBackgroundColor": "#ffffff" },
  "files": {}
}
```

---

## Customization

All files are plain Markdown — edit them to match your preferences:

- **`references/color-palette.md`** — swap in your own brand colors or theme palette
- **`references/design-patterns.md`** — add project-specific layout patterns
- **`references/element-templates.md`** — extend with custom element configurations

---

## License

MIT © [darthkamal](https://github.com/darthkamal)
