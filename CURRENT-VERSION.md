CURRENT STABLE CHECKPOINT
20 September 2026

# Irene Vinuesa website: current stable version

Documentation only. Nothing in the website was changed to write this file.
Last edit to `observatory-test.html`: 20 Sep 2026, 13:50. Section pages: 13:30.

## Project rules (from the owner, always apply)

1. `index.html` is the only *live* site. It is still the OLD site and has NOT been touched. The new prototype is `observatory-test.html`.
2. Never modify `Antiguos/`. Never overwrite or delete previous versions.
3. Explain briefly before a major change. Change only what is asked. Preserve existing functionality.
4. After every change, say exactly which parts of the file were modified.
5. No Git, GitHub, Vercel, npm, frameworks or build tools unless explicitly asked. Keep it a simple static site.
6. Priority: visual quality, interactivity, responsiveness.

## Files in this stable version

Pages (project root):
- `observatory-test.html` - the main prototype (everything is inline: HTML, CSS, JS, no libraries)
- `about.html`, `experience.html`, `projects.html`, `cool-recs.html`, `in-touch.html` - "WORK IN PROGRESS... :)" placeholders

Images actually used (all in `Fotos/observatory/`, never modify them):
- `obs-full-plate.png` - 2880x1620 observatory master
- `obs-eyepiece-front.png` - 1672x941, view inside the telescope tube
- `planet-hub.png` - 1536x1024, galaxy + five planets, no text

Other files (not used by the prototype): `index.html` (old live site), `Antiguos/` (old versions), `Fotos/observatory/obs-full-plate-1672.png` (backup of the 1672px master), `Fotos/home-observatory-reference.png` (original visual reference), the `ChatGPT Image ...png` files (raw generations), `CURRENT-VERSION.md`.

External: Cormorant Garamond from Google Fonts (needs internet, falls back to Georgia).
Verified: every local reference (images, the five pages, back links) exists.

## The sequence (one scroll-driven page, 1300vh tall, fully reversible)

The camera is a function of scroll only (no autoplay). Total scroll is split: the first 600vh drive the approved observatory/telescope sequence (progress `p` 0..1), the remaining scroll drives the telescope-to-universe phase (progress `e` 0..1).

1. Observatory (p=0): `obs-full-plate.png` fills the screen. Live text: IRENE VINUESA, Finance · Markets · Mathematics · Technology, LOOK THROUGH THE TELESCOPE. Gentle candle glows and dust.
2. Approach (p 0-0.70): the image scales up to about 13x aimed at the eyepiece (40% / 46% of the image), with growing darkness, soft blur, fading text.
3. Alignment (0.70-0.82) and crossfade (0.82-0.96): the camera reaches the eyepiece, slides right/forward along the tube, then `obs-eyepiece-front.png` emerges from darkness. Approved, do not retune.
4. Inside the telescope (p=1, e=0): the brass tube around us. **`planet-hub.png` is already visible inside the glass opening** (a circular mask over the eyepiece image, see below), so the universe is seen through the telescope. No labels yet.
5. Through the telescope (e 0.08-0.78): the camera moves forward; the whole telescope container scales from 1.12x to about 2.9x and the opening widens up to 60%, until the brass leaves the screen and the hub image sits at its final size/position. There is NO image swap or crossfade here.
6. Settle (e 0.78-0.88), then labels (about 0.88-0.98: labels one by one, EXPLORE ~0.92, footer ~0.94; clickable after 0.96).

## How the telescope window works (do not break)

- `#eye` (container, same size as the cover-fitted image) holds `#eyeImg` and `#eyeWin`; `#eyeWin` holds `#hubImg` (planet-hub.png) and is clipped by a CSS radial mask centred on the lens (`CFG.lens` = 0.501, 0.464; radius `CFG.glassR` = 0.14 of image width x 0.97, growing by `EYE_GROW` = 0.6).
- `layoutEye()` computes the end camera scale `eyeSEnd` so the opening covers the viewport, and sets the hub image scale `eyeSH = hubSF / eyeSEnd`, so at the end the image is exactly at its final position (`hubOX`, `hubOY`, `hubSF`). The labels/hit areas are a separate layer (`#hub` > `#hubStage`) laid out at that same final position. If you change one, keep the other consistent.
- `#eye` has NO `will-change` on purpose (so it re-rasterises sharply while scaling). `#cam` (observatory) keeps its `will-change` (approved softness).
- The crossfade blur/dim filter is applied to `#eye` (so the hub inside gets it too).
- planet-hub.png is never enlarged beyond its final on-screen scale.

## Five planets (mapping is final)

Coordinates are pixels of `planet-hub.png` (1536x1024). Each has an invisible hit area and a live-text label; both link to the page.

| Planet | Section | Page | Hit area | Label |
|---|---|---|---|---|
| top-left | ABOUT ME | about.html | circle 384,190 r104 | below |
| top-right, ringed | EXPERIENCE | experience.html | ellipse 1158,205 rx172 ry88 | below |
| bottom-left, red | PROJECTS & RESEARCH | projects.html | circle 299,545 r93 | below |
| bottom-centre | COOL RECS | cool-recs.html | circle 749,704 r90 | left of planet |
| bottom-right, blue | IN TOUCH | in-touch.html | circle 1241,604 r97 | below |

Typography (do not change): Cormorant Garamond, uppercase, ivory `#efe4cd`/pale gold `#d6bf88`, wide letter-spacing. Also EXPLORE (top centre), SAME CURIOSITY / A LARGER UNIVERSE + `← BACK HOME` (bottom centre). Hover: faint glow + brighter label + thin gold underline. Press **D** to outline the hit areas.

## Navigation (three levels)

- **HOME** (top-right, next to the hamburger, always visible): resets instantly to the very beginning of the observatory (scroll 0, `#universe` removed).
- **☰ menu**: full-screen dark blurred veil, five links (About me, Experience, Projects & Research, Cool Recs, In Touch), gold hairlines, star + underline on hover. The button becomes an X. Closes with X, ESC, or a click outside the list.
- **`observatory-test.html#universe`**: loads directly into the settled five-planet hub (jumps scroll to the end, no earlier stage plays; `history.scrollRestoration` is set to manual).
- **Section pages** each have `← BACK TO THE UNIVERSE` (`observatory-test.html#universe`) and `← BACK HOME` (`observatory-test.html`, start of the observatory).
- **`← BACK HOME` on the hub** (under the footer): same as HOME.

## Debug and testing helpers

- **D** key toggles a readout (progress, phase, scales) and the hit-area outlines.
- URL params: `?p=0.9` freezes the approved sequence; `?e=0.5` freezes the telescope-to-universe phase; add `&nodebug` to hide the readout; `&hover=proj` shows a planet's hover state.
- Headless screenshots work with Chrome `--headless=new --virtual-time-budget=9000 --screenshot=...`. Quirks: a top-level `#universe` screenshot can come out black (headless artifact); read animation state carefully, because rAF may not run between virtual-time waits.

## Known limitations / not done yet

- No cinematic zoom-to-planet transition yet (clicking a planet navigates directly).
- Section pages are placeholders only. `index.html` has not been replaced.
- Portrait/phone: the whole hub image is shrunk to fit, so planets are small (labels are kept on screen automatically). A portrait version of the hub art would help.
- Performance: the scaled telescope layer is re-drawn each frame and may be heavy on weak GPUs.
- Approved and LOCKED unless the owner asks: observatory look, telescope approach, crossfade into the tube, planet positions/mapping, hub typography, HOME + menu design.

## Housekeeping

- No Git commands were run for this checkpoint. A `.git` folder exists in the project root; the owner has not asked for Git to be used.
- Temporary backups made during development lived outside the project (session scratchpad) and are not part of this version. To keep an exact copy, duplicate the files listed above.
