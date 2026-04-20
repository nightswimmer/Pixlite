# Pixlite

**Pixlite** is a standalone, browser-based image editor packaged as a single HTML file. No server, no install, no account — just open [index.html](index.html) in any modern browser and start editing.

## Features

- **Crop** — free draw or aspect-locked presets (1:1, 4:3, 3:2, 16:9, 9:16, 4:5, 2:1, 21:9, 1280×720, 1080×1080, 1200×630, 800×600) grouped by tag: social, photo, video, web, legacy, custom. Editable W/H inputs and "Crop & Resize" to exact pixel dimensions in one step.
- **Reference overlay** — drop a second image onto the canvas while in Crop mode to show it at 42% opacity inside the crop box as a framing guide.
- **Resize** — quick scales (25%, 50%, 2×, 4×) or custom W/H with aspect-ratio lock. Uses multi-pass stepped scaling (≤2× per step) for quality.
- **Rotate** — drag-to-rotate on the canvas with live preview; ±90°/±180°/±45° presets and ±1°/±5°/±15° fine nudges.
- **Mirror** — horizontal and vertical flip.
- **Adjust** — Brightness, Contrast, Saturation, Exposure, Highlights, Shadows, Temperature, Tint, and Vignette sliders with live canvas pixel processing.
- **Before/After compare** — draggable vertical split bar with synced zoom and pan; on by default for Adjust and Resize.
- **Export** — PNG, JPEG, or WebP with a 100%-zoom, pannable preview. Compare mode renders two formats side-by-side with independent quality sliders and estimated file size.
- **Light / Dark** mode toggle.
- **Undo** and **Reload original** to discard all edits.
- **Zoom & pan** — mouse wheel to zoom, right/middle-click drag to pan, Fit and 100% buttons.
- Drag-and-drop or file picker for opening images. Toast notifications for key actions. Settings (theme, export format/quality, custom resolution) persist in localStorage.

## Tech

- React 18 (UMD from CDN) + Babel Standalone — JSX is transpiled inline in the browser.
- HTML5 Canvas 2D for all pixel work; SVG overlays for crop handles, rotation indicator, and the split bar.
- One file, no build step: the entire app is [index.html](index.html).

## Usage

1. Clone or download this repo.
2. Open `index.html` in any modern browser — or point a static host (e.g. GitHub Pages) at the folder and it loads automatically.
3. Drop an image onto the canvas (or click **Load new image**).

Works fully offline after the first load (CDN bundles are cached by the browser).

## License

See [LICENSE](LICENSE).
