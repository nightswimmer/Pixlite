Pixlite is a standalone, self-contained image editing web app delivered as a single HTML file. It requires no server, no installation, and no internet connection after first load — just open the file in a browser.

Purpose
A lightweight but capable image editor for common photo editing tasks: cropping to standard aspect ratios and resolutions, resizing with high-quality multi-pass scaling, rotating, mirroring, and making tonal/color adjustments. It also includes a before/after split-screen comparison mode for non-destructive preview of changes.

Tech Stack

- React 18 (UMD bundles loaded via unpkg CDN)
- Babel Standalone — JSX is transpiled inline in the browser (no pre-build step, no separate App.jsx)
- HTML5 Canvas 2D for all image rendering and pixel manipulation
- SVG overlays for interactive UI elements (crop handles, rotation indicator, split bar)
- Everything lives in a single `pixlite.html` file (script tag with `type="text/babel"`)

Current Features

- Crop — free draw or aspect-ratio-locked presets grouped by tag (social, photo, video, web, legacy, custom): 1:1, 4:3, 3:2, 16:9, 9:16, 4:5, 2:1, 21:9, 1280×720, 1080×1080, 1200×630, 800×600, plus Custom W×H. Editable W/H inputs and a "Crop & Resize" action that crops + scales to exact pixel dimensions in one step
- Reference image overlay (Crop tool) — drop a second image onto the canvas to display it at 42% opacity inside the crop box as a framing guide; the crop aspect ratio auto-matches the reference
- Resize — quick scale buttons (25%, 50%, 2×, 4×) and custom dimensions with aspect-ratio lock; multi-pass stepped scaling (≤2× per step) for quality
- Rotate — drag-to-rotate on canvas with visual overlay; preset buttons (±90°, ±180°, ±45°) and fine-nudge buttons (±1°, ±5°, ±15°); live preview with Apply/Reset
- Mirror — horizontal and vertical flip
- Adjust — sliders for Brightness, Contrast, Saturation, Exposure, Highlights, Shadows, Temperature, Tint, Vignette; live pixel processing via canvas getImageData with Apply/Reset
- Before/After compare — vertical split bar draggable across the canvas; synced zoom and pan; enabled by default on Adjust and Resize tools
- Export modal — PNG, JPEG, WebP with a pannable/zoomable 100% preview; quality slider (10–100); Compare mode renders two formats side-by-side with independent format/quality controls, synced pan/zoom, and per-slot Download buttons; estimated file size shown
- Light/Dark mode toggle
- Undo history (single-step) and Reload original (discard all edits)
- Zoom (mouse wheel + toolbar +/−, 100%, Fit), pan (right/middle-click drag), fit-to-screen on load
- Toast notifications for key actions (load, apply, errors)
- Settings persistence via localStorage (`pixlite_settings`): theme, export format/quality for both compare slots, custom crop resolution

File Input

- Drag-and-drop onto the canvas (replaces image; when Crop is active, drops are treated as reference image)
- "Load new image" button with file picker; accepts any browser-decodable format (PNG, JPEG, WebP, GIF, …)

Architecture Notes
All hot-path values (zoom, pan, crop box, tool state, adjust sliders) are stored in refs for use inside event handlers, with a lightweight `forceTick` counter triggering React re-renders when needed. The canvas draw function reads exclusively from refs to avoid stale closure issues. SVG overlays are rendered in screen-space coordinates derived from the same ref values, ensuring the crop mask, rotation indicator, and split bar are always pixel-accurate.
