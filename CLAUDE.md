# CLAUDE.md — MindFlow Project Instructions

## Project Overview
Browser-based mind mapping tool inspired by XMind. Zero external dependencies — single HTML file (`mindflow_v3.html`) containing all CSS, HTML, and JavaScript. No build step, no npm, no server required.

**Owner:** David (Eaglemamba)
**License:** MIT
**Version:** 3.0

---

## Key Files
- `mindflow_v3.html` — the entire application (1,580 lines, ~92 KB)
- `README.md` — feature documentation and keyboard shortcut reference

**Do not create separate JS/CSS files.** The single-file architecture is intentional.

---

## Code Structure (mindflow_v3.html)

| Lines | Section |
|-------|---------|
| 1–330 | HTML head + embedded CSS (themes, layout, components) |
| 331–445 | HTML body (toolbar, canvas, panels, dialogs, menus) |
| 447–525 | Data model + state variables |
| 527–815 | Core functions (layout, render, undo/redo) |
| 999–1,041 | Node editing (add, delete, edit, collapse) |
| 1,043–1,060 | Pan & zoom |
| 1,065–1,086 | Keyboard handling |
| 1,088–1,199 | Panels, menus, save/load |
| 1,202–1,319 | Export (JSON, Markdown, SVG, PNG) + clipboard |
| 1,322–1,580 | Relationships, boundaries, summaries, markers, floating topics, outliner, zen mode |

---

## Data Model

```js
// Node
{ id, text, parentId, children[], collapsed, color, note, link, x, y, side, markers[], floatX, floatY }

// Relationship (curved dashed connector between any two nodes)
{ id, fromId, toId, label }

// Boundary (colored outline grouping sibling nodes)
{ id, nodeIds[], color, label }

// Summary (bracket label for a group of siblings)
{ id, nodeIds[], label }
```

**Key global state:** `NM` (node map), `selectedId`, `scale`, `panX`, `panY`, `undoStack`, `redoStack`

---

## Architecture Decisions
- Vanilla HTML/CSS/JS — no frameworks, no libraries (Google Fonts is the only external resource)
- Markdown + Gemini 1M context NOT applicable here — this is a standalone browser app
- Layout algorithm: recursive bi-directional tree (`layoutBranch()` + `doLayout()`)
- Themes: 16 color themes × 2 modes (dark/light) + 12 background colors via CSS variables
- Export: JSON (full state), Markdown (outline), SVG (vector), PNG (2× DPI)
- Undo/redo: snapshot-based, 60-deep stack

---

## How to Add a New Feature
1. Identify which section the feature belongs to (see line map above)
2. Add new functions in the appropriate section — keep the ASCII divider comments
3. If adding a new toolbar button: add HTML button → add CSS → add JS handler
4. If modifying the data model: update `exportJSON()` and `importJSON()` for backward compatibility
5. Test all 4 export formats after any render change

---

## Git Workflow
- Remote: `git@github.com:Eaglemamba/MindMap.git` (SSH)
- Branch naming: `claude/feature-name-XXXXX`
- PR workflow: Claude creates branch → push → Eaglemamba merges
- Do NOT push directly to `main`

---

## Style Preferences
- Direct, consulting tone. No emojis.
- Vanilla JS — no jQuery, no lodash, no frameworks
- Keep functions small and named clearly
- Amaran brand colors NOT applicable here (this is a personal tool, not pharma)
- Dark theme is default

---

## Current Status
- Version 3.0: feature-complete for core use case
- Floating topics, relationships, boundaries, summaries, markers, outliner, zen mode — all done
- Potential next features: localStorage auto-save, multi-sheet support, image insertion, mobile responsiveness

---

## Known Complexity — Read Before Modifying
- `layoutBranch()` / `doLayout()`: recursive layout with left/right balancing. Modifying this affects the entire tree render.
- `render()`: rebuilds the full DOM on every state change. Do not add expensive operations here.
- `exportSVG()` / `exportPNG()`: depends on canvas size and current zoom — test after any layout change.
- `importJSON()`: must stay backward compatible with older saved files.
