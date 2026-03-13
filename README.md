# MindFlow — Mind Map Editor

A powerful, browser-based mind mapping tool built as a single HTML file. No dependencies, no build step — just open and map.

![MindFlow](https://img.shields.io/badge/version-3.0-blue) ![License](https://img.shields.io/badge/license-MIT-green) ![Zero Dependencies](https://img.shields.io/badge/dependencies-0-brightgreen)

## Features

### Core Mind Mapping
- **Add / Edit / Delete nodes** — build your map with child and sibling topics
- **Drag & drop** — rearrange nodes by dragging them to a new parent
- **Bi-directional layout** — branches auto-distribute left and right from the center
- **Collapse / Expand** — fold branches to focus on what matters
- **5 depth levels** — distinct visual styling for root, main ideas, sub-topics, and details
- **Notes & Links** — attach rich notes and URLs to any node

### XMind-Inspired Features
- **Search / Find** (`Ctrl+F`) — locate nodes instantly with match-by-match navigation
- **Copy / Cut / Paste** (`Ctrl+C` / `Ctrl+X` / `Ctrl+V`) — duplicate or move entire subtrees
- **Relationships** — draw labeled connecting lines between any two topics
- **Boundaries** — group related topics with a colored outline
- **Summaries** — add concluding brackets to sibling groups
- **Markers & Icons** — tag nodes with priority levels, task status, flags, and symbols
- **Outliner View** — toggle a hierarchical list panel for structured navigation
- **Floating Topics** — drag any node to empty canvas to detach it as an independent free-positioned topic. Drag it back onto another node to re-attach. Right-click → "Detach as Floating Topic" also works.
- **Zen Mode** — distraction-free fullscreen for focused brainstorming

### Theming & Styling
- **16 color themes** across 3 categories (Simple, Classic, Vivid)
- **Dark / Light mode** toggle
- **Rainbow branches** — unique color per branch or uniform
- **Canvas background** — pick from curated background colors
- **Per-node colors** — customize individual node colors via right-click

### Export & Save
| Format   | Description                        |
|----------|------------------------------------|
| **JSON** | Full save/load with all metadata   |
| **PNG**  | High-res 2x raster image           |
| **SVG**  | Scalable vector graphic            |
| **Markdown** | Hierarchical outline with notes |

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
| `Delete` / `Backspace` | Delete selected node |
| `/` | Fold / unfold |
| `Arrow keys` | Navigate between nodes |
| `Ctrl+Z` | Undo |
| `Ctrl+Y` | Redo |
| `Ctrl+S` | Save as JSON |
| `Ctrl+F` | Search nodes |
| `Ctrl+C` | Copy node subtree |
| `Ctrl+X` | Cut node subtree |
| `Ctrl+V` | Paste subtree under selected |
| `Esc` | Deselect / exit Zen Mode |
| `Scroll wheel` | Zoom in/out |
| `Click + drag` (canvas) | Pan the view |

## Mouse Actions

| Action | Result |
|--------|--------|
| **Click** node | Select |
| **Double-click** node | Edit text |
| **Right-click** node | Context menu (color, markers, copy, delete, etc.) |
| **Drag** node | Move to a new parent |
| **Click** collapse dot | Fold/unfold children |

## Toolbar Guide

| Button | Function |
|--------|----------|
| **Relate** | Draw a relationship line between two nodes |
| **Boundary** | Add a grouping outline around selected node and its children |
| **Summary** | Add a summary bracket to sibling nodes |
| **Marker** | Open marker picker (priority, task, flag, symbol) |
| **Outline** | Toggle outliner panel |
| **Notes** | Toggle notes & link panel |
| **Themes** | Open theme picker |
| **Zen** | Enter distraction-free mode |

## Architecture

The entire application is a single `mindflow_v3.html` file containing:

- **CSS** — custom properties for theming, no external frameworks
- **HTML** — toolbar, canvas viewport, side panels, context menus
- **JavaScript** — vanilla JS with a flat node map (`NM`) data model

### Data Model

```
Node: { id, text, parentId, children[], collapsed, color, note, link, side, markers[] }
Relationship: { id, fromId, toId, label }
Boundary: { id, nodeIds[], color, label }
Summary: { id, nodeIds[], label }
```

Layout is computed via a recursive algorithm that distributes subtrees vertically, with left/right balancing from the root.

## Browser Support

Works in all modern browsers (Chrome, Firefox, Safari, Edge). No IE support.

## License

MIT
