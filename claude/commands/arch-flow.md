---
description: Generate a 60fps isometric 3D architecture-flow motion scene as one HTML file
argument-hint: [optional extra direction, e.g. "add a rate limiter node"]
---

Create one self-contained HTML motion scene named `scenes/arch-flow.html`. Create the `scenes/` folder if it does not exist.

Extra direction (ignore if empty): $ARGUMENTS

## Subject
An isometric 3D service architecture. Four nodes: **API Gateway**, **LLM Router**, **Redis Cache**, **Vector DB**. Glowing packets travel along the connecting edges. Two live badges: `12ms` (latency) and `99.98%` (uptime).

## Technical constraints
- Single file, no build step. Load Tailwind (`https://cdn.tailwindcss.com/3.4.16`), GSAP (`https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/gsap.min.js`) and Three.js (`https://cdn.jsdelivr.net/npm/three@0.149.0/build/three.min.js`). Pin exact versions.
- Fonts from Google Fonts: Inter (UI text) and JetBrains Mono (numbers and labels).
- Stage is a 420x780 px (9:16) frame centered in the viewport. Keep any control UI outside the stage so screen recordings stay clean.
- Palette as CSS custom properties: background `#09090B`, surface `#121215`, border `#27272A`, accent `#FF5500`, emerald `#10B981`, text `#FAFAFA`.
- Rendering: one WebGL renderer, one animation loop (`gsap.ticker`). Dispose geometries and materials you create. Target 60 fps with no per-frame allocations.
- Easing: `power3.out` for entrances, `expo.out` for hero moves.
- Respect `prefers-reduced-motion`: show the final frame without motion.

## Timing (about 3.2 s per scene)
1. 0.0–0.5 s: type the command `/arch-flow` and show a context pill.
2. 0.5–0.9 s: orange spark status line, "Animating with /arch-flow...".
3. 0.9–3.2 s: full-bleed animation. Nodes rise into place, packets flow along the edges, badges count in.

## Controls
`1`–`6` play a scene, `A` or `Space` starts auto-play, `R` resets, `H` hides the control panel.

## Verification (required before you say it is done)
Open the file in a real browser. Capture a screenshot mid-animation and one at the end state. Confirm there are no console errors and that frame times stay under 16.7 ms over a 3 s run. Report the measured numbers.
