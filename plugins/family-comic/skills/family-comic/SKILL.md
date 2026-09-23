---
name: family-comic
description: "Turn a family moment, memory, or lighthearted scenario into one cohesive six-panel comic in the bundled reference image's established visual style."
---

# Family Comic

Create a warm, easy-to-read six-panel family comic from the user's premise. Keep the tone affectionate and grounded in the requested situation; do not add private facts, names, or character traits the user has not supplied.

## Style reference

`assets/family-comic-style-reference.jpg` is the canonical visual reference. Before generating a comic, inspect it and include it as a **style reference image** in the image-generation request. Match its soft anime-influenced chibi illustration, dark rounded panel outlines, warm muted night-time palette, expressive faces, clean 2-by-3 grid, rounded white text boxes, and hand-drawn Traditional Chinese lettering treatment. It guides the look only: do not copy its exact scenes, dialogue, or layout details unless the user requests them.

## Comic construction

- Produce one finished image with exactly six distinct, clearly separated panels in a readable 2-by-3 grid.
- Build a small visual arc: setup, development, turn, and a gentle payoff. Give every panel a distinct story beat.
- Preserve character continuity across all panels: recognizable faces, hairstyles, clothing, relationships, ages, and key props. Reuse user-provided character details exactly; make minimal neutral assumptions only when needed to draw the scene.
- Keep dialogue brief. If exact wording matters, quote it verbatim in the prompt and ensure it is legible. Use Traditional Chinese when the user writes in Chinese, unless they request another language.
- Maintain an all-ages, family-friendly tone unless the user explicitly asks for a different treatment.

## Generation workflow

1. Distill the request into six beats. Ask one concise question only when a missing detail would materially alter the characters or story.
2. Load the canonical asset with `view_image`; label it as a style reference, not an edit target.
3. Use the built-in image generation tool. Specify that the result is one finished six-panel comic, not six separate images.
4. Include the six beats, character-continuity details, any exact in-image text, and the reference-derived visual constraints in the prompt.
5. Inspect the result for panel count, reading order, continuity, legibility, and style match. If needed, regenerate with one focused correction.

Use a structured prompt along these lines:

```text
Use case: illustration-story
Asset type: finished six-panel family comic
Input image: canonical family-comic style reference; match visual style only
Story: <one-sentence premise>
Characters: <appearance and relationships>
Six panel beats: 1) <...> 2) <...> 3) <...> 4) <...> 5) <...> 6) <...>
Style/medium: match the bundled reference image's illustration, linework, palette, panel framing, and emotional tone
Text (verbatim): <only requested dialogue/captions>
Constraints: one single image; exactly six distinct bordered panels in a 2-by-3 grid; clear reading order; consistent characters and props; legible text; no watermark
```
