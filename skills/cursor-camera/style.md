# Cursor camera: style

One proof of the product film as a shot of its own: the real screen wide, the
big cursor, a zoom on the click, the real result, and the pull back out. The
camera follows the cursor and moves only for the click. Take the grammar, never
the content.

## Format

- 8 s, four bars of 120 BPM: a beat is 0.5 s, a bar 2 s. The click lands on a
  downbeat (4.0 s).
- 60 fps, rendered with motion blur (`--blur 4`). Choreography is timed in
  steps of 1/12 s (`F`): a press lasts two steps.
- Three shapes, each laid out for its frame: 16:9 (1920 × 1080), 1:1
  (1440 × 1440), 9:16 (1080 × 1920). Wide shows the desktop page; square and tall
  show the product in a window of their own proportions (its phone layout, or,
  for a desktop product, the page captured at 1080 × 1080 and 1080 × 1920, as
  the reference's Lamplit), never a desktop page shrunk. The camera never shows
  past the page's edges: no empty band above or beside it.
- The screen fills the frame. The product's own words say what it is; the
  result must read in the zoom (2.4% of the short side or more).

## The shot

| Time | Grid | What happens |
|---|---|---|
| 0–1.0 | bar 0, beats 0–1 | The screen, wide and settled. A clean first frame. |
| 1.0–2.0 | beats 2–3 | The cursor comes in from just below the frame's bottom edge (right of the control, 55% of the way to the frame's right edge) and glides 12 steps, fast first (ease-out cubic), to wait beside the control (135% across, 20% down), clear of its label and of the lines around it. |
| 2.5–3.42 | bar 1, beat 1 | Zoom in: an ease in and out, 11 steps for 1.8×. The cursor rides the camera. |
| 3.5–3.83 | beat 3 | The cursor aims: onto the control's lower right (70% across, 72% down), so its label stays in view, arriving two steps before the click. |
| 4.0 | bar 2 | The click: the cursor shrinks to 0.84 for two steps and holds still; the capture swaps to the result 0.05 s after the press. |
| 4.17–4.67 | | The cursor steps off past the control's right edge (112% across, 95% down) so the result reads. |
| 5.5–6.42 | bar 2, beat 3 | Pull back out to the wide view: front-loaded (1 − (1 − p)^3.5), half the zoom in the first fifth. |
| 6.42–8 | bar 3 | Wide, with the result in place. |

The camera breathes during every hold, the scale drifting 1.5% (0–2.5 s,
3.42–5.5 s, 6.42–8 s); that is as much as it moves during the press.

## The camera

From OpenScreen's auto-zoom planner (MIT), on our beat grid:

- **Open wide for 2.5 s** and **end wide for 1 s or more** (here 1.58 s).
- **Zoom on clicks only.** Clicks within 3 s share one zoom.
- **Fully in 0.5 s before the click** (here 0.58 s) and **hold 1.5 s after the
  last click**; 1.8 s zoomed at least (here 2.08 s). At least 1.5 s wide
  between two zooms.
- **Zoom by 1.25, 1.5 or 1.8**: the most at which the `focus` fits in 92% of
  the view and the captures stay sharp (their scale × 1.15; past that, text
  softens).
- **Each ramp lasts 0.6 s + 0.55 s × ln(zoom)**, rounded to the step: 11 steps
  for 1.8×, 10 for 1.5×, 9 for 1.25×.
- **The click stays 12% or more in** from every edge of the zoomed frame.

And from the product film:

- **The wide view** is the `screen` rect whole, with an 8% margin.
- **The zoom's centre** is the click, moved as little as needed to keep the
  whole `focus` in view with a margin (4% of the view, less where it's tight);
  on an axis where the whole `screen` fits in the zoomed view, the screen's
  centre instead. It stays inside the wide view.
- **Edges in gaps.** Both views settle so their edges fall between lines of
  text, never through words: moved up to 10% of the view and scaled up to 4%
  either way, to rows and columns of the page capture that hold no more detail
  than the plainest one near them, and stay plain as the camera breathes.
  Where no such place is near, the view stays where it was.
- A page camera: the page point at the frame's centre and a scale, the scale
  moving in log space, so every shape gets its own framing from the same rects.

## The cursor

A black arrow with a white outline (4.5 px at 53 px tall) and a soft shadow.
9.5% of the frame's short side in the wide view, growing to 12% as the camera
zooms in, and back. It tilts toward where it's going (rest −8°, up to ±16°),
moves fast first with a soft landing, and never rests on the result. Once
in, the whole arrow stays 12 px inside the frame.

## The caption (optional)

Empty by default. When the shot needs one (used on its own, say), it says what
the click does for the viewer, and takes the product film's caption grammar:

- Beside the screen, never on it: a band across the top, 20% of the height,
  in every shape, in the accent. (The product film puts captions in a column
  in wide; here the screen needs the frame's whole width for its result to
  read in the zoom.)
- The product's font at 700 (the reference: Instrument Sans), tracking −0.03 em, on the accent band: 5.6% of the short side; line height
  1.08; inset 8% of the short side; wrapped at the width less 1.6 × the inset.
  It only shrinks (5% at a time) when a word or the lines won't fit.
- It lands at 0.5 s, a word a step, each line 3 steps after the last, from
  116% size and soft to set in 0.22 s; words arrive in the accent and cool to
  white over 0.4 s.
- Up to 32 characters. The screen's part of the frame gets smaller, so check
  the result still reads in the zoom.

## Colour

Paper (the product's background, or `#f1f1ed`) behind the page, ink
(`#0b0b0b`) for the cursor, and one accent, the product's brand colour, for the
caption when there is one. The screen keeps its own colours.

## Sound

- `swish` (0.6) in the middle of the zoom in (2.92 s); `tap` on the click and
  `chime` (0.8) a step after it; `swish` (0.8) as the pull back out starts
  (5.67 s); `pop` (0.6) as a caption lands, when there is one.
- With `--music`, the 120 BPM bed: pad and hats in bar 0, the full groove in
  bars 1–2, pad and hats in bar 3, and a break (drums and bass out) in the beat
  before the click.
- Mastered around −14 LUFS.

The score's sound is `music.style`: here `'synth'`, the default. For the user's product, pick by what it is: `'organic'` for plants, food and drink, and other natural or handmade things; `'synth'` (oscillators, the default) for software and tools; `'felt'` (a sparse felt piano over a sub bass and a light kit) for a quiet, minimal film. In a break (`music.breaks`) the drums, bass and lead stop and the chords play on; the film's name seeds the key (always major), the progressions and the patterns.

## Banned

- A zoom with no click, or a click with no visible change.
- The camera moving during the press (beyond its 1.5% breath).
- A zoom past the captures' scale × 1.15; a frame edge through a line of text.
- A result too small to read in the zoom; the cursor covering it after the
  click.
- A caption laid over the screen; a desktop page in the tall frame.
- Drawn or imagined UI; customer data.
