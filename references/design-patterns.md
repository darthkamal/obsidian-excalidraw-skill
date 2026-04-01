# Design Patterns & Diagram Strategy

## Visual Pattern Library

Match the visual structure to what the concept *does*, not just what it *is*. Each major concept should use a different pattern.

### Fan-Out (One-to-Many)
Central source radiates arrows to multiple outputs. Use for: hubs, root causes, PRDs, anything that spawns multiple things.
```
         ○
        ↗
  [Hub] → ○
        ↘
         ○
```

### Convergence (Many-to-One)
Multiple inputs merge into one output. Use for: aggregation, synthesis, funnels, decision points with prerequisites.
```
  ○ ↘
  ○ → [Result]
  ○ ↗
```

### Assembly Line (Transformation)
Input → Process → Output with clear before/after. Use for: data transformations, pipelines, conversion flows.
```
  [Raw Input] → [Transform] → [Clean Output]
```

### Cycle (Continuous Loop)
Steps in sequence with an arrow returning to the start. Use for: feedback loops, iterative processes, OODA loops.
```
  A → B
  ↑     ↓
  D ← C
```

### Tree / Hierarchy
Lines + free-floating text, no boxes needed. Use for: file systems, org charts, taxonomies, concept breakdowns.
```
  Root
  ├── Branch 1
  │   ├── Leaf A
  │   └── Leaf B
  └── Branch 2
```
Build with `line` elements (trunk and branches) + free-floating text labels. No boxes needed.

### Timeline
Vertical or horizontal line with small dot markers at intervals. Use for: event sequences, milestones, model evolution, protocol steps.
```
  ●─── Event 1
  │
  ●─── Event 2
  │
  ●─── Event 3
```
Build with one `line` element for the spine, small `ellipse` elements (12 px) as markers, and free-floating text beside each dot.

### Side-by-Side Comparison
Two parallel groups with a shared baseline or connecting axis. Use for: before/after, option A vs option B, traditional vs modern.
```
  [Option A]    [Option B]
  ─────────    ─────────
  Feature 1    Feature 1
  Feature 2    Feature 2
```

### Swimlane
Separate horizontal or vertical bands for each actor/system, with arrows crossing bands. Use for: cross-system workflows, responsibility boundaries.
```
  ┌─ User ─────────────┐
  │ Request → Wait      │
  └─────────────────────┘
  ┌─ System ────────────┐
  │ Process → Respond   │
  └─────────────────────┘
```
Build with large background rectangles (low opacity, dashed border) as lanes, plus a free-floating text title for each lane.

---

## Multi-Zoom Architecture

Comprehensive technical diagrams operate at three zoom levels simultaneously:

**Level 1 — Summary flow:** A simplified 3–5 step overview at the top or bottom of the diagram. The 10,000-foot view.

**Level 2 — Section boundaries:** Labeled regions (background rectangles) that group related components. Creates "rooms" — viewers know what belongs together.

**Level 3 — Detail inside sections:** Concrete examples, specific labels, step names, real identifiers. This is where the educational value lives.

For technical diagrams, aim for all three levels. For conceptual sketches, Level 2 alone is fine.

---

## Section-by-Section Strategy (Large Diagrams)

**Never generate an entire complex diagram in a single pass.** The output token limit will truncate the JSON mid-element, producing a broken file. Even if it fits, section-by-section produces better results.

### Phase 1: Build sections one at a time

1. **Create the base file** with the JSON wrapper and the first section's elements.
2. **Add one section per edit.** Think carefully about layout and cross-section connections before adding each section.
3. **Use descriptive string IDs** (`"auth_start"`, `"db_query_rect"`) so cross-section references are readable.
4. **Namespace seeds by section** — section 1: 1xxxx, section 2: 2xxxx, etc. Avoids collisions.
5. **Update `boundElements`** on both ends of any arrow that crosses sections when you add the new section.

### Phase 2: Review the whole

After all sections are in place:
- Do cross-section arrows bind correctly on both ends?
- Is spacing balanced, or are some sections cramped?
- Do all IDs and bindings reference elements that exist?

### Phase 3: Final validation

Check against the quality checklist in SKILL.md before saving.

### Typical section plan

- **Section 1:** Entry point, title, summary flow strip
- **Section 2:** First major component or decision
- **Section 3:** Main content (hero section — largest)
- **Section 4–N:** Remaining phases, outputs, legend

---

## Container Discipline

**Default to free-floating text. Add containers only when they carry meaning.**

| Use a container when... | Use free-floating text when... |
|------------------------|-------------------------------|
| It's the focal point of a section | It's a label or description |
| Arrows need to connect to it | It's a heading or annotation |
| The shape IS the meaning (decision diamond, cylinder) | Typography alone creates hierarchy |
| It groups children (swimlane background) | It describes something nearby |

**Typography as hierarchy:** A 28 px title doesn't need a rectangle around it. A 14 px annotation beside a shape doesn't need a box. Use font size and color to create hierarchy before reaching for containers.

**The container test:** For each boxed element, ask: "Would this work as free-floating text?" If yes, remove the container.

---

## Size Guidelines

| Element Role | Width × Height |
|---|---|
| Hero / primary node | 240 × 100 |
| Standard process box | 180 × 80 |
| Small / secondary | 140 × 60 |
| Decision diamond | 180 × 100 |
| Section background | Varies — at least 60 px padding around contents |

Whitespace encodes importance: the most important element has the most empty space around it (200 px+).

---

## Bad vs Good

| Bad (just displays) | Good (argues a relationship) |
|---------------------|------------------------------|
| 5 equal boxes labeled A–E | Each concept has a shape that mirrors its behavior |
| Uniform card grid | Structure matches conceptual structure |
| Same container for everything | Distinct visual vocabulary per concept |
| Every label in a box | Free-floating text with selective containers |
| "API" → "Database" | Real step names, real data labels |
