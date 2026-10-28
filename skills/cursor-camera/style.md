# Cursor camera: style

A short demo where the cursor is the star: one real task done through the
product's real screens the way a person does it, with a camera the cursor
carries. The cursor glides between targets on gentle arcs, lights what it
hovers, presses on the beat, scrolls, drags a selection; the camera pushes in
as it sets off for a target and pulls back when a page changes. Take the
grammar, never the content.

## Format

- 18 s, nine bars of 120 BPM: a beat is 0.5 s, a bar 2 s. Presses fall on
  beats; the result lands on a downbeat (bar 7, 14 s).
- 60 fps, rendered with motion blur (`--blur 4`). Choreography is timed in
  steps of 1/12 s (`F`): a press lasts two steps.
- Three shapes, each laid out for its frame: 16:9 (1920 × 1080), 1:1
  (1440 × 1440), 9:16 (1080 × 1920). Wide shows the desktop window (1440 × 900);
  square and tall show the product in a window of their own proportions (its
  phone layout, or, for a desktop product, the window at 1080 × 1080 and
  1080 × 1920, as the reference's Lamplit), never a desktop page shrunk. The
  camera never shows past the window's edges: no empty band.
- The screens fill the frame. The product's own words say what it is.

## The task

Four to six actions in the product's own order, each on its own beat, ending on
a result the viewer can see: open something, look into it, act on it, see it
work. At least one action shows each of the cursor's moves: a click that opens
a page, a scroll, a drag (a selection, a slider, a reorder: whatever the
product has), a button that changes state. Real screens for every state,
captured; the app's own hover states, captured too.

## The shot (the reference: Lamplit replays a failed run)

| Time | Grid | What happens |
|---|---|---|
| 0–0.35 | | The Runs page, wide and still. A clean first frame, no cursor. |
| 0.35–0.75 | | The cursor fades in at rest over the run table (and grows from 92% to full size): never sliding in half off the frame. |
| 1.0–2.0 | bar 0, beat 2 | It glides on an arc to the failed run, sync-invoices #4,812; the camera pushes in with it (one move). The row lights with the app's hover. |
| 2.5 | bar 1, beat 1 | Press (after a 0.5 s hover): the row lights a touch and the cursor dips. From 2.55 the run's page arrives: the old page lifts out over 5 frames while the new one's parts rise in, a frame apart, from where the click was outward. |
| 2.6–3.5 | | The camera pulls back to the run's page whole (front-loaded). |
| 3.5–4.0 | | A beat on the new page. |
| 4.0–5.0 | bar 2 | To the logs; the camera pushes in on them with it. |
| 5.0–6.0 | bar 2, beat 2 | A scroll: the lines coast up to the end of the log (quick, then slowing), and the camera rides it, drifting up a third as far. (Only where the window's logs overflow: in square and tall they're whole, and the camera simply holds.) |
| 6.0–6.5 | | A beat to find the error. |
| 6.5–7.0 | bar 3, beat 1 | The cursor moves to the start of the error, the camera closing in with it. |
| 7.5–8.25 | bar 3, beat 3 | Press and drag: "Error: ledger timeout after 30000ms" is selected a character at a time as the cursor crosses it (the app's own selection colour); the cursor stays down (84%) while it drags. |
| 8.25–9.5 | | The selection holds to be read (five words, 1.25 s). |
| 9.5–10.5 | bar 4, beat 3 | Up to "Replay from write-ledger" on a long arc, the camera carried with it to the header. The button lights with the app's hover. |
| 11.0 | bar 5, beat 2 | Press (after a 0.5 s hover): the button sinks 5% and darkens. From 11.05 the replay's page arrives, queued. |
| 12.0–12.6 | bar 6 | After a beat, across the header to the status pill, the camera shifting with it. |
| 13.0 | bar 6, beat 2 | Press (0.4 s hover): the pill refreshes the status: running. The pill and everything after it in the header, and the outcome line, roll over (old up and out, new up and in); the rest eases across in 8 frames. The cursor steps off; the camera eases out to show the running bar. |
| 14.0 | bar 7 | It succeeds by itself (the product's own work: nothing waits before it): green, rolling over the same way. |
| 14.1–15.0 | | The camera pulls back to the whole page; the cursor moves aside, clear of the result. |
| 15.0–18.0 | | The result, still. |

**Pauses** (the founder's pause rule, 2026-10-22). The cursor hovers about
0.45 s on everything it presses; after a big move (a page change, a scroll) the
screen holds a beat before the cursor sets off again; what the viewer must read
(the selected error) holds at about a quarter second a word; the product's own
work (queued, running) doesn't wait; nothing is still for more than about 3 s.
Holds are simply still: no slow push between moves (it reads as pulsing).

## The camera

- **Carried by the cursor.** Every camera move starts with a cursor move and
  lasts as long, on the same ease, so the frame and the cursor arrive together.
  It never moves on its own except to pull back after a page changes, to ride a
  scroll, and to show the result.
- **Views:** wide (the window covering the frame, from its top, so the app's
  own bar is whole) and zoom (a box of the page, whole with 4% to spare: the
  row and its neighbours, the logs, the error line, the header). A zoom never
  goes past the captures' scale × 1.15 (sharp), never below wide, and never
  shows past the window.
- **Edges in gaps.** Every settled view moves (up to 10%) and scales (up to 4%)
  so its edges fall between lines of text, never through words.
- **Eases.** Moves start straight off (speed rising over the first tenth, never
  a jolt) and settle on a long tail: `glide` for pushes and the cursor,
  `pull` (a longer tail) for pull backs, `fling` for a scroll. Scale moves in
  log space.

## The cursor

A black arrow with a white outline (4.5 px at 53 px tall) and a soft shadow.
9.5% of the frame's short side in the wide view, growing to 12% at the
sharpest zoom. It tilts toward where it's going (rest −8°, up to ±16°) and
glides on gentle arcs (the path bows by about a tenth of its length), fast
first with a soft landing. It enters by fading in at rest, never from half off
the frame, and every target keeps it whole in the frame. On a press it shrinks
to 84% for two steps; on a drag it stays down. It never rests on the result.

## The app's own motion

- **Hovers** are the app's: its `:hover` styles, captured on the element (the
  plan copies each `:hover` rule to a `.hov` class and adds it), easing on in
  0.1 s as the cursor arrives. Where the app has no hover style, nothing lights.
- **Presses** dip on the beat: the pressed thing sinks a few percent and
  lights (on a dark ground) or darkens (a light button), then comes back.
- **A page change:** the old content lifts out (5 frames) as the new arrives,
  part by part, a frame apart, from the click outward (a rise and a fade, 9
  frames): never empty where the eye is, never swapped in one frame.
- **A state change on the same page:** the changed label and its line roll
  over (old up and out, then new up and in); the rest eases across in 8 frames.
- **A scroll** moves the real, whole content (captured in full) inside its
  panel.
- **A selection** grows with the drag a character at a time, from a capture of
  the real selection.

## The caption (optional)

Empty by default. When the shot needs one (used on its own, say), it says what
the task does for the viewer, and takes the product film's caption grammar:

- Beside the screen, never on it: a band across the top, 20% of the height,
  in every shape, in the accent.
- The product's font at 700 (the reference: Instrument Sans), tracking −0.03 em, on the accent band: 5.6% of the short side; line height
  1.08; inset 8% of the short side; wrapped at the width less 1.6 × the inset.
  It only shrinks (5% at a time) when a word or the lines won't fit.
- It lands at 0.5 s, a word a step, each line 3 steps after the last, from
  116% size and soft to set in 0.22 s; words arrive in the accent and cool to
  white over 0.4 s.
- Up to 32 characters. The screen's part of the frame gets smaller, so check
  the zooms still read.

## Colour

Paper (the product's background) behind the page, ink for the cursor, and one
accent, the product's brand colour, for the caption when there is one. The
screens keep their own colours.

## Sound

- A soft `swish` (0.22) as the camera sets off with the cursor (carrying its
  travel); a `click` (0.6) on every press and the drag; a `pop` (0.36) as each
  page or state the press opens arrives; three fading `tick`s as the logs
  scroll; a `chime` (0.5) on the success; a `swish` as the camera pulls back.
- The skill's own song (`music/song.mp3`, crisp, clever electro-pop at 120 BPM),
  landing one hit on the success (14 s in the reference) as its drums stop and
  the rest fades. On the site, the reference plays a cut of another of
  omnigami's songs, landing on the success.
- With `--music`, the synthesised 120 BPM score instead: pad and hats in bar 0,
  the full groove from bar 1 to the success, pad and hats under the result, and
  a break (drums and bass out) in the beat before the main button's press.
- Mastered around −14 LUFS.

The score's sound is `music.style`: here `'synth'`, the default. For the user's product, pick by what it is: `'organic'` for plants, food and drink, and other natural or handmade things; `'synth'` (oscillators, the default) for software and tools; `'felt'` (a sparse felt piano over a sub bass and a light kit) for a quiet, minimal film. In a break (`music.breaks`) the drums, bass and lead stop and the chords play on; the film's name seeds the key (always major), the progressions and the patterns.

## Banned

- A cursor that slides in partly off the frame, jumps, or arrives somewhere it
  then leaves without a reason; a cursor resting on the result.
- A camera move with no cursor move behind it (beyond the pull backs, the
  scroll ride and the result); zooming in and out back to back.
- A press with no hover before it, or a hover that lights something the app
  doesn't.
- A whole capture swapped in one frame; a page left empty while the next
  arrives.
- A zoom past the captures' scale × 1.15; a settled frame edge through a line
  of text; a caption laid over the screen; a desktop page in the tall frame.
- Drawn or imagined UI; customer data.
