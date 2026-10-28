# Cursor camera: critique

Judge the shot as a stranger seeing it in a feed, with the sound off first.
Look at the stress sheets (`out/stress/`), the key-frame and phone sheets of
every shape, the strips at the cursor's entrance, every press, the scroll and
the drag, `motion.mjs` over every camera and cursor move, and the MP4 once for
the picture and once for the sound.

## Score each 1–10 (nothing ships under 8)

1. **The task:** a stranger can say what was done and what came of it; every
   step is the product's own, in its order, once; the last screen is the real
   result.
2. **The cursor:** it enters whole (fading in at rest, never sliding in half
   off the frame) and is exactly where the next beat needs it; it glides on
   gentle arcs, fast out with a soft landing; it hovers about 0.45 s on
   everything it presses, presses on the beat, stays down through a drag, and
   never covers what the viewer must read. No jump, no stop mid-move.
3. **The camera:** every move is carried by a cursor move (same start, same
   length) except the pull backs after a page change, the scroll ride and the
   result; never in and out back to back; no settled edge through a line of
   text; nothing past the captures' sharpness.
4. **Pace:** a beat after every page change and scroll before the next move;
   reading time on what must be read; no wait on the product's own work;
   nothing still past about 3 s; holds simply still.
5. **The app's motion:** hovers are the app's own; presses dip and come back; a
   page change never leaves the eye on an empty page and never swaps in one
   frame; a changed label rolls over, one at a time.
6. **Truth and shapes:** every frame is a real capture with sample data; tall
   shows a tall window; each shape is laid out for its frame; the first frame
   is clean; the text in every zoom reads on the phone sheet.
7. **Sound:** a click on every press, a soft swish with each camera move, a
   pop as each new state arrives, nothing crunchy.

## Hunt for

- **Type centred in its container** (pills, buttons, chips, badges, a word beside a mark): the capitals sit on the container's centre line, measured, not by eye. Words that ride high are the usual fault (textBaseline 'middle' and CSS line boxes both centre the font's em box, not the letters); draw with `kit.centreText`, and in HTML use `text-box: trim-both cap alphabetic` with equal padding. The quick test fails canvas text set with 'middle'; captured screens and HTML are checked on the stills.
- **The film's own shapes, finished:** every click has a press state on its visual onset (what's pressed sinks a few percent and lights or darkens, then comes back), and a held control shows it's held; apertures and reveals are clean circles or the product's own shapes, never blades or drawn lines; a shape that becomes another does it in one continuous move, not a chain of in-between shapes; a pulse is one thin ring that thins as it grows; nothing (a check, a label, an icon) vanishes or appears in a single frame at a hand-off: it moves, shrinks or is covered. Check each on a strip of consecutive frames from the MP4.

For each issue write the shape, the time, what's wrong and the exact fix
("tall, 13.4 s: the cursor covers Running: step off to 115%, 320%"). Fix the worst
three, review again, score again. After three rounds, report what remains.

With each fix, write what it must keep (the timing, sizes and moves already
right) and the times to look at again; look at them, and at the cuts either
side, before scoring again. If the same problem survives two fixes, stop
fixing it and report it with what you tried. Never loosen a check, a size
floor or the bar to get a pass.
