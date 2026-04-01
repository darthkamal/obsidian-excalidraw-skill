# Element Templates

Copy-paste JSON for each element type. Replace `"#hex"` with colors from `color-palette.md` based on semantic purpose. All templates use Obsidian Excalidraw defaults: `fontFamily: 5`, `roughness: 1`.

The full file is plain JSON written to a `.excalidraw` file — no markdown wrapper needed.

---

## Free-Floating Text (no container)

Use for titles, section labels, annotations, and descriptions. Default to this — add a container only if the shape carries meaning.

```json
{
  "type": "text",
  "id": "title_1",
  "x": 100, "y": 60,
  "width": 300, "height": 35,
  "angle": 0,
  "strokeColor": "#1e40af",
  "backgroundColor": "transparent",
  "fillStyle": "solid",
  "strokeWidth": 1,
  "strokeStyle": "solid",
  "roughness": 1,
  "opacity": 100,
  "groupIds": [],
  "seed": 11111,
  "version": 1,
  "isDeleted": false,
  "boundElements": null,
  "updated": 1,
  "link": null,
  "locked": false,
  "text": "Section Title",
  "originalText": "Section Title",
  "fontSize": 24,
  "fontFamily": 5,
  "textAlign": "left",
  "verticalAlign": "top",
  "containerId": null,
  "lineHeight": 1.25,
  "autoResize": true
}
```

Adjust `strokeColor` for hierarchy: `#1e40af` title · `#3b82f6` subtitle · `#374151` body.

---

## Rectangle (process / action / component)

```json
{
  "type": "rectangle",
  "id": "rect_1",
  "x": 100, "y": 100,
  "width": 180, "height": 80,
  "angle": 0,
  "strokeColor": "#5f3dc4",
  "backgroundColor": "#e5dbff",
  "fillStyle": "solid",
  "strokeWidth": 2,
  "strokeStyle": "solid",
  "roughness": 1,
  "opacity": 100,
  "groupIds": [],
  "roundness": {"type": 3},
  "seed": 22222,
  "version": 1,
  "isDeleted": false,
  "boundElements": [{"id": "text_rect_1", "type": "text"}],
  "updated": 1,
  "link": null,
  "locked": false
}
```

Paired text (set `containerId` to the rectangle's `id`):

```json
{
  "type": "text",
  "id": "text_rect_1",
  "x": 110, "y": 128,
  "width": 160, "height": 25,
  "angle": 0,
  "strokeColor": "#374151",
  "backgroundColor": "transparent",
  "fillStyle": "solid",
  "strokeWidth": 1,
  "strokeStyle": "solid",
  "roughness": 1,
  "opacity": 100,
  "groupIds": [],
  "seed": 22223,
  "version": 1,
  "isDeleted": false,
  "boundElements": null,
  "updated": 1,
  "link": null,
  "locked": false,
  "text": "Process Step",
  "originalText": "Process Step",
  "fontSize": 16,
  "fontFamily": 5,
  "textAlign": "center",
  "verticalAlign": "middle",
  "containerId": "rect_1",
  "lineHeight": 1.25,
  "autoResize": true
}
```

---

## Ellipse (start / end / external actor)

Shape and paired text — always include both:

```json
{
  "type": "ellipse",
  "id": "ellipse_1",
  "x": 100, "y": 100,
  "width": 160, "height": 80,
  "angle": 0,
  "strokeColor": "#2f9e44",
  "backgroundColor": "#d3f9d8",
  "fillStyle": "solid",
  "strokeWidth": 2,
  "strokeStyle": "solid",
  "roughness": 1,
  "opacity": 100,
  "groupIds": [],
  "seed": 33333,
  "version": 1,
  "isDeleted": false,
  "boundElements": [{"id": "text_ellipse_1", "type": "text"}],
  "updated": 1,
  "link": null,
  "locked": false
}
```

```json
{
  "type": "text",
  "id": "text_ellipse_1",
  "x": 120, "y": 128,
  "width": 120, "height": 25,
  "angle": 0,
  "strokeColor": "#1a5c28",
  "backgroundColor": "transparent",
  "fillStyle": "solid",
  "strokeWidth": 1,
  "strokeStyle": "solid",
  "roughness": 1,
  "opacity": 100,
  "groupIds": [],
  "seed": 33334,
  "version": 1,
  "isDeleted": false,
  "boundElements": null,
  "updated": 1,
  "link": null,
  "locked": false,
  "text": "Start",
  "originalText": "Start",
  "fontSize": 16,
  "fontFamily": 5,
  "textAlign": "center",
  "verticalAlign": "middle",
  "containerId": "ellipse_1",
  "lineHeight": 1.25,
  "autoResize": true
}
```

---

## Diamond (decision / branch)

Shape and paired text — always include both:

```json
{
  "type": "diamond",
  "id": "diamond_1",
  "x": 100, "y": 100,
  "width": 180, "height": 100,
  "angle": 0,
  "strokeColor": "#e67700",
  "backgroundColor": "#fff4e6",
  "fillStyle": "solid",
  "strokeWidth": 2,
  "strokeStyle": "solid",
  "roughness": 1,
  "opacity": 100,
  "groupIds": [],
  "seed": 44444,
  "version": 1,
  "isDeleted": false,
  "boundElements": [{"id": "text_diamond_1", "type": "text"}],
  "updated": 1,
  "link": null,
  "locked": false
}
```

```json
{
  "type": "text",
  "id": "text_diamond_1",
  "x": 120, "y": 138,
  "width": 140, "height": 25,
  "angle": 0,
  "strokeColor": "#7c4a00",
  "backgroundColor": "transparent",
  "fillStyle": "solid",
  "strokeWidth": 1,
  "strokeStyle": "solid",
  "roughness": 1,
  "opacity": 100,
  "groupIds": [],
  "seed": 44445,
  "version": 1,
  "isDeleted": false,
  "boundElements": null,
  "updated": 1,
  "link": null,
  "locked": false,
  "text": "Decision?",
  "originalText": "Decision?",
  "fontSize": 16,
  "fontFamily": 5,
  "textAlign": "center",
  "verticalAlign": "middle",
  "containerId": "diamond_1",
  "lineHeight": 1.25,
  "autoResize": true
}
```

---

## Arrow (connection between shapes)

```json
{
  "type": "arrow",
  "id": "arrow_1",
  "x": 280, "y": 140,
  "width": 120, "height": 0,
  "angle": 0,
  "strokeColor": "#5f3dc4",
  "backgroundColor": "transparent",
  "fillStyle": "solid",
  "strokeWidth": 2,
  "strokeStyle": "solid",
  "roughness": 1,
  "opacity": 100,
  "groupIds": [],
  "seed": 55555,
  "version": 1,
  "isDeleted": false,
  "boundElements": null,
  "updated": 1,
  "link": null,
  "locked": false,
  "points": [[0, 0], [120, 0]],
  "startBinding": {"elementId": "source_id", "focus": 0, "gap": 5},
  "endBinding": {"elementId": "target_id", "focus": 0, "gap": 5},
  "startArrowhead": null,
  "endArrowhead": "arrow"
}
```

For **dashed arrows** (optional paths, weak links): `"strokeStyle": "dashed"`.

For **curved arrows** (feedback loops, back-edges): use 3 points:
```json
"points": [[0, 0], [60, -80], [120, 0]]
```

For **arrow with label**: add a free-floating text element near the midpoint of the arrow.

---

## Line (structural, not directional)

Use for timelines, tree branch lines, dividers. Not for connections between shapes (use arrow for those).

```json
{
  "type": "line",
  "id": "line_1",
  "x": 100, "y": 100,
  "width": 0, "height": 200,
  "angle": 0,
  "strokeColor": "#adb5bd",
  "backgroundColor": "transparent",
  "fillStyle": "solid",
  "strokeWidth": 2,
  "strokeStyle": "solid",
  "roughness": 1,
  "opacity": 100,
  "groupIds": [],
  "seed": 66666,
  "version": 1,
  "isDeleted": false,
  "boundElements": null,
  "updated": 1,
  "link": null,
  "locked": false,
  "points": [[0, 0], [0, 200]]
}
```

---

## Small Marker Dot (timeline / bullet)

Use as visual anchors on timelines or to mark list items without a full shape.

```json
{
  "type": "ellipse",
  "id": "dot_1",
  "x": 94, "y": 94,
  "width": 12, "height": 12,
  "angle": 0,
  "strokeColor": "#1e40af",
  "backgroundColor": "#3b82f6",
  "fillStyle": "solid",
  "strokeWidth": 1,
  "strokeStyle": "solid",
  "roughness": 0,
  "opacity": 100,
  "groupIds": [],
  "seed": 77777,
  "version": 1,
  "isDeleted": false,
  "boundElements": null,
  "updated": 1,
  "link": null,
  "locked": false
}
```

---

## Section Background Rectangle

Used to visually group regions of the diagram. Low opacity, no bound text.

```json
{
  "type": "rectangle",
  "id": "bg_section_1",
  "x": 50, "y": 50,
  "width": 400, "height": 300,
  "angle": 0,
  "strokeColor": "#7048e8",
  "backgroundColor": "#e5dbff",
  "fillStyle": "solid",
  "strokeWidth": 1,
  "strokeStyle": "dashed",
  "roughness": 1,
  "opacity": 20,
  "groupIds": [],
  "seed": 88888,
  "version": 1,
  "isDeleted": false,
  "boundElements": null,
  "updated": 1,
  "link": null,
  "locked": false
}
```

Place background rectangles first in the `elements` array so they render behind other elements. Label them with a free-floating text element above the region.

---

## Complete Minimal Example

A two-node flowchart: Start → Process:

```json
{
  "type": "excalidraw",
  "version": 2,
  "source": "https://github.com/zsviczian/obsidian-excalidraw-plugin",
  "elements": [
    {
      "type": "ellipse",
      "id": "start",
      "x": 100, "y": 100, "width": 160, "height": 70,
      "angle": 0,
      "strokeColor": "#2f9e44", "backgroundColor": "#d3f9d8",
      "fillStyle": "solid", "strokeWidth": 2, "strokeStyle": "solid",
      "roughness": 1, "opacity": 100, "groupIds": [],
      "seed": 1001, "version": 1, "isDeleted": false,
      "boundElements": [{"id": "text_start", "type": "text"}, {"id": "arr1", "type": "arrow"}],
      "updated": 1, "link": null, "locked": false
    },
    {
      "type": "text", "id": "text_start",
      "x": 130, "y": 122, "width": 100, "height": 25,
      "angle": 0, "strokeColor": "#1a5c28", "backgroundColor": "transparent",
      "fillStyle": "solid", "strokeWidth": 1, "strokeStyle": "solid",
      "roughness": 1, "opacity": 100, "groupIds": [],
      "seed": 1002, "version": 1, "isDeleted": false,
      "boundElements": null, "updated": 1, "link": null, "locked": false,
      "text": "Start", "originalText": "Start",
      "fontSize": 18, "fontFamily": 5, "textAlign": "center", "verticalAlign": "middle",
      "containerId": "start", "lineHeight": 1.25, "autoResize": true
    },
    {
      "type": "arrow", "id": "arr1",
      "x": 260, "y": 135, "width": 100, "height": 0,
      "angle": 0, "strokeColor": "#5f3dc4", "backgroundColor": "transparent",
      "fillStyle": "solid", "strokeWidth": 2, "strokeStyle": "solid",
      "roughness": 1, "opacity": 100, "groupIds": [],
      "seed": 1003, "version": 1, "isDeleted": false,
      "boundElements": null, "updated": 1, "link": null, "locked": false,
      "points": [[0,0],[100,0]],
      "startBinding": {"elementId": "start", "focus": 0, "gap": 5},
      "endBinding": {"elementId": "proc", "focus": 0, "gap": 5},
      "startArrowhead": null, "endArrowhead": "arrow"
    },
    {
      "type": "rectangle", "id": "proc",
      "x": 360, "y": 100, "width": 180, "height": 70,
      "angle": 0, "strokeColor": "#5f3dc4", "backgroundColor": "#e5dbff",
      "fillStyle": "solid", "strokeWidth": 2, "strokeStyle": "solid",
      "roughness": 1, "opacity": 100, "groupIds": [],
      "roundness": {"type": 3},
      "seed": 1004, "version": 1, "isDeleted": false,
      "boundElements": [{"id": "text_proc", "type": "text"}, {"id": "arr1", "type": "arrow"}],
      "updated": 1, "link": null, "locked": false
    },
    {
      "type": "text", "id": "text_proc",
      "x": 380, "y": 122, "width": 140, "height": 25,
      "angle": 0, "strokeColor": "#374151", "backgroundColor": "transparent",
      "fillStyle": "solid", "strokeWidth": 1, "strokeStyle": "solid",
      "roughness": 1, "opacity": 100, "groupIds": [],
      "seed": 1005, "version": 1, "isDeleted": false,
      "boundElements": null, "updated": 1, "link": null, "locked": false,
      "text": "Process Step", "originalText": "Process Step",
      "fontSize": 16, "fontFamily": 5, "textAlign": "center", "verticalAlign": "middle",
      "containerId": "proc", "lineHeight": 1.25, "autoResize": true
    }
  ],
  "appState": {
    "gridSize": null,
    "viewBackgroundColor": "#ffffff"
  },
  "files": {}
}
```
