# dayflow-demo v2 — cinematic motion graphics demo

> 24.0s landscape (1920×1080, 30fps) cinematic motion graphics demo of the Dayflow app.
> Built the **brag-skill way**: every frame is a pure function of time (--t CSS var),
> captured frame-by-frame via Playwright screenshot() at true 30fps.

## What changed vs v1 (the bad version)

| Aspect | v1 (bad) | v2 (this) |
|---|---|---|
| Format | vertical 1080×1920 portrait | **landscape 1920×1080** (proper for desktop) |
| Capture | Playwright recordVideo (real-time, 25fps) | **--t-driven frame-by-frame screenshot() at 30fps** (the brag-skill way) |
| Framerate conversion | 25fps source → 30fps output via frame duplication (caused stutter) | **No duplication** — 720 unique frames captured at exact 30fps timecodes |
| Encoding | libx264 -preset ultrafast -crf 18 (4.2 Mbps, Constrained Baseline) | **libx264 -preset slow -crf 16** (2.8 Mbps, **High profile** — better quality per bitrate) |
| Framing | Phone content stuck in top-left of landscape player (looked "horrendously bad") | **Phone mockup centered on stylized dark background** (no letterbox issues) |
| App transitions | Source CSS transitions tied to wall-clock (played too fast/slow depending on capture rate) | **--t-driven CSS animations** (deterministic per frame, source's transitions nulled) |
| File size | 13 MB | 9.2 MB (smaller despite higher quality, thanks to better compression) |

## Deliverables

| File | Size | What |
|---|---|---|
| `dayflow_demo.mp4` | 9.2 MB | Final video — 1920×1080, 30fps, H264 High + AAC, visually lossless (-crf 16) |
| `dayflow_demo.jpg` | 75 KB | Poster (t=22.8s — fully visible brand outro with "Dayflow" text) |
| `demo.html` | 175 KB | Source + injected cinematic driver (--t-driven camera + state animations) |
| `source.html` | 158 KB | The uploaded Dayflow source, unmodified |

## Choreography (24.0s timeline)

| t (s) | Camera | Action |
|---|---|---|
| 0.0 | scale 1.0, opacity 0→1 | Fade in from black |
| 1.0 | scale 1.0 | Vignette fades in |
| 3.0 | scale 2.4, origin 50% 22% | Zoom into Today's night card |
| 4.8 | scale 1.0 | Zoom out |
| 5.5 | scale 1.0 | Switch to Habits tab (pill slides via --t) |
| 6.5 | scale 1.4, origin 50% 30% | Zoom into Habits hero |
| 8.0 | scale 2.8, origin 50% 62% | Push further into habit rows |
| 8.5 | hold | Tap first habit (checkmark draws + counter increments) |
| 9.12 | hold | "New Seal Earned" modal appears (shimmer chord SFX) |
| 10.0 | hold | Seal modal dismissed |
| 10.8 | scale 1.0 | Zoom out |
| 12.5 | scale 1.0 | Switch to Training tab |
| 14.0 | scale 1.6, origin 50% 32% | Zoom into training card |
| 16.0 | scale 1.0 | Zoom out |
| 16.5 | scale 1.0 | Switch to Nutrition tab |
| 18.0 | scale 2.4, origin 50% 28% | Zoom into kcal counter |
| 20.0 | scale 1.0 | Zoom out |
| 21.0 | scale 1.0 | Press + button (menu slides up) |
| 22.0 | scale 1.0 | Brand card fades in ("Dayflow. a day, in motion.") |
| 24.0 | scale 1.0, opacity 0.7 | End (dimmed) |

## How it was made (the brag-skill way)

1. **Every frame is a pure function of time**. All camera moves and visual transitions are CSS animations tied to `--t` via `animation-delay: calc(-1 * var(--t))`. Setting `--t = 5.0s` puts every animation at exactly the state it should be at 5.0s, regardless of wall-clock capture speed.

2. **Source's CSS transitions are nulled** (`transition: none !important`) so they don't fire on wall-clock time. The visual transitions are replaced with `--t`-driven CSS animations on the same properties (`.hl` transform, `.pane` opacity, `.ck.on` background + svg stroke-dashoffset, `#menu` opacity + transform, `#sm` opacity).

3. **One-shot app interactions** (tab clicks, habit check, plus menu) are fired by JS at specific `--t` timecodes via `window.__demoPlay(t)`, tracked with a `fired` object to avoid re-firing. The source's real event handlers run; my CSS animations override the visual transitions.

4. **Phone mockup on stylized background**. The source's `#st`/`#nav`/`#menu`/`#sm` are transplanted into a `#phone-frame` div (540×960 with 10px black border, 44px rounded corners, large soft drop shadow) centered on a dark gradient background with three drifting aurora blobs (`#5b6cff` periwinkle, `#ff6b57` coral, `#30c48d` green — the source's category colors).

5. **Frame-by-frame capture via Playwright `screenshot()` per frame at 30fps**. Captured 720 unique frames (24s × 30fps) over 338s of wall-clock (capture rate 2.1fps — doesn't matter since each frame is a pure function of `--t`).

6. **Wait for fonts and images to load before each capture** (`await page.evaluate(() => document.fonts.ready)` per frame).

7. **High-quality encoding**: libx264 -preset slow -crf 16 (visually lossless), H264 High profile, yuv420p, 1920×1080 @ 30fps, AAC 256k audio.

8. **Poster baked as frame 0** (frame 684 at t=22.8s — fully visible brand outro) so every platform's thumbnail shows the strongest settled frame.
