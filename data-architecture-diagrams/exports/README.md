# Exported diagram images

Place **SVG** or **PNG** exports here so they render directly in GitHub README files.

## How to export from draw.io

1. Open any file in [`../drawio/`](../drawio/) at [app.diagrams.net](https://app.diagrams.net)
2. **File → Export as → SVG** (recommended — stays sharp at any size)
3. Save with the same base name, e.g.:
   - `platform-api-rbac-er.svg`
   - `video-call-system-architecture.svg`
   - `yoruba-calendar-er.svg`
   - `pcss-content-model.svg`

## Embed in README

```markdown
![Platform API RBAC ER Diagram](exports/platform-api-rbac-er.svg)
```

## Mermaid vs exports

- **Mermaid** (in `../mermaid/`) renders on GitHub without exporting — use for quick docs
- **draw.io SVG exports** — use for polished portfolio diagrams and profile README previews
- **DBML** (in `../dbml/`) — export PNG from [dbdiagram.io](https://dbdiagram.io)
- **PlantUML** (in `../plantuml/`) — export SVG from [plantuml.com](https://www.plantuml.com/plantuml)
