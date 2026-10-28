---
name: cursor-camera
description: Make an 18-second cursor-led demo for a launch video in square, wide and tall, with sound. One real task on the product's real screens, the way a person does it: a big cursor glides between targets, hovers, clicks, scrolls and drags a selection, and the camera it carries pushes in and pulls back with it, ending on the real result. Use when the user asks for a cursor zoom, an auto-zoom demo, a screen-recording-style walkthrough or a feature clip of their product, app or website.
---

# Cursor camera

A short demo where the cursor is the star: one real task, done through the
product's real screens the way a person does it. The big cursor glides between
targets on gentle arcs, lights what it hovers, presses on the beat, scrolls and
drags a selection; the camera it carries pushes in as it sets off and pulls
back when a page changes, and the shot ends on the real result. 18 s on a
120 BPM grid, in 16:9, 1:1 and 9:16, each laid out for its frame. The screens
fill the frame and their own words say what they are; a caption beside them is
optional.

Start from the finished shot in `reference/` (Lamplit, a fictional developer
tool made for omnigami's examples: from the Runs page the cursor opens a failed
run, scrolls its logs, selects the error, presses "Replay from write-ledger",
refreshes the replay's status and the replay succeeds). Its toolkit (type,
cursor, camera, the app's own motion, timing, sound) stays; its task, screens
and words become the user's.

Read `style.md` before you build and `critique.md` before you judge.

## What to ask for

- The product's URL, and the page where the action lives (the page itself, a
  live demo or a sandbox). A demo account if it needs a sign-in.
- The task to show (four to six actions ending on a result), if the user has one in mind.
- A caption, only if they want one (up to 32 characters): useful when the shot
  is used on its own, not when it goes into a film that has its own.

Read the site before asking, and ask once for what it can't answer. If the user
wants no questions or an unattended run, decide from the site: pick a task the
product is for, in its own order: open something, look into it (a scroll, a
selection, a filter), act on it (a button that changes state), see it work.

## Set up

Check Node 20+, ffmpeg and a local Chrome-family browser (`scripts/chrome.mjs`
finds it; `CHROME_PATH` overrides). Explain anything missing. Then:

```bash
mkdir cursor-camera && cd cursor-camera
cp -R "$SKILL_DIR/reference" reference && cp -R "$SKILL_DIR/reference" film && cp -R "$SKILL_DIR/scripts" scripts && cp -R "$SKILL_DIR/music" music
rm -rf film/assets/screens film/assets/screens-mobile film/plans
npm init -y >/dev/null && npm i -D puppeteer-core
```

`SKILL_DIR` is this file's folder. `reference/` stays untouched, to compare
against.

## Capture the real screen

1. Write `film/plans/desktop.json`, `film/plans/square.json` and
   `film/plans/tall.json` in the shape of `reference/plans/` (the format is at
   the top of `scripts/screens.mjs`; the three differ only in `viewport`):
   - `init`: the reference's line that copies every `:hover` rule to a `.hov`
     class, so the app's own hover states can be captured;
   - a `tap` on an empty spot first and after every click, so the real mouse
     never leaves a hover in a capture;
   - for every state of the task, its `rects` (by name, the same names in
     every state) and a whole-window capture at scale 2 (`"full": true`);
   - each hover: an `eval` adding `hov` to the element, a capture `around` it,
     an `eval` removing it;
   - a scroll: an `eval` that lets the scrolled panel grow to its whole content,
     a capture `around` it (the strip the film scrolls), then the page restored;
   - a selection: an `eval` wrapping the words in a `[data-sel]` span (it
     doesn't change the layout) and selecting them, a capture of the strip with
     the selection;
   - the clicks themselves (`click`), with a `wait` after each.
   Dismiss cookie banners with a `click` step. Use `hide` for anything you
   don't want in the frame.
2. Run them:
   ```bash
   node scripts/screens.mjs film/plans/desktop.json film/assets/screens
   node scripts/screens.mjs film/plans/square.json film/assets/screens-mobile
   node scripts/screens.mjs film/plans/tall.json film/assets/screens-tall
   ```
3. Look at every capture. Each state must show its change plainly; no capture
   may show a hover or a focus ring the film doesn't want. Sample data only:
   never capture customer data, and never draw an imagined UI. If the page
   can't be reached, ask for a demo account, a public demo or the user's own
   screenshots.

## Adapt

Edit `film/index.html`. Its sections are labelled KEEP and ADAPT.

- **`T`:** the beats, on the grid (see `style.md`): a hover of about 0.45 s
  before every press, a beat after every page change or scroll, reading time
  (a quarter second a word) on anything the viewer must read, no wait on the
  product's own work, nothing still past about 3 s.
- **`PAGES` and `planFor()`:** the states by capture name, the views (wide, or
  a zoom on a box of the page by rect name), the cursor's targets (points from
  the rects) and the two lists that drive the shot: `C` (camera moves) and `K`
  (cursor moves). Every camera move starts with a cursor move and takes its
  time and ease.
- **`scene()`:** which state draws when, with its hovers, presses, scroll and
  selection, and which transition joins two states (`pageChange` for a new
  page, `stateChange` for the same page changing).
- **The colours:** `PAPER`, `INK` and `ACCENT` from the site;
  `node scripts/capture.mjs <url> capture` lists them in `capture/brand.json`.
- **The caption:** empty by default. If the user wants one, set
  `DEFAULTS.caption` to what the task does for the viewer in a few words. It
  takes a band across the top (20% of the height): check the zooms still read.
- **`cues` and `music`:** a sound on every press and arrival, in step with `T`.
- **KEEP** the toolkit, the camera's rules, the cursor, the transitions and the
  120 BPM grid.

Write `film/SHOT.md`: the URL, the task step by step, the caption, the brand
colour, the date.

## Check

```bash
node scripts/render.mjs film --all --stress
node scripts/render.mjs film --all --times key --sheet
node scripts/render.mjs film --all --phone
node scripts/render.mjs film --all --strip 0.3
node scripts/render.mjs film --all --strip 2.45
node scripts/render.mjs film --all --strip 5.0
node scripts/render.mjs film --all --strip 7.45
node scripts/render.mjs film --all --strip 10.95
node scripts/render.mjs film --all --strip 12.95
node scripts/render.mjs film --all --strip 13.95
node scripts/render.mjs film --all --check
```

`--stress` renders every shape without a caption and with one (product-film
words, at its longest and at its shortest), and fails when words leave the
frame, overlap or fall under the size floor. Look at every sheet it writes to
`out/stress/`, then at the key sheets, phone sheets and strips (the cursor's
entrance, every press and the change it makes, the scroll, the drag). Look
hardest at the cursor: it enters whole, never jumps, hovers before every press,
and never covers what the viewer must read. Then the zooms: their text reads,
and no settled edge cuts through a line of text. After the render, run
`node scripts/motion.mjs out/16x9.mp4 <from> <to>` over every camera and cursor
move.

Score with `critique.md` and fix the worst problems. Before shipping, get a
fresh judgement: if your agent can start a sub-agent without this session's
memory, give it `critique.md`, `film/SHOT.md` and the images, nothing else.
Otherwise reread `critique.md` and score from the images alone. Nothing ships
below 8. After three rounds, report what remains.

## Render

```bash
node scripts/render.mjs film --all --video --blur 4 --audio music/song.mp3 --sound --poster 17
```

This writes `out/16x9.mp4`, `out/1x1.mp4` and `out/9x16.mp4` (60 fps, motion
blur, the skill's song and the effects on every action, around −14 LUFS) and a
poster of the result for each. The song (`music/song.mp3`: crisp, clever
electro-pop at 120 BPM, the shot's grid) starts on a bar line and, near the end,
lands one hit on the success, where its drums stop and the rest closes and fades
(from its stems in `music/song-stems/`). `--from <seconds>` starts at another of its distinct 8-bar sections (the song is about two minutes long).
`--music` gives the synthesised 120 BPM score instead; the user's own song works
with `--audio their.wav`. Leave out `--audio` when the shot goes into a film
with its own music: the effects alone. Run it in the foreground and wait for
all three files.

## Deliver

Run `node scripts/preview.mjs film` and give its localhost address: it plays
every shape and edits the optional caption (a saved edit needs a new render to
reach the MP4s). Hand over the MP4s, the posters, a short check summary, and the one
change that would most improve the shot.

## Hard rules

- Real screens only, captured; sample data only; only the user's brand.
- The camera moves with the cursor, and every state on screen is the real
  next state.
- `seek(t, values)` paints from its arguments only: no clocks, unseeded
  randomness, timers or network. CPU-backed canvases, reset every frame.
- Every file the shot loads lives inside `film/`.

## Files

- `reference/`: the finished shot (`index.html`), the capture `plans/`, the
  captured screens (a wide, a square and a tall window: every state, the hover
  states, the scrolled logs whole and the selection) and the licensed font
  (Instrument Sans, SIL Open Font License).
- `style.md`: the grammar, with numbers. `critique.md`: the review.
- `music/`: the skill's song and its stems.
- `scripts/`: `screens.mjs` (real screens in states), `render.mjs` (stills,
  strips, checks, MP4s), `preview.mjs`, `music.mjs`, `song.mjs` (fits a supplied song), `sfx.mjs` with the sound
  kit, `capture.mjs` (brand colours from a URL) and `chrome.mjs`.

This skill is omnigami's (https://omnigami.ai), © 2026 Auberon LLC. Use what it makes for anything,
commercial work included, and change the skill for your own use; don't redistribute or
sell the skill. Full terms: https://github.com/omnigami-ai/skills/blob/main/LICENSE.md
