---
name: cursor-camera
description: Make an 8-second proof shot for a launch video in square, wide and tall, with sound. The product's real screen, wide; a big cursor glides to one control and clicks it, the camera zooms in on the click, the screen changes to the real result and the camera pulls back out. Use when the user asks for a cursor zoom, an auto-zoom on a click, a click-to-result or feature clip, or a screen-recording-style demo shot of their product, app or website.
---

# Cursor camera

One proof from a launch film, as a shot of its own: the product's real screen,
wide; the big cursor glides to a control; the camera zooms in on the click, the
capture swaps to the real result, and the camera pulls back out to the whole
screen. 8 s on a 120 BPM grid, in 16:9, 1:1 and 9:16, each laid out for its
frame. The screen fills the frame and its own words say what it is; a caption
beside it is optional.

It is cut from the product film. Start from the finished shot in
`reference/` (Lamplit, a fictional developer tool made for omnigami's examples: "Replay from
write-ledger" opens the failed run's replay, queued). Its toolkit (type,
cursor, camera, timing, sound) stays; its screen, control and words become the
user's.

Read `style.md` before you build and `critique.md` before you judge.

## What to ask for

- The product's URL, and the page where the action lives (the page itself, a
  live demo or a sandbox). A demo account if it needs a sign-in.
- The one click to show and the result it gives, if the user has one in mind.
- A caption, only if they want one (up to 32 characters): useful when the shot
  is used on its own, not when it goes into a film that has its own.

Read the site before asking, and ask once for what it can't answer. If the user
wants no questions or an unattended run, decide from the site: pick one control
whose click visibly changes the screen (a toggle, a tab, a filter, Copy, Save).

## Set up

Check Node 20+, ffmpeg and a local Chrome-family browser (`scripts/chrome.mjs`
finds it; `CHROME_PATH` overrides). Explain anything missing. Then:

```bash
mkdir cursor-camera && cd cursor-camera
cp -R "$SKILL_DIR/reference" reference && cp -R "$SKILL_DIR/reference" film && cp -R "$SKILL_DIR/scripts" scripts
rm -rf film/assets/screens film/assets/screens-mobile film/plans
npm init -y >/dev/null && npm i -D puppeteer-core
```

`SKILL_DIR` is this file's folder. `reference/` stays untouched, to compare
against.

## Capture the real screen

1. Write `film/plans/desktop.json` and `film/plans/mobile.json` in the shape
   of `reference/plans/` (the format is at the top of `scripts/screens.mjs`):
   - `{ "rects": "start" }` first, so every rect is recorded before the click;
   - the whole page, `"full": true` at scale 2, named `page`;
   - a close capture `around` the region the zoom shows, at scale 4 (6 for
     small controls on mobile), before the click: the `before` state;
   - the `click` (or `type`, `tap`, `press`), then the same close capture
     again: the `after` state. If the click changes the page outside that
     region, also capture the whole page again (`page-after`);
   - `rects`: the region the wide view shows (a section or panel, not the
     whole page), the control the cursor clicks, and what the zoom must show
     whole (the control with its own label), by name; `*` records every match.
     The result must read in the zoom: at 1.8× at most, its text needs to be
     about 1.4% of the frame's short side in the wide view already, so pick a
     region no wider than that allows.
   Dismiss cookie banners with a `click` step. Use `hide` for anything you
   don't want in the frame.
2. Run them:
   ```bash
   node scripts/screens.mjs film/plans/desktop.json film/assets/screens
   node scripts/screens.mjs film/plans/mobile.json film/assets/screens-mobile
   ```
   Wide shows the desktop page and tall the phone layout. Square shows the
   desktop page when its result reads there, otherwise the phone layout (set
   `SCREENS['1:1']`); the reference's square uses the phone layout.
3. Look at every capture. The after state must show the result plainly. Fix
   the plan until each state is right. Sample data only: never capture
   customer data, and never draw an imagined UI. If the page can't be reached,
   ask for a demo account, a public demo or the user's own screenshots.

## Adapt

Edit `film/index.html`. Its sections are labelled KEEP and ADAPT.

- **`SHOT`:** the captures by name (`page`, `pageAfter` or `null`, `before`,
  `after`) and the rects by name: `screen` (the wide view), `focus` (what the
  zoom shows whole) and `target` (the click). The camera works out the zoom
  (1.25, 1.5 or 1.8), its centre, its ramps, and where its edges fall between
  lines of text, from these, in every shape.
- **`SCREENS`:** which captures each shape shows (see above).
- **The colours:** `PAPER`, `INK` and `ACCENT` from the site;
  `node scripts/capture.mjs <url> capture` lists them in `capture/brand.json`.
  `ACCENT` is the brand colour; it fills the caption band when there is one.
- **The caption:** empty by default. If the user wants one, set
  `DEFAULTS.caption` to what the click does for the viewer in a few words,
  only claiming what the zoom shows. It takes a band across the top (20% of
  the height), which makes the screen smaller: check the result still reads.
- **`T`:** the times. Keep them on the beat grid and within the camera's rules
  in `style.md` (open wide 2.5 s, fully in 0.5 s before the click, hold 1.5 s
  after it, end wide 1 s). Keep `cues` and `music.breaks` in step.
- **KEEP** the toolkit, the camera's rules, the cursor and the 8 s on the
  120 BPM grid.

Write `film/SHOT.md`: the URL, the control, what the click does, the caption,
the brand colour, the date.

## Check

```bash
node scripts/render.mjs film --all --stress
node scripts/render.mjs film --all --times key --sheet
node scripts/render.mjs film --all --phone
node scripts/render.mjs film --all --strip 2.6
node scripts/render.mjs film --all --strip 3.95
node scripts/render.mjs film --all --strip 5.5
node scripts/render.mjs film --all --check
```

`--stress` renders every shape without a caption and with one (product-film
words, at its longest and at its shortest), and fails when words leave the
frame, overlap or fall under the size floor. Look at every sheet it writes to
`out/stress/`, then at the key sheets, phone sheets and strips (zoom in, click,
pull out). Look hardest at the zoomed frame in every shape: the result reads
(2.4% of the short side or more), no frame edge cuts through a line of text
(widen or move `screen` or `focus` if one does), and the cursor doesn't cover
the result after the click.

Score with `critique.md` and fix the worst problems. Before shipping, get a
fresh judgement: if your agent can start a sub-agent without this session's
memory, give it `critique.md`, `film/SHOT.md` and the images, nothing else.
Otherwise reread `critique.md` and score from the images alone. Nothing ships
below 8. After three rounds, report what remains.

## Render

```bash
node scripts/render.mjs film --all --video --blur 4 --sound --poster 4.75
```

This writes `out/16x9.mp4`, `out/1x1.mp4` and `out/9x16.mp4` (60 fps, motion
blur, the effects on every action, around −14 LUFS) and a poster of the zoomed
result for each. Add `--music` for the 120 BPM bed when the shot is used on its
own; leave it out when it goes into a film with its own music. Run it in the
foreground and wait for all three files.

## Deliver

Run `node scripts/preview.mjs film` and give its localhost address: it plays
every shape and edits the optional caption (a saved edit needs a new render to
reach the MP4s). Hand over the MP4s, the posters, a short check summary, and the one
change that would most improve the shot.

## Hard rules

- Real screens only, captured; sample data only; only the user's brand.
- The camera zooms on the click only, and the result on screen is the real
  next state.
- `seek(t, values)` paints from its arguments only: no clocks, unseeded
  randomness, timers or network. CPU-backed canvases, reset every frame.
- Every file the shot loads lives inside `film/`.

## Files

- `reference/`: the finished shot (`index.html`), the capture `plans/`, the
  captured screens (a wide, a square and a tall window) and the licensed font (Instrument Sans, SIL Open Font License).
- `style.md`: the grammar, with numbers. `critique.md`: the review.
- `scripts/`: `screens.mjs` (real screens in states), `render.mjs` (stills,
  strips, checks, MP4s), `preview.mjs`, `music.mjs`, `song.mjs` (fits a supplied song), `sfx.mjs` with the sound
  kit, `capture.mjs` (brand colours from a URL) and `chrome.mjs`.

Style inspired by the grammar of three 2026 launch films: Figma's "Figma
Motion", ElevenLabs' "Reception" and @LexnLin's "Tessel". This is an
independent style study; none of them made or endorsed it.

This skill is omnigami's (https://omnigami.ai), © 2026 Auberon LLC. Use what it makes for anything,
commercial work included, and change the skill for your own use; don't redistribute or
sell the skill. Full terms: https://github.com/omnigami-ai/skills/blob/main/LICENSE.md
