# 🍄 Hyphae Growth Simulation

A generative art piece simulating the branching growth patterns of fungal hyphae — the thread-like filaments that form the body of a fungus. Built with [p5.js](https://p5js.org/).


## 🔬 Live Preview

[![Launch Live Preview](https://img.shields.io/badge/Launch-Live_Preview-brightgreen?style=for-the-badge)](https://adminnooot.github.io/myceliumgrowthhtml/)

> Interactive simulation with real-time controls — adjust origin point, branching, speed, and more.

---

## What It Does

Hundreds of filaments radiate outward from a single origin point, each one growing, wandering, and branching in real time. The result mimics the organic spread of mycelium across a dark surface.

Key behaviors:

- **Noise-driven wandering** — each hypha steers using Perlin noise, producing smooth, organic paths
- **Outward bias** — filaments are gently pulled away from the origin, preventing tangling
- **Tapering** — strokes thin over time as the hypha "uses up" its energy
- **Branching** — thicker, younger filaments occasionally split into two, with the probability decreasing each generation
- **Alpha-mapped opacity** — stroke opacity tracks filament width, so thin ends fade naturally into the background

---

## Parameters

| Variable | Default | Effect |
|---|---|---|
| `MAX_HYPHAE` | `5000` | Hard cap on simultaneous filaments |
| `spawnCount` | `80` | Number of filaments spawned at start |
| `generation` limit | `6` | Maximum branch depth |
| `taperRate` | `0.998 – gen×0.002` | How quickly each filament narrows |
| `speed` | `0.8–1.5 × 0.85^gen` | Movement per frame, slows with depth |
| `wanderScale` | `0.04–0.20` | Noise influence (stronger near origin) |

Tweak any of these in the `Hypha` constructor or `initSimulation()` to change the density, reach, and character of the growth.

---

## How It Works

```
setup()
  └─ createCanvas → initSimulation()
        └─ spawn 80 Hypha objects in a ring around the origin

draw() [every frame]
  └─ for each Hypha:
        ├─ update() — move, wander, taper, maybe branch
        └─ draw()  — render a line segment from prev → current pos
```

Each `Hypha` is removed from the array once it either:
- shrinks below a minimum stroke width (`0.1`)
- exits the canvas bounds

New branches are appended to the same `hyphae` array during `update()`, up to `MAX_HYPHAE`.

---

## Responsive Behavior

The canvas fills the full browser window. On resize, if the width changes by more than 20px (filtering out mobile address-bar scroll noise), the simulation resets and redraws from scratch.

---

## Tech

- [p5.js](https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.4.0/p5.js) `1.4.0` — loaded from CDN, no npm required
- Vanilla JS, single HTML file
- No build tools, no framework

---

## Usage

```bash
git clone https://github.com/adminnooot/myceliumgrowthhtml.git
cd myceliumgrowthhtml
open index.html   # or drag it into a browser
```

Or visit the [live GitHub Pages site](https://adminnooot.github.io/myceliumgrowthhtml/) for the interactive version with GUI controls.

**GUI Controls** (toggle with the ⚙ button in the top-left corner):

| Control | What it does |
|---|---|
| Origin X / Origin Y | Reposition where growth radiates from |
| Max Hyphae | Cap on simultaneous filaments |
| Spawn Count | Initial filaments spawned at start |
| Max Generations | Branch depth limit |
| Taper Rate | How quickly filaments narrow |
| Speed | Movement speed multiplier |
| Wander Scale | Perlin noise influence strength |
| Branch Prob | Chance of each filament splitting |
| ↺ Restart | Re-initialize with current slider values |

---

## License

MIT — do whatever you like with it.
