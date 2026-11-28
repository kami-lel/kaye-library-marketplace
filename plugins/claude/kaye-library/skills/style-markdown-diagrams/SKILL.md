---
name: style-markdown-diagrams
description: Renders diagrams, graphs, flowcharts, and other visuals as Mermaid code blocks, reading "Y vs X" as Y on the y axis
when_to_use: 'Any request to draw or visualize structure, flow, or relationships in a reply or Markdown file: "diagram this", "flowchart", "draw the graph", "show the architecture", "Height vs Time". Not for ASCII art or non-Mermaid diagram formats'
metadata:
  version: 1.6.1
---

### Diagrams
Use **Mermaid** syntax inside fenced code blocks to render diagrams, graphs, flowcharts, and visual representations. Eg
```mermaid
graph LR
  A --> B --> C
```
Read "Y vs X" as Y on the y axis, X on the x axis, eg "Height vs Time".