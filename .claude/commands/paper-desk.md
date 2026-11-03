---
description: Generate a 60fps paper-desk collage motion scene (cards, hand-drawn marks, highlighter) as one HTML file
argument-hint: [optional extra direction, e.g. "add a sticky note with a TODO"]
---

Create one self-contained HTML motion scene named `scenes/paper-desk.html`. Create the `scenes/` folder if it does not exist.

Extra direction (ignore if empty): $ARGUMENTS

## Subject
A cutting mat on a desk, with paper cards placed on it:
- Card 1: **Benchmark Report Fig. 4**, a small chart on paper.
- Card 2: an engineering note with short lines of monospace text.
- A hand-drawn orange `#FF5500` circle is drawn around a figure in the report. Animate it with an SVG `stroke-dashoffset` so it looks drawn by hand, with a slight wobble.
- An emerald `#10B981` highlighter swipe passes over one line of the note, drawn with a semi-transparent stroke.

Cards slide onto the mat one by one, with a small rotation that settles. A cutting-mat grid sits underneath.

## Technical constraints
- Single file, no build step. Load Tailwind (`https://cdn.tailwindcss.com/3.4.16`) and GSAP (`https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/gsap.min.js`). Pin exact versions. Use inline SVG for the hand-drawn marks.
- Fonts from Google Fonts: Inter (UI text) and JetBrains Mono (note text, labels and numbers).
- Stage is a 420x780 px (9:16) frame centered in the viewport. Keep any control UI outside the stage.
- Palette as CSS custom properties: background `#09090B`, surface `#121215`, border `#27272A`, accent `#FF5500`, emerald `#10B981`, text `#FAFAFA`. Paper cards use a warm off-white surface; keep them within the palette's dark mood by using a muted tone, not pure white.
- Animate only `transform`, `opacity` and SVG `stroke-dashoffset`. Target 60 fps.
- Easing: `power3.out` for card slides, `expo.out` for the hand-drawn marks.
- Respect `prefers-reduced-motion`: show the finished desk with all marks drawn.

## Timing (about 3.2 s per scene)
1. 0.0–0.5 s: type `/paper-desk` and show a context pill.
2. 0.5–0.9 s: orange spark status line, "Animating with /paper-desk...".
3. 0.9–3.2 s: full-bleed animation. Cards land on the mat, the orange circle is drawn, then the emerald highlighter sweeps across the note.

## Controls
`1`–`6` play a scene, `A` or `Space` starts auto-play, `R` resets, `H` hides the control panel.

## Verification (required before you say it is done)
Open the file in a real browser. Capture a screenshot mid-animation and one at the end state. Confirm the orange circle closes fully around its target, the highlighter stays on its line, that there are no console errors, and that frame times stay under 16.7 ms over a 3 s run. Report the measured numbers.
