---
name: diagramit
description: "Genera diagramas editables en FigJam a partir de informes, specs o flujos creativos. Usar cuando el usuario pida /Diagramit, diagramit, diagramar, visualizar un flujo, o crear un diagrama del informe semanal 2894_signals. Requiere Figma MCP autenticado y la skill figma-generate-diagram antes de cada llamada a generate_diagram."
disable-model-invocation: true
---

# Diagramit

Wrapper del proyecto para diagramar informes y flujos creativos en **FigJam** (no Mermaid en el chat).

## Antes de generar

1. Confirma que **Figma MCP** está conectado y autenticado en Cursor (plugin Figma del marketplace).
2. **Carga la skill `figma-generate-diagram`** del plugin Figma antes de cada llamada a `generate_diagram`.
3. Lee el material fuente (informe en `reports/`, PRD, spec) — no inventes nodos ni conexiones.

## Flujo

1. Identifica el tipo de diagrama (flowchart, sequence, state, gantt, erDiagram, architecture).
2. Sigue las restricciones universales de `figma-generate-diagram` (sin emojis, sin `\n` en labels, IDs camelCase, labels con caracteres especiales entre comillas).
3. Para flowcharts genéricos, aplica `references/flowchart.md` de la skill Figma.
4. Llama a `generate_diagram` con:
   - `name`: título descriptivo
   - `mermaidSyntax`: Mermaid validado
   - `userIntent`: qué quiere ver el usuario
5. Devuelve al usuario el **enlace FigJam** que retorna la herramienta.

## Para informes 2894_signals

- Fuente habitual: `reports/YYYY-MM-DD-ai-news.md`
- Diagrama recomendado: **flowchart LR** con subgraphs por categoría (diseño/tokens, imagen, video, recuperación) y decisión central (edición regional vs regeneración total).
- Guarda el Mermaid fuente en `docs/diagrams/YYYY-MM-DD-flujo-creativo.mmd` para reutilizar o iterar con `fileKey`.

## No hacer

- No pegar bloques Mermaid sueltos en el chat como sustituto de FigJam.
- No llamar `generate_diagram` sin cargar `figma-generate-diagram`.
- No usar `create_new_file` antes de `generate_diagram` (la herramienta crea su propio archivo).

## Si Figma MCP no está autenticado

Indica al usuario que conecte el plugin Figma en Cursor (Settings → MCP) y vuelva a invocar `/Diagramit`. Guarda el `.mmd` en `docs/diagrams/` para que la generación sea un solo paso tras autenticar.
