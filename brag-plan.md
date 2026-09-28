# brag-plan.md — focus triad.

> Second `/brag-slim` run. Same creative playbook (no Hyperframes; built entirely on-machine with FFmpeg + Playwright). Voiceover is OFF this time per user direction.

## 1. What is it

**focus triad.** — a tracker. for your day.

Built on top of the real **dayflow-web** project (https://github.com/Mohamedkhaled420/dayflow-web). The user rebranded it as "Focus Triad" for this launch — the brand mark in all video scenes is `focus triad.` (lowercase, period in cream), but the UI shown is dayflow-web's actual design: periwinkle window, cream glass cards, charcoal CTAs, Nunito, real category colors.

## 2. Source material (extracted from the repo)

I read these files from the actual repo:
- `README.md` — full product description (6 views, real category list, mock-data-first privacy claim, Supabase-ready architecture, BYO AI keys)
- `package.json` — confirms Next.js 16 + Tailwind 4 + Radix UI + motion + zustand
- `src/app/globals.css` — design-system layer (.df-material, .df-dock, springs-not-durations, glass backdrop-filter recipe)
- `src/styles/theme.css` — exact color tokens (Lively Pastel revamp, 2026-09)

**Exact tokens used in the video:**

| Token | Value | Where it's used |
|---|---|---|
| `--df-window-bg` (light) | `#A5B4FC` | periwinkle window bg for UI scenes |
| `--card` (light) | `#FFFBF5` | cream glass cards |
| `--foreground` (light) | `#1E293B` | primary ink on light bg |
| `--muted-foreground` | `#3F4668` | secondary ink |
| `--primary` (CTA) | `#1C1917` | charcoal — punchline bg + brand mark |
| `--border` (translucent) | `rgba(255,255,255,0.55)` | card edges |
| `--color-accent-focus` | `#58A6FF` | Work category |
| `--color-accent-craft` | `#BC8CFF` | Personal category |
| `--color-accent-fitness` | `#3FB950` | Movement category |
| `--color-accent-recovery` | `#F0883E` | Sleep category |
| `--color-accent-hydration` | `#38BDF8` | Water category |
| `--font-nunito` | Nunito (Google Fonts) | all body + brand |
| Motion | `cubic-bezier(0.32, 0.72, 0, 1)` | critical-damped spring — replaces the previous cubic-bezier(.2,.7,.2,1) |
| Panel radius | 24px | card radius |
| Pill radius | 9999px | CTAs / chips / habit dots |

Glass recipe (faithful port from `.df-material`):
```css
background: rgba(255, 251, 245, 0.78);
-webkit-backdrop-filter: blur(24px) saturate(180%);
backdrop-filter: blur(24px) saturate(180%);
box-shadow: inset 0 0.5px 0 rgba(255,255,255,0.9),
            0 12px 32px -8px rgba(30, 27, 59, 0.18);
border: 0.5px solid rgba(255, 255, 255, 0.55);
```

## 3. Who it's for / what it does for them

For people who want to track the things that make up a day — workouts, work, sleep, water, meals, personal projects — without their data leaving their browser. The README's privacy claim is real and worth leading with: mock data persisted to localStorage now, Supabase-ready later, BYO AI keys.

## 4. What sets it apart

Three real differentiators (not invented):
- The Timeline view — 24-hour proportional blocks with hydration markers, a live now-line, category filters, day/week navigation
- Privacy-first — data stays in your browser by default
- Six tracker categories, distilled from the source's `theme.css` semantic accents

## 5. Most impressive / funniest claim

"Three things you care about. We track three more." — the parody is that the brand is called "Focus Triad" but the source app actually tracks 6 categories. We honor that absurdity deadpan.

## 6. Visual hook

Pure charcoal (#1C1917). Cream (#FFFBF5) lowercase text fades up center: **you have a day.** Two seconds of nothing. Hard cut.

## 7. Real UI / flow to show (per Show-the-thing law — these are real source UI, not invented)

1. **Timeline view** — a vertical 24-hour proportional timeline with colored blocks (Movement green, Work blue, Personal purple, Sleep orange, Water cyan dots as hydration markers) + a "now" line. Caption: "It shows your day. As blocks."
2. **Habits view with streaks** — habit rows with 7-day met/unmet dot grid (filled pastel, empty cream-stroke), flame icon next to current streak count. Caption: "Streaks. With flames." Subline: "(the flames are the point.)"
3. **Weekly Donut** — donut chart with 5 category segments (the real category colors), legend below. Caption: "And the week. As a donut."

All three are faithful recreations of the actual views documented in the repo's README.

## 8. Tone

`yc-parody` (carried over from the previous run, which the user said "nice" to) — deadpan 2016-era Series A startup energy, played completely straight.
- Hard cuts between scenes
- Lowercase type, period in the brand mark (cream-colored period)
- No exclamation marks anywhere. Ever.
- Nunito at weight 800 for the brand mark, weight 600 for captions, weight 500 for body
- Spring easing `cubic-bezier(0.32, 0.72, 0, 1)` for everything that moves (honors the source's "springs, not durations" rule)

## 9. One-line share caption

> focus triad. three things you care about. we track three more. now in private beta. your day stays yours.

## 10. Storyboard (scene-by-scene)

Total target: **~18s** at 30fps = ~540 frames. Square 1080×1080.

| # | Scene | Duration | Frames | Content | SFX |
|---|---|---|---|---|---|
| 1 | Hook | 0.0–2.5s | 0–74 | Charcoal bg. Cream text `you have a day.` fades up at 0.6s, settles, holds. | soft click at cut-in |
| 2 | Reveal | 2.5–5.5s | 75–164 | Hard cut to charcoal. `focus triad.` brand mark fades up large (weight 800, period in cream #FFFBF5). Below: `A TRACKER. FOR YOUR DAY.` small caps. | soft click |
| 3 | Timeline | 5.5–9.0s | 165–269 | Hard cut to periwinkle bg. Glass cream panel containing a 24h vertical timeline. 5 colored blocks (green/blue/purple/orange + a tall sleep block at the bottom), hydration cyan dots scattered, a diagonal "now" line crossing mid-block. Caption above the panel: `It shows your day. As blocks.` Blocks slide in one-by-one with spring easing. | 5 spring ticks (one per block) |
| 4 | Streaks | 9.0–12.0s | 270–359 | Hard cut to periwinkle bg. Glass cream panel with 4 habit rows: goal name + 7-day dot grid (4 filled, 3 empty) + flame icon + streak count. Caption: `Streaks. With flames.` Subline: `(the flames are the point.)` Rows slide in staggered. | 4 spring ticks |
| 5 | Donut | 12.0–15.0s | 360–449 | Hard cut to periwinkle bg. Glass cream panel with a donut chart — 5 segments in the real category colors (cyan + green + blue + purple + orange) + legend dots+labels below. Donut draws itself with `stroke-dasharray` animation. Caption: `And the week. As a donut.` | pencil-draw tick as donut draws |
| 6 | Punchline | 15.0–18.0s | 450–539 | Hard cut to charcoal. `focus triad.` brand mark. Below: `Three things you care about.` Subline: `We track three more.` Then smaller line: `Now in private beta. Your day stays yours.` | final soft click, then nothing |

Durations sum: 2.5 + 3.0 + 3.5 + 3.0 + 3.0 + 3.0 = **18.0s**. ✓

## 11. Voiceover

**Off.** Per user direction. The mix is music + SFX only this time.

## 12. Music + SFX mix (no VO duck needed this time)

- **Music**: same A-minor pad (A2 + E3 + A3 + C4 sines, low-passed 800 Hz, 0.3 Hz tremolo). Slightly lower gain (-16 dB) since no VO to duck under.
- **SFX**:
  - 6 soft clicks at hard-cut timecodes (0.0, 2.5, 5.5, 9.0, 12.0, 15.0)
  - 5 spring ticks during scene 3's block-stagger (5.8, 6.0, 6.2, 6.4, 6.6s)
  - 4 spring ticks during scene 4's row-stagger (9.4, 9.6, 9.8, 10.0s)
  - 1 pencil-draw tick during scene 5's donut draw (12.4–14.0s, 80ms spacing)
- **Mix**: music at -16 dB, SFX at -22 dB. No sidechain duck (no VO).

## 13. Output deliverables

```
brag-output-2026-09-28-235542/
├── brag-plan.md            ← this file
├── brag.mp4                ← final video, 18s, 1080×1080, 30fps, music + SFX only
├── brag.jpg                ← poster (frame 535, fully-settled punchline)
├── share-copy.txt
└── work/
    ├── scenes/scene1.html..scene6.html
    ├── frames/f0000.png..f0539.png
    ├── audio/{music.wav, sfx.wav, mix.wav}
    └── verify/
```

## 14. Creative laws checklist

- [x] **Short** — 18s, inside the 15-25s envelope
- [x] **Clear to a stranger** — by the end you know: it's a tracker called `focus triad.`, it tracks the parts of a day, in private beta, your data stays yours
- [x] **The hook is everything** — first 2s = pure charcoal + lowercase claim, forces attention
- [x] **Show the thing** — scenes 3/4/5 show actual UI views from dayflow-web (Timeline, Habits, Donut), faithfully recreated with the source's real tokens. No invented metrics, no fake testimonials. The habit "streak counts" shown are abstract dots (no specific numbers).
- [x] **Specific** — every line is in `focus triad.`'s own deadpan register; uses real claims from the source ("your day stays yours" maps to the README's "nothing leaves your browser")
- [x] **Readable** — every text line settles ≥1.2s; block/row staggers are 200ms each, fully visible
- [x] **Make it alive** — timeline blocks slide in one-by-one, habit rows stagger, donut draws itself with stroke-dashoffset
- [x] **Funny earns its place** — "three things you care about. we track three more." humor comes from the brand-name absurdity (triad implies 3, app tracks 6), not from jokes
- [x] **Every frame postable** — every scene is a centered composition with the brand mark visible (corner mark) and faithful source-design aesthetics

## 15. What's different from the previous brag run

| Aspect | Previous (tracked.) | This (focus triad.) |
|---|---|---|
| Source | An idea in text (invented UI) | Real repo at github.com/Mohamedkhaled420/dayflow-web |
| Brand | tracked. (lowercase + green dot) | focus triad. (lowercase + cream dot) |
| Brand font | Inter 700 | Nunito 800 (source's actual font) |
| Bg color | pure black + pure white | #1C1917 charcoal + #A5B4FC periwinkle (source's actual colors) |
| Card color | white | #FFFBF5 cream glass (source's actual card) |
| Easing | `cubic-bezier(.2,.7,.2,1)` | `cubic-bezier(0.32, 0.72, 0, 1)` (source's spring token) |
| Accent | generic yc green #00C805 | 5 real category accents from `theme.css` |
| VO | On (jam voice, 5 lines) | Off (per user) |
| Music gain | -15 dB | -16 dB (no VO to duck under) |
| Punchline claim | "Backed by people you've heard of." | "Your day stays yours." (real source claim) |
| Triad joke | n/a | "Three things you care about. We track three more." — leverages brand name vs real category count mismatch |
