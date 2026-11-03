---
description: Generate a 60fps exploded-view GPU teardown motion scene as one HTML file
argument-hint: [optional extra direction, e.g. "show the VRM voltage regulators"]
---

Create one self-contained HTML motion scene named `scenes/gpu-teardown.html`. Create the `scenes/` folder if it does not exist.

Extra direction (ignore if empty): $ARGUMENTS

## Subject
An exploded isometric view of an AI accelerator board, built from stacked layers: **Cold Plate** (top), **HBM3e** memory stacks (both sides of the die), **Tensor Core Die** (center), and the **PCB** (base). The layers start apart, then assemble into a closed unit, with the cut-away lines drawn in as they settle.

Callout labels, exactly as written:
- `01 HBM3e — 192GB @ 8TB/s`
- `02 Tensor Core Die — FP8`
- `03 Cold Plate — 1.2kW liquid`

Labels attach to their parts with thin leader lines that are projected from 3D to screen space each frame.

## Technical constraints
- Single file, no build step. Load Tailwind (`https://cdn.tailwindcss.com/3.4.16`), GSAP (`https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/gsap.min.js`) and Three.js (`https://cdn.jsdelivr.net/npm/three@0.149.0/build/three.min.js`). Pin exact versions.
- Fonts from Google Fonts: Inter (UI text) and JetBrains Mono (numbers and labels).
- Stage is a 420x780 px (9:16) frame centered in the viewport. Keep any control UI outside the stage.
- Palette as CSS custom properties: background `#09090B`, surface `#121215`, border `#27272A`, accent `#FF5500`, emerald `#10B981`, text `#FAFAFA`. Use `#FF5500` for the active part and its callout only.
- Rendering: one WebGL renderer, one animation loop (`gsap.ticker`). Dispose geometries and materials. Use simple box and plane geometry with low draw-call counts. Target 60 fps.
- Easing: `power3.out` for entrances, `expo.out` for the explode and assemble moves.
- Respect `prefers-reduced-motion`: show the assembled view without motion.

## Timing (about 3.2 s per scene)
1. 0.0–0.5 s: type `/gpu-teardown` and show a context pill.
2. 0.5–0.9 s: orange spark status line, "Animating with /gpu-teardown...".
3. 0.9–3.2 s: full-bleed animation. Layers separate, labels slide in in order 01, 02, 03, and the view settles at a slight rotation.

## Controls
`1`–`6` play a scene, `A` or `Space` starts auto-play, `R` resets, `H` hides the control panel.

## Verification (required before you say it is done)
Open the file in a real browser. Capture a screenshot mid-explode and one at the end state. Confirm that all three labels are fully inside the stage (no clipping at the edges), that there are no console errors, and that frame times stay under 16.7 ms over a 3 s run. Report the measured numbers.
