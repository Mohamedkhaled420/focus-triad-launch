# dayflow-demo — cinematic motion graphics demo

> 24.0s vertical (1080×1920, 30fps) cinematic motion graphics demo of the
> Dayflow app. Real source HTML, real micro-interactions, driven by a
> choreographed camera (zoom in/out, pan) over a 4-tab tour with a brand outro.

## Deliverables

| File | Size | What |
|---|---|---|
| `dayflow_demo.mp4` | 13 MB | Final video — 1080×1920, 30fps, H264 video + AAC audio (music + SFX), cinematic vignette overlay |
| `dayflow_demo.jpg` | 71 KB | Poster frame (t=11s — habit check moment, the most cinematic interaction) |
| `work/source.html` | 158 KB | The uploaded source HTML, unmodified |
| `work/demo.html` | 165 KB | Source + injected cinematic camera driver |
| `work/video/*.webm` | 2.8 MB | Raw Playwright video recording (25fps, 28s) |
| `work/video_only.mp4` | 16 MB | Trimmed + 30fps-converted video (no audio, no vignette) |
| `work/audio/mix.wav` | 1.7 MB | Final audio mix (48kHz stereo, 24.0s) |
| `work/audio/music.wav` | 1.7 MB | Music stem — Cmaj9 pad + sub-bass + high shimmer |
| `work/audio/sfx.wav` | 1.7 MB | SFX stem — UI ticks, camera rumbles, whooshes, confirm chords |

## Choreography (24.0s timeline)

| t (s) | Camera | Action | UI effect |
|---|---|---|---|
| 0.0 | scale 1.05 (fade-in) | Fade in from black | App appears |
| 0.6 | scale 1.05 → 1.00 | zoom-out + vignette on | Settled framing |
| 1.6 | scale 1.00 → 1.40 (translate -10%) | zoom-today-hero | Today's night card + clock fills frame |
| 4.0 | scale 1.40 → 1.00 | zoom-out | Pull back to full Today view |
| 5.5 | scale 1.00 | click Habits tab | Tab pill highlight slides, habits pane fades in |
| 6.6 | scale 1.00 → 1.25 (translate +5%) | zoom-habits-hero | Counter + streak grid scales up |
| 8.6 | scale 1.25 → 1.55 (translate +22%) | zoom-habit-rows | Camera pushes into the habit list |
| 10.5 | hold | tap first habit checkbox | Check circle fills, checkmark SVG draws, counter increments — **New Seal Earned** modal slides up with shimmer burst |
| 12.0 | scale 1.55 → 1.00 | dismiss seal modal + zoom-out | Modal fades, pull back |
| 13.5 | scale 1.00 | click Training tab | Training pane fades in, "Picked for You" card visible |
| 14.6 | scale 1.00 → 1.20 (translate -8%) | zoom-training | Push into training card |
| 16.5 | scale 1.20 → 1.00 | zoom-out | Pull back |
| 18.0 | scale 1.00 | click Nutrition tab | Nutrition pane fades in, kcal counter visible |
| 19.0 | scale 1.00 → 1.45 (translate -18%) | zoom-kcal | Push into kcal counter |
| 21.0 | scale 1.45 → 1.00 | zoom-out | Pull back |
| 22.5 | scale 1.00 | click + button | Plus menu slides up from bottom-right |
| 23.2 | scale 1.00 | brand card show | "Dayflow" text fades in over dimmed app, tagline "a day, in motion." |
| 23.7 | scale 1.00, opacity 0.55 | fade-final | App dims behind brand card |
| 24.0 | end | | (Black) |

## Camera system

The driver wraps `#st` (the main content area) in a `#camera` div. The bottom nav pill (`#nav`) and slide-up menu (`#menu`) stay outside the camera so they're always visible at their natural size.

Each camera position is a CSS class on `#camera`:

```css
#camera.zoom-today-hero    { transform: scale(1.40) translate(0, -10%); }
#camera.zoom-habits-hero   { transform: scale(1.25) translate(0, 5%); }
#camera.zoom-habit-rows    { transform: scale(1.55) translate(0, 22%); }
#camera.zoom-training      { transform: scale(1.20) translate(0, -8%); }
#camera.zoom-kcal          { transform: scale(1.45) translate(0, -18%); }
#camera.zoom-out           { transform: scale(1.00) translate(0, 0); }
```

Transitions between classes use `cubic-bezier(0.32, 0.72, 0, 1)` (Apple's spring) over 1.6s.

## Audio

**Music**: layered Cmaj9 pad (C3 + E3 + G3 + B3 + D5 sines, low-passed 700 Hz, 0.20 Hz tremolo) + sub-bass C2 (65.41 Hz) for warmth + high shimmer (E5 + B5) that swells in the middle (bell curve from t=6 to t=22). Emotional swell: quieter at start, +10% bump during the habit check (t=10-12), recedes for the brand outro. ~ -13 dB.

**SFX** (synced to choreography):
- 1 intro fade-in whoosh (sine sweep 100→50 Hz, 1.2s)
- 7 camera zoom rumbles (sine sweeps 50→200 Hz or reverse, 0.7-0.9s each)
- 4 tab switch whooshes (sine sweep 200→100 Hz, 250ms each)
- 1 habit check confirm chord (C5-E5-G5 major triad, 400ms)
- 1 seal modal shimmer chord (E5-B5-E6-G6, 800ms with fast-attack slow-decay envelope)
- 1 seal dismiss pop (400 Hz, 100ms)
- 1 plus menu pop (320 Hz, 120ms)
- 1 brand card impact (low sine 80 Hz + definition click, 600ms)

Final mix: 48kHz stereo, mean -16.8 dB, peak -1.1 dB (no clipping).

## How it was made

1. **Recon** (`scripts/dayflow_recon.js`): loaded the source HTML, clicked through all 4 tabs + the + menu, screenshotted each. VLM-analyzed the screenshots to identify the strongest hero shot (Today view, due to night card's depth and completeness).

2. **Injection** (`scripts/dayflow_demo_inject.py`): inserted a `<style>` + `<script>` block before `</body>` that:
   - Dynamically wraps `#st` in a `#camera` div (so we can zoom/pan the content area without affecting the bottom nav pill)
   - Adds 7 camera-position CSS classes (`.zoom-today-hero`, `.zoom-habits-hero`, etc.) with `cubic-bezier(0.32, 0.72, 0, 1)` spring transitions
   - Adds a vignette overlay (radial gradient, fades in at t=0.6)
   - Adds a black fade-overlay for intro/outro
   - Adds a brand-card overlay ("Dayflow" + tagline "a day, in motion.") that fades in at t=23.2
   - Runs a choreography timeline that toggles camera classes + triggers the source app's real interactions (tab clicks via `button.tab[data-t="N"]`, habit check via `.ck`, plus menu via `#plus`, seal modal dismiss via `#sm.classList.remove('on')`)

3. **Capture** (`scripts/dayflow_demo_capture.js`): used Playwright's `recordVideo` at 1080×1920 (viewport 540×960 + deviceScaleFactor 2 + recordVideo.size 1080×1920) for 25.5s of real-time playback. Captured the real CSS transitions + the source app's real interaction animations (tab pill slide, habit check draw, seal modal shimmer, plus menu slide-up).

4. **Encode**: trimmed the webm to 24.0s + converted to 30fps mp4 (frame duplication from 25fps source) with libx264 + AAC.

5. **Audio** (`scripts/dayflow_demo_audio.py`): synthesized the cinematic music + SFX with numpy + scipy, mixed to a single 24.0s 48kHz stereo track.

6. **Mux**: combined video + audio with ffmpeg, applying a `vignette=PI/5` filter for cinematic depth.

7. **Poster**: extracted the frame at t=11.0s — the moment of the habit check, when the camera is zoomed into the habit rows and the check animation is playing. Strongest single-frame "postable" moment.

## Centering (addressing the previous demo's issue)

The previous Log a block demo had the sheet at `place-items: end center` (bottom-anchored), which made it look bottom-heavy. This demo fixes centering by:

- Using the source app's natural full-screen layout (the app already uses `#st { position: fixed; inset: 0; }` minus 92px for the bottom nav)
- Wrapping `#st` in `#camera` with `inset: 0` — so the camera fills the viewport
- All zoom/pan transforms use `transform-origin: 50% 50%` (center) so zoom movements are centered on the focal point
- Camera positions use `translate()` to shift the focal point (e.g., `scale(1.40) translate(0, -10%)` zooms toward the upper portion where the night card lives)

## What's NOT in this demo (could be added in a longer cut)

- Wheel time picker (the Log a block style) — Dayflow's time selection UI
- Chat view (Dayflow has a chat tab for asking about your data)
- Settings view (customization, categories, goals)
- Multiple habit checks (showing 2-3 habit completions in sequence)
- Plus menu item selection (currently just opens the menu, doesn't pick an item)
- Slower / more dramatic camera moves (could push to 1.6x zoom for hero shots)

These could all be added in a 30s or 45s cut.
