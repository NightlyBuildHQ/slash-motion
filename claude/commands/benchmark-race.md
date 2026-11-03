---
description: Generate a 60fps throughput benchmark race motion scene as one HTML file
argument-hint: [optional extra direction, e.g. "add a baseline vs. quantized legend"]
---

Create one self-contained HTML motion scene named `scenes/benchmark-race.html`. Create the `scenes/` folder if it does not exist.

Extra direction (ignore if empty): $ARGUMENTS

## Subject
A throughput race drawn on a Canvas 2D chart. Two curves draw from left to right over the same time axis:
- **Baseline** (muted, `#27272A` stroke with a light `#FAFAFA` label)
- **Optimized** (accent `#FF5500` stroke with a soft glow)

The counter starts at **42** and eases up to **318 tok/s** with `expo.out`. Show the unit `tok/s` in JetBrains Mono.

When the optimized curve reaches the end, a callout appears: `KV-Cache Quantization • 4.2x Throughput`. Give the callout an opaque background so it stays readable over the curve.

## Technical constraints
- Single file, no build step. Load Tailwind (`https://cdn.tailwindcss.com/3.4.16`) and GSAP (`https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/gsap.min.js`). Pin exact versions. Use Three.js only if you need it for a glow effect; a Canvas 2D chart is preferred.
- Fonts from Google Fonts: Inter (UI text) and JetBrains Mono (numbers and labels).
- Stage is a 420x780 px (9:16) frame centered in the viewport. Keep any control UI outside the stage.
- Palette as CSS custom properties: background `#09090B`, surface `#121215`, border `#27272A`, accent `#FF5500`, emerald `#10B981`, text `#FAFAFA`.
- Canvas: size the backing store to `devicePixelRatio`. Redraw only on change, and keep one draw per frame. Target 60 fps.
- Easing: `power3.out` for the curve draw, `expo.out` for the counter and callout.
- Respect `prefers-reduced-motion`: show the final chart and counter value.

## Timing (about 3.2 s per scene)
1. 0.0–0.5 s: type `/benchmark-race` and show a context pill.
2. 0.5–0.9 s: orange spark status line, "Animating with /benchmark-race...".
3. 0.9–3.2 s: full-bleed animation. Both curves draw, the counter climbs from 42 to 318, and the callout appears at the end.

## Controls
`1`–`6` play a scene, `A` or `Space` starts auto-play, `R` resets, `H` hides the control panel.

## Verification (required before you say it is done)
Open the file in a real browser. Capture a screenshot mid-race and one at the end state. Confirm the counter ends at exactly 318, that the callout is fully visible, that there are no console errors, and that frame times stay under 16.7 ms over a 3 s run. Report the measured numbers.
