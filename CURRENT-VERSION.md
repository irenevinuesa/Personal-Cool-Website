CURRENT STABLE CHECKPOINT
20 September 2026

# Irene Vinuesa website: current stable version

Documentation only. `index.html` is now the REAL and APPROVED homepage; `observatory-test.html` is only a backup/reference copy.
Last edits: `index.html` created 20 Sep 2026, 14:02 (copy of `observatory-test.html` from 13:50, with only the file name updated in its internal links). Section pages updated at the same time to link to `index.html`.

## Project rules (from the owner, always apply)

1. `index.html` is the only *live* site: it is now the approved observatory experience.
2. Never modify `Antiguos/`. Never overwrite or delete previous versions. (Do not delete `observatory-test.html` unless the owner says so.)
3. Explain briefly before a major change. Change only what is asked. Preserve existing functionality.
4. After every change, say exactly which parts of the file were modified.
5. No Git, GitHub, Vercel, npm, frameworks or build tools unless explicitly asked. Keep it a simple static site.
6. Priority: visual quality, interactivity, responsiveness.

## Files in this stable version

Pages (project root, all self-contained: HTML, CSS and JS inline, no libraries):
- `index.html` - THE homepage: the whole observatory -> telescope -> universe experience, HOME + hamburger menu, planet hub
- `about.html`, `experience.html`, `projects.html`, `cool-recs.html`, `in-touch.html` - "WORK IN PROGRESS... :)" placeholders with two links each (see Navigation)
- `observatory-test.html` - backup/reference copy of the same experience. It is identical to `index.html` except that its own HOME / BACK HOME links and comments still say `observatory-test.html`. Nothing links to it any more. Do not edit it; keep it as the safety copy.

Images actually used (all in `Fotos/observatory/`, never modify them):
- `obs-full-plate.png` - 2880x1620 observatory master
- `obs-eyepiece-front.png` - 1672x941, view inside the telescope tube
- `planet-hub.png` - 1536x1024, galaxy + five planets, no text (the file must be named exactly `planet-hub.png`)

Other files (not used by the site): `Antiguos/` (old versions; `Antiguos/index-2.html` is byte-identical to the OLD homepage that `index.html` replaced, so the old homepage is preserved there), `Fotos/observatory/obs-full-plate-1672.png` (backup of the 1672px master), `Fotos/home-observatory-reference.png` (original visual reference), the `ChatGPT Image ...png` files (raw generations), `CURRENT-VERSION.md`.

External: Cormorant Garamond from Google Fonts (needs internet, falls back to Georgia).
Verified when migrating: every local reference (images, the five pages, back links) exists, and no reference to `observatory-test.html` remains in `index.html` or the section pages.

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

Coordinates are pixels of `planet-hub.png` (1536x1024). Each has an invisible hit area and a live-text label; both are real links to the page.

| Planet | Section | Page | Hit area | Label |
|---|---|---|---|---|
| top-left | ABOUT ME | about.html | circle 384,190 r104 | below |
| top-right, ringed | EXPERIENCE | experience.html | ellipse 1158,205 rx172 ry88 | below |
| bottom-left, red | PROJECTS & RESEARCH | projects.html | circle 299,545 r93 | below |
| bottom-centre | COOL RECS | cool-recs.html | circle 749,704 r90 | left of planet |
| bottom-right, blue | IN TOUCH | in-touch.html | circle 1241,604 r97 | below |

Typography (do not change): Cormorant Garamond, uppercase, ivory `#efe4cd`/pale gold `#d6bf88`, wide letter-spacing. Also EXPLORE (top centre), SAME CURIOSITY / A LARGER UNIVERSE + `← BACK HOME` (bottom centre). Hover: faint glow + brighter label + thin gold underline. Press **D** to outline the hit areas.

## Navigation

Three ways to move around; they are deliberately different:

| Control | Where | Goes to |
|---|---|---|
| **HOME** | top-right of `index.html`, always visible, next to the hamburger | `index.html`: the very beginning of the observatory (scroll reset to 0, `#universe` removed from the address, instant) |
| **☰ hamburger** | top-right of `index.html`, next to HOME | opens the menu with the five sections (see below): a direct route to any page, skipping the journey |
| **← BACK HOME** | bottom of the hub (under SAME CURIOSITY / A LARGER UNIVERSE), and on every section page | same as HOME: `index.html`, beginning of the observatory |
| **← BACK TO THE UNIVERSE** | every section page | `index.html#universe`: the settled five-planet hub |

- **BACK TO THE UNIVERSE = the five planets. BACK HOME / HOME = the beginning of the observatory.** They are NOT the same action.
- **`index.html#universe`**: loads directly into the fully settled five-planet hub (the script jumps the scroll to the end and skips smoothing, so no earlier stage plays; `history.scrollRestoration` is set to manual). Also reacts to a `hashchange` to `#universe`. Plain `index.html` always starts at the observatory.
- **HOME / BACK HOME implementation** (`goHome`): intercepts the click, removes the hash with `history.replaceState`, scrolls to 0 and resets the smoothed progress to 0 (no rewinding through the stages). Ctrl/Cmd/Shift-clicks open normally.
- **Hamburger menu**: full-screen dark blurred veil over whatever scene is showing, five links (About me, Experience, Projects & Research, Cool Recs, In Touch) in wide-spaced serif with thin gold hairlines above and below; on hover a small four-point star and a thin gold underline appear. The button turns into an X. It closes with the X, ESC, or a click outside the list; the page underneath cannot scroll while it is open. Links are only tabbable while open.
- **Normal journey**: observatory -> telescope -> universe -> click a planet or label -> section page -> BACK TO THE UNIVERSE (returns to the hub) or BACK HOME (returns to the start).
- **Recruiter shortcut**: HOME ☰ at any point jumps straight to any section.
- **Section pages** (`about.html` etc.): centred title, `WORK IN PROGRESS... :)`, then `← BACK TO THE UNIVERSE` (`index.html#universe`) and `← BACK HOME` (`index.html`) side by side. Background: a dimmed, blurred copy of `planet-hub.png`. All internal links use `index.html`.

## Debug and testing helpers (all in `index.html`)

- **D** key toggles a readout (progress, phase, scales) and the hit-area outlines. Hit areas are invisible when D is off.
- URL params: `index.html?p=0.9` freezes the approved sequence; `?e=0.5` freezes the telescope-to-universe phase; add `&nodebug` to hide the readout; `&hover=proj` shows a planet's hover state. (These params turn debug on by default.)
- Headless screenshots work with Chrome `--headless=new --virtual-time-budget=9000 --screenshot=...`. Quirks: a top-level `#universe` screenshot can come out black (headless artifact); read animation state carefully, because rAF may not run between virtual-time waits.

## Known limitations / not done yet

- No cinematic zoom-to-planet transition yet (clicking a planet navigates directly).
- Section pages are placeholders only; real content for About, Experience, Projects & Research, Cool Recs and In Touch has not been built.
- Portrait/phone: the whole hub image is shrunk to fit, so planets are small (labels are kept on screen automatically). A portrait version of the hub art would help.
- Performance: the scaled telescope layer is re-drawn each frame and may be heavy on weak GPUs.
- Approved and LOCKED unless the owner asks: observatory look, telescope approach, crossfade into the tube, the telescope-window universe sequence, planet positions/mapping, hub typography, HOME + menu design.
- Deployment: it is a plain static site (open `index.html`); nothing is configured for hosting yet.

## Housekeeping

- Tests run on the migrated `index.html` (headless Chrome): starts at the observatory; `#universe` opens the hub; HOME and BACK HOME reset to the start; hamburger opens and closes (X, ESC, outside click); all five planets and a label open the right page; BACK TO THE UNIVERSE returns to `index.html#universe`; all three images load. The experience is visually unchanged from `observatory-test.html`.
- The owner keeps a backup of this version locally and on GitHub. Do not run Git commands or push unless the owner asks.
- Temporary working backups made during development lived outside the project (session scratchpad) and are not part of this version.
