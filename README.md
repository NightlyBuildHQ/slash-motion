# slash-motion

Programmatic 60fps engineering motion scenes built with Three.js, Canvas, and GSAP.

## Quickstart

Open `index.html` directly in a browser. There is no build step and no install.

The page loads Tailwind, GSAP, Three.js, and Google Fonts from CDNs, so it needs internet access and a WebGL-capable browser. It was tested in Chromium. The Tailwind Play CDN logs a "should not be used in production" warning in the console. This is expected.

### Keyboard

| Key         | Action                              |
|-------------|-------------------------------------|
| `1`–`6`     | Play scene 1–6                      |
| `A` or `Space` | Auto-play all scenes (about 20 s) |
| `R`         | Reset                               |
| `H`         | Hide or show the control panel      |

Open `index.html?autoplay` to start auto-play on load.

### Scenes

| Key | Command           | Scene                                          |
|-----|-------------------|------------------------------------------------|
| 1   | `/arch-flow`      | Isometric 3D service architecture with packets |
| 2   | `/gpu-teardown`   | Exploded accelerator board                     |
| 3   | `/benchmark-race` | Throughput curve race                          |
| 4   | `/code-diff`      | Tilted TypeScript diff                         |
| 5   | `/paper-desk`     | Cutting mat with cards and hand-drawn marks    |
| 6   | finale            | 2 × 3 grid of live mini scenes and source code |

Each scene runs for about 3.2 s: a command typed in, a status line, then the full-bleed animation.

The stage is 420 × 780 px (9:16), centered in the page. The control panel sits outside the stage so screen recordings stay clean.

## Project layout

```
index.html          The studio: all six scenes in one file
.claude/commands/   Slash-command templates for generating new scenes
README.md
```

## Slash commands

The files in `.claude/commands/` are Claude Code prompt templates. Each one generates a single self-contained HTML scene in `scenes/`, using the same palette, timing, and controls as `index.html`.

| Command           | Argument example                             |
|-------------------|----------------------------------------------|
| `/arch-flow`      | `add a rate limiter node`                    |
| `/gpu-teardown`   | `show the VRM voltage regulators`            |
| `/benchmark-race` | `add a baseline vs. quantized legend`        |
| `/code-diff`      | `use a Python file instead of TypeScript`    |
| `/paper-desk`     | `add a sticky note with a TODO`              |

Use them in any project:

1. Copy `.claude/commands/` into the project's `.claude/commands/` folder. For all projects, copy it to `~/.claude/commands/` instead.
2. Start Claude Code in that project and run a command:

   ```
   /arch-flow add a rate limiter node
   ```

`$ARGUMENTS` is replaced with the text after the command name. If you leave it out, the command uses its default scene spec.

Each command asks Claude to verify its output in a real browser (screenshots and frame-time measurement) before reporting it as done.
