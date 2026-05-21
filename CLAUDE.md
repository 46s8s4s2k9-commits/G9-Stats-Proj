# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project overview

Grade 9 statistics project — a single-page academic report investigating whether study method (Offline/Online/Hybrid) and family income level are associated with final exam scores. Dataset: Kaggle's "Student Lifestyle vs. Academic Performance" (n = 8,000).

Authors: Bryan Tu, Andy Sha, Kingsley Sy.

## Repository structure

Everything lives in `index.html` — a self-contained page with embedded CSS and JavaScript. The repo has no build step, no dependencies to install, and no tests.

```
index.html   — The entire project: HTML structure, CSS styles, Chart.js charts, simulation renderers, and scroll animations
README.md    — Title only
```

## Making changes

Open `index.html` directly in a browser to preview. No build step required — edit the file and refresh.

## External libraries (loaded via CDN)

- **Chart.js** (v4, `chart.js`) — all bar charts, histogram, and simulation distribution charts
- **AOS** (Animate on Scroll v2.3.1) — scroll-triggered fade/translate animations (`data-aos` attributes)

## Key data in the JS block

- `SIM` object — pre-computed randomization distribution data (centers + counts) for 6 group comparisons, each from 1,000 simulations. Each sim key has `obs` (observed mean difference) and `p` (p-value).
- `HIST` object — binned histogram data for the full-dataset final score distribution (12 bins, 20–100).
- `MEAN`, `SD`, `N` — full-dataset constants: mean 83.21, std dev 12.76, n = 8,000.

## Chart rendering notes

- Simulation charts are lazy-rendered on tab click via `buildSimChart()` and a custom Chart.js `vline` plugin that draws the observed-difference marker.
- Tab groups are initialized with `initTabGroup()`. First panel builds immediately; subsequent panels build on first activation.
- Counter animations (`[data-count]`) and progress bar fills (`[data-w]`) are triggered by IntersectionObserver.
- The hero canvas (`#hcv`) runs a persistent particle-network animation loop.
