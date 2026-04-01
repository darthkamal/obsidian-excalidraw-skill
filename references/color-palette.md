# Color Palette

Single source of truth for all colors. Use semantic purpose to pick fill/stroke pairs — never invent colors outside this palette.

---

## Shape Colors (Semantic)

Always pair a lighter fill with a darker stroke for contrast.

| Semantic Purpose | Fill | Stroke | Text on Fill |
|-----------------|------|--------|--------------|
| Start / trigger / input | `#d3f9d8` | `#2f9e44` | `#1a5c28` |
| End / success / output | `#c5f6fa` | `#0c8599` | `#0a5d6a` |
| Process / action / step | `#e5dbff` | `#5f3dc4` | `#3b1f8c` |
| Decision / branch | `#fff4e6` | `#e67700` | `#7c4a00` |
| Data / storage / memory | `#fff3bf` | `#e67700` | `#7c4a00` |
| External / actor / system | `#f8f9fa` | `#868e96` | `#343a40` |
| Warning / error / critical | `#ffe3e3` | `#c92a2a` | `#7b1414` |
| Highlight / emphasis | `#ffd8a8` | `#e67700` | `#7c4a00` |
| AI / ML / model | `#ddd6fe` | `#6d28d9` | `#3b1f8c` |
| Neutral / secondary | `#f1f3f5` | `#adb5bd` | `#343a40` |

---

## Text Colors (Hierarchy)

Use on free-floating text (no container) to create visual hierarchy without boxes.

| Level | Color | Use For |
|-------|-------|---------|
| Section title | `#1e40af` | Major headings, diagram title |
| Subtitle | `#3b82f6` | Subheadings, group labels |
| Body / label | `#374151` | Descriptions, node annotations |
| Muted / metadata | `#757575` | Secondary notes, version info |
| On light-colored fills | `#374151` | Text inside any light shape |
| On dark-colored fills | `#ffffff` | Text inside dark shapes (rare) |

**Minimum contrast on white background:** Never use text colors lighter than `#757575`.

---

## Section Background Colors

Large background rectangles (low opacity, used to group diagram regions):

| Purpose | Fill | Stroke | Opacity |
|---------|------|--------|---------|
| Frontend / UI layer | `#dbe4ff` | `#4c6ef5` | 20 |
| Logic / processing layer | `#e5dbff` | `#7048e8` | 20 |
| Data / storage layer | `#d3f9d8` | `#2f9e44` | 20 |
| External / boundary | `#f1f3f5` | `#adb5bd` | 20 |

Use these as large background rectangles with low opacity to visually group related elements — not as containers with bound text.

---

## Arrow and Line Colors

| Element | Color |
|---------|-------|
| Primary flow arrows | Match source element's stroke color |
| Secondary / optional (dashed) | `#868e96` |
| Structural lines (timelines, tree branches) | `#adb5bd` |
| Timeline marker dots | `#3b82f6` fill + `#1e40af` stroke |

---

## Canvas Background

`viewBackgroundColor: "#ffffff"`

---

## Quick Reference Card

```
Start      fill:#d3f9d8  stroke:#2f9e44
End        fill:#c5f6fa  stroke:#0c8599
Process    fill:#e5dbff  stroke:#5f3dc4
Decision   fill:#fff4e6  stroke:#e67700
Data       fill:#fff3bf  stroke:#e67700
External   fill:#f8f9fa  stroke:#868e96
Error      fill:#ffe3e3  stroke:#c92a2a
AI/Model   fill:#ddd6fe  stroke:#6d28d9

Title text     #1e40af
Subtitle text  #3b82f6
Body text      #374151
Muted text     #757575
```
