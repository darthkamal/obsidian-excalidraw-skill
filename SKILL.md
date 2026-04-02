---
name: obsidian-excalidraw
description: "Create Excalidraw diagrams as .excalidraw files that open directly in the Obsidian Excalidraw plugin. Use when the user asks to: draw a diagram, create a flowchart, visualize an architecture, make a mind map, sketch a concept, create a decision tree, diagram a workflow, draw a system design, visualize relationships, or produce any kind of visual/sketch in Obsidian. Saves the file to the current working directory so it immediately appears in the vault. Triggers on: 'draw', 'diagram', 'excalidraw', 'flowchart', 'visualize', 'sketch', 'mind map', 'architecture diagram', 'system design', 'create a visual'."
---

# Obsidian Excalidraw

Creates `.excalidraw` files (pure JSON) that the Obsidian Excalidraw plugin opens directly. Files save to the current working directory and appear immediately in the vault — no import step required.

## Workflow

1. **Assess depth** — is this a quick conceptual sketch or a detailed technical diagram?
2. **Choose diagram type** — match structure to content (see table below)
3. **Design the diagram** — plan layout before generating JSON; read [design-patterns.md](references/design-patterns.md) for visual patterns and section-by-section strategy for large diagrams
4. **Generate JSON** — pull colors from [color-palette.md](references/color-palette.md); use templates from [element-templates.md](references/element-templates.md)
5. **Save file** — write to `<topic>.excalidraw.md` in the current working directory
6. **Confirm to user** — tell them the file name and to open it in Obsidian

**For large or complex diagrams: build JSON one section at a time.** Do NOT generate the full diagram in a single pass — the output token limit will truncate it and produce broken JSON. See [design-patterns.md](references/design-patterns.md) for the section-by-section workflow.

---

## Diagram Type Selection

| Content Type | Diagram Type | Layout Hint |
|---|---|---|
| Process steps, decisions, workflows | **Flowchart** | Top-down or left-right flow with decision diamonds |
| Actor interactions over time | **Sequence** | Vertical timeline, horizontal actor columns |
| States and transitions | **State machine** | Nodes = states, arrows = transitions with labels |
| Concepts branching from a center | **Mind map** | Radial fan-out from central node |
| System components and their relationships | **Architecture** | Layered sections with arrows between components |
| Before/after or option A vs option B | **Comparison** | Side-by-side subregions |
| Cause → effect chains | **Causal chain** | Left-to-right assembly line |
| Hierarchical structure | **Tree/hierarchy** | Top-down branching with lines, no boxes needed |
| Freeform notes or brainstorm | **Freeform** | No fixed layout, visual grouping by proximity |

---

## Design Philosophy

**Diagrams should argue, not display.** A good diagram shows relationships, causality, and flow that words alone can't express. The shape should BE the meaning.

**Isomorphism test:** If you removed all text, would the structure alone communicate the concept? If not, redesign.

**Education test:** Could someone learn something concrete from this diagram, or does it just label boxes?

**Container discipline:** Not every piece of text needs a box around it. Default to free-floating text; add containers only when the shape carries meaning. Aim for fewer than 30% of text elements inside containers.

**Each major concept uses a different visual pattern.** Avoid uniform card grids. See [design-patterns.md](references/design-patterns.md) for the full pattern library.

---

## File Format

Save as `.excalidraw.md` — the native format for the Obsidian Excalidraw plugin v2.x. Raw `.excalidraw` JSON files open in "compatibility mode" in newer plugin versions.

```markdown
---

excalidraw-plugin: parsed
tags: [excalidraw]

---
==⚠  Switch to EXCALIDRAW VIEW in the MORE OPTIONS menu of this document. ⚠==


# Excalidraw Data

## Text Elements
Element label ^elementId

%%
## Drawing
```json
{"type":"excalidraw","version":2,"source":"https://excalidraw.com","elements":[...],"appState":{"gridSize":null,"viewBackgroundColor":"#ffffff"},"files":{}}
```
%%
```

**Text Elements section**: list each text element as `text content ^elementId` (one per line, newlines in text collapsed to spaces). This section is used for vault search and internal block links — it can be empty but should be populated.

**Drawing section**: the full Excalidraw JSON on a single line between the ` ```json ` fence and `%%` delimiters. The Obsidian Excalidraw plugin opens this file directly in drawing view.

---

## Element Essentials

Use templates from [element-templates.md](references/element-templates.md) for copy-paste JSON. Key rules:

**Required on every element:**
```json
{
  "id": "unique-string-id",
  "type": "rectangle|ellipse|diamond|text|arrow|line",
  "x": 0, "y": 0, "width": 160, "height": 80,
  "angle": 0,
  "strokeColor": "#hex",
  "backgroundColor": "transparent",
  "fillStyle": "solid",
  "strokeWidth": 2,
  "strokeStyle": "solid",
  "roughness": 1,
  "opacity": 100,
  "groupIds": [],
  "seed": 123456,
  "version": 1,
  "isDeleted": false,
  "boundElements": null,
  "updated": 1,
  "link": null,
  "locked": false
}
```

**Forbidden fields** (break excalidraw.com compatibility): `frameId`, `index`, `versionNonce`, `rawText`. Use `boundElements: null` when there are no bindings — never use `[]`. Use `updated: 1` not a timestamp.

**Shapes:**
- `rectangle` — add `"roundness": {"type": 3}` for rounded corners (omitting it gives sharp corners; always include it unless sharp corners are intentional)
- `ellipse` — use for start/end nodes, external actors
- `diamond` — use for decisions and branching
- `line` — structural lines (timelines, tree branches); uses `"points": [[0,0],[x,y]]`
- `arrow` — connections; requires `startBinding` and `endBinding`

**Text defaults:**
```json
{
  "type": "text",
  "fontSize": 20,
  "fontFamily": 5,
  "textAlign": "center",
  "verticalAlign": "middle",
  "containerId": null,
  "originalText": "same as text",
  "autoResize": true,
  "lineHeight": 1.25
}
```

**Font families:** `1` Virgil (hand-drawn) · `2` Helvetica · `3` Cascadia (monospace) · `4` Assistant · `5` Excalifont (default, Obsidian-native)

**Style defaults:** `roughness: 1` (hand-drawn feel) · `roughness: 0` for clean technical diagrams. Always `opacity: 100`.

---

## Text Centering

Independent text elements have no auto-centering — `x` is the left edge, not the center. Calculate manually:

```
estimatedWidth = text.length × fontSize × 0.5   (use × 1.0 for CJK)
x = centerX − estimatedWidth / 2
```

Example: "Hello" (5 chars, fontSize 20) centered at x=400 → width=50 → x=375

---

## Arrow Binding

Bind arrows to shapes on both ends so they stay connected when elements move:

```json
{
  "type": "arrow",
  "startBinding": {"elementId": "source_id", "focus": 0, "gap": 5},
  "endBinding": {"elementId": "target_id", "focus": 0, "gap": 5},
  "startArrowhead": null,
  "endArrowhead": "arrow",
  "points": [[0, 0], [120, 0]]
}
```

Also add to **both** the source and target shape's `boundElements`:
```json
"boundElements": [{"id": "arrow_id", "type": "arrow"}]
```
Both ends must register the arrow or the binding breaks when elements are moved.

Use `"strokeStyle": "dashed"` for optional paths, weak associations, or async flows.

---

## File Naming

| Pattern | Example |
|---------|---------|
| `<topic>.excalidraw.md` | `auth-flow.excalidraw.md` |
| `<topic>.excalidraw.md` | `project-ideas.excalidraw.md` |
| `<topic>.excalidraw.md` | `backend-services.excalidraw.md` |

Save to current working directory. After saving, tell the user:
> "Saved as `<filename>.excalidraw.md`. Open it in Obsidian — it will open directly in Excalidraw view."

---

## Common Mistakes

| Mistake | Fix |
|---------|-----|
| Text element `x` set to center, not left edge | Apply centering formula: `x = centerX − (text.length × fontSize × 0.5) / 2` |
| Elements overlapping | Minimum 20–30 px gap between any two elements |
| Content touching canvas edge | 50–80 px padding on all sides |
| Arrow label too long for short arrow | Keep labels under 3 words, or extend arrow length |
| `boundElements: []` | Must be `null`, not empty array |
| Text color too light on white background | Never use colors lighter than `#757575` on white |
| Font size below 14 px | Minimum 14 px; body text minimum 16 px |
| Generating entire complex diagram in one pass | Build section by section — see design-patterns.md |

---

## Quality Checklist

Before saving the file:

- [ ] JSON is valid (no trailing commas, all brackets closed)
- [ ] All IDs are unique strings
- [ ] No `frameId`, `index`, `versionNonce`, or `rawText` fields
- [ ] `boundElements` is `null`, not `[]` (unless element has actual bindings)
- [ ] `updated` is `1`, not a timestamp
- [ ] All text elements have `originalText` matching `text`
- [ ] Arrow bindings reference IDs that actually exist
- [ ] No element extends beyond canvas padding (50 px from edges)
- [ ] No two elements overlap (20 px minimum gap)
- [ ] Font size: titles 20–28 px, body 16–20 px, minimum 14 px
- [ ] All colors from [color-palette.md](references/color-palette.md) — no invented colors
- [ ] No emoji in text — use color coding instead
- [ ] Diagram argues a relationship, not just labels boxes
- [ ] File is saved as `.excalidraw.md` with correct frontmatter (`excalidraw-plugin: parsed`), `## Text Elements` section, and JSON inside ` ```json ` / `%%` delimiters
