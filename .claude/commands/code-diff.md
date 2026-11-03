---
description: Generate a 60fps 3D-tilted code diff motion scene as one HTML file
argument-hint: [optional extra direction, e.g. "use a Python file instead of TypeScript"]
---

Create one self-contained HTML motion scene named `scenes/code-diff.html`. Create the `scenes/` folder if it does not exist.

Extra direction (ignore if empty): $ARGUMENTS

## Subject
A TypeScript code editor, tilted in 3D, showing a refactor in progress:
- Line numbers and syntax coloring in JetBrains Mono.
- Removed lines get a red strikethrough and fade out.
- Added lines in emerald `#10B981` slide in with a left border.
- A badge reads `Heap usage: -68%`. It counts down from its starting value with `expo.out`.

The editor gets a subtle 3D tilt (rotateX/rotateY) that settles as the diff plays. Keep the editor's text sharp: apply the transform to a container, not to each line.

## Technical constraints
- Single file, no build step. Load Tailwind (`https://cdn.tailwindcss.com/3.4.16`) and GSAP (`https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/gsap.min.js`). Pin exact versions. Use CSS 3D transforms for the tilt; Three.js is optional.
- Fonts from Google Fonts: Inter (UI text) and JetBrains Mono (code, numbers and labels).
- Stage is a 420x780 px (9:16) frame centered in the viewport. Keep any control UI outside the stage.
- Palette as CSS custom properties: background `#09090B`, surface `#121215`, border `#27272A`, accent `#FF5500`, emerald `#10B981`, text `#FAFAFA`. Use `#FF5500` for the cursor and the badge.
- Animate only `transform` and `opacity` for smooth frames. Target 60 fps.
- Easing: `power3.out` for line entrances, `expo.out` for the tilt and the badge counter.
- Respect `prefers-reduced-motion`: show the final diff state.

## Timing (about 3.2 s per scene)
1. 0.0–0.5 s: type `/code-diff` and show a context pill.
2. 0.5–0.9 s: orange spark status line, "Animating with /code-diff...".
3. 0.9–3.2 s: full-bleed animation. The editor tilts in, red lines strike through, green lines land, and the badge counts down to `-68%`.

## Controls
`1`–`6` play a scene, `A` or `Space` starts auto-play, `R` resets, `H` hides the control panel.

## Verification (required before you say it is done)
Open the file in a real browser. Capture a screenshot mid-diff and one at the end state. Confirm the badge text is fully visible, that the code is not clipped at the top or bottom edge, that there are no console errors, and that frame times stay under 16.7 ms over a 3 s run. Report the measured numbers.
