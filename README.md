# MindFlow — Mind Map Editor

A powerful, browser-based mind mapping tool built as a single HTML file. No dependencies, no build step — just open and map.

![MindFlow](https://img.shields.io/badge/version-3.0-blue) ![License](https://img.shields.io/badge/license-MIT-green) ![Zero Dependencies](https://img.shields.io/badge/dependencies-0-brightgreen)

## Features

### Core Mind Mapping
- **Add / Edit / Delete nodes** — build your map with child and sibling topics
- **Drag & drop rearrange** — move nodes to a new parent by dragging onto them
- **Drag-to-reorder siblings** — drag a branch topic above or below a sibling to rearrange order (XMind-style)
- **Multi-select** (`Ctrl+Click`) — select multiple nodes for batch operations (delete, move)
- **Collapse / Expand** — fold branches to focus on what matters
- **5 depth levels** — distinct visual styling for root, main ideas, sub-topics, and details
- **Notes & Links** — attach rich notes and URLs to any node
- **Internal node links** — link one node to another; clicking jumps to and reveals the target (auto-expands collapsed ancestors)

### Layout Modes
- **Bilateral** — branches auto-distribute left and right from the center (default)
- **Right-only** — all branches extend to the right
- **Left-only** — all branches extend to the left
- **Org Chart** — top-down hierarchical layout
- **Tree** — indented tree layout

### XMind-Inspired Features
- **Search / Find** (`Ctrl+F`) — locate nodes instantly with match-by-match navigation
- **Copy / Cut / Paste** (`Ctrl+C` / `Ctrl+X` / `Ctrl+V`) — duplicate or move entire subtrees
- **Relationships** — draw labeled connecting lines between any two topics
- **Boundaries** — group related topics with a colored outline
- **Summaries** — add concluding brackets to sibling groups
- **Markers & Icons** — tag nodes with priority levels, task status, flags, and symbols
- **Outliner View** — toggle a hierarchical list panel for structured navigation
- **Floating Topics** — drag any node to empty canvas to detach it as an independent free-positioned topic; drag back onto another node to re-attach; right-click → "Detach as Floating Topic" also works
- **Zen Mode** — distraction-free fullscreen for focused brainstorming
- **Auto-numbering** — cycle through numbering styles (1. / 1.1. / a. / i.) for child nodes
- **Multi-sheet tabs** — create, rename, delete, and switch between multiple mind maps in the same file

### Format Panel (Per-Node Styling)
- **7 node shapes** — rectangle, rounded, pill, ellipse, underline, diamond, none
- **Background color** — custom fill color per node
- **Border style** — solid, dashed, dotted, or double borders with custom color and width
- **Font styling** — family (Inter / Georgia / JetBrains Mono), size, weight (bold), color
- **Text decoration** — italic, strikethrough, underline, text alignment
- **Connector style** — curve (bezier), straight, angular (L-shape), or step (H-V-H) per branch
- **Connector width & color** — customize line thickness and color with inheritance from parent
- **Node images** — embed images directly into nodes via file picker (Base64); resize with width control

### Theming & Styling
- **16 color themes** across 3 categories (Simple, Classic, Vivid)
- **Dark / Light mode** toggle (light mode default, XMind-inspired aesthetic)
- **Rainbow branches** — unique color per branch or uniform
- **Canvas background** — pick from curated background colors
- **Per-node colors** — customize individual node colors via right-click
- **XMind-style branch coloring** — Level 1 nodes get solid colored backgrounds; Level 2 nodes get colored side borders

### Export & Save
| Format       | Description                        |
|--------------|------------------------------------|
| **JSON**     | Full save/load with all metadata   |
| **PNG**      | High-res 2x raster image           |
| **SVG**      | Scalable vector graphic            |
| **Markdown** | Hierarchical outline with notes    |

### Undo / Redo
- Snapshot-based undo/redo system (up to 60 steps)
- Full state serialization preserves all node styles, images, sheets, connectors, and links

## Getting Started

1. **Open the file** — double-click `mindflow_v3.html` or serve it locally
2. **Start mapping** — the editor loads with a sample map ready to edit

That's it. No install, no server, no npm.

## Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `Tab` | Add child node |
| `Enter` | Add sibling node |
| `F2` | Edit selected node |
| `Delete` / `Backspace` | Delete selected node(s) |
| `/` | Fold / unfold |
| `Arrow keys` | Navigate between nodes |
| `Ctrl+Z` | Undo |
| `Ctrl+Y` | Redo |
| `Ctrl+S` | Save as JSON |
| `Ctrl+F` | Search nodes |
| `Ctrl+C` | Copy node subtree |
| `Ctrl+X` | Cut node subtree |
| `Ctrl+V` | Paste subtree under selected |
| `Ctrl+Click` | Multi-select nodes |
| `Esc` | Deselect / exit Zen Mode |
| `Scroll wheel` | Zoom in/out |
| `Click + drag` (canvas) | Pan the view |

## Mouse Actions

| Action | Result |
|--------|--------|
| **Click** node | Select |
| **Double-click** node | Edit text |
| **Right-click** node | Context menu (color, markers, copy, delete, etc.) |
| **Drag** node onto another | Reparent (move to new parent) |
| **Drag** node above/below sibling | Reorder siblings |
| **Drag** node to empty canvas | Detach as floating topic |
| **Ctrl+Click** nodes | Multi-select |
| **Click** collapse dot | Fold/unfold children |

## Toolbar Guide

| Button | Function |
|--------|----------|
| **Layout** | Switch between bilateral, right, left, org chart, or tree layout |
| **Relate** | Draw a relationship line between two nodes |
| **Boundary** | Add a grouping outline around selected node and its children |
| **Summary** | Add a summary bracket to sibling nodes |
| **Marker** | Open marker picker (priority, task, flag, symbol) |
| **Image** | Insert an image into the selected node |
| **Numbering** | Toggle auto-numbering style on child nodes |
| **Outline** | Toggle outliner panel |
| **Notes** | Toggle notes & link panel |
| **Format** | Toggle format panel (node shape, font, border, connector styling) |
| **Themes** | Open theme picker |
| **Zen** | Enter distraction-free mode |

## Multi-Sheet Tabs

The bottom bar provides a tab system for managing multiple mind maps within a single file:
- **+** — add a new sheet
- **Double-click** tab — rename the sheet
- **Right-click** tab — delete the sheet (minimum 1 sheet required)
- Sheet state (nodes, layout, zoom, pan) is saved and restored independently

## Architecture

The entire application is a single `mindflow_v3.html` file containing:

- **CSS** — custom properties for theming, Inter font, XMind-inspired design language
- **HTML** — toolbar, canvas viewport, side panels (notes, themes, format), context menus, sheet tabs
- **JavaScript** — vanilla JS with a flat node map (`NM`) data model

### Data Model

```
Node: {
  id, text, parentId, children[], collapsed, color, note, link, side, markers[],
  floatX, floatY,
  shape, bgColor, borderStyle, borderColor, borderWidth,
  fontFamily, fontSize, fontWeight, fontColor,
  italic, strikethrough, underline, textAlign,
  image, imageWidth,
  connStyle, connWidth, connColor,
  linkedNodeId
}

Relationship: { id, fromId, toId, label }
Boundary: { id, nodeIds[], color, label }
Summary: { id, nodeIds[], label }
Sheet: { name, state (full serialized map state) }
```

Layout is computed via recursive algorithms that distribute subtrees based on the selected layout mode (bilateral, right, left, org chart, or tree).

## Browser Support

Works in all modern browsers (Chrome, Firefox, Safari, Edge). No IE support.

## License

MIT
