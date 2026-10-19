# Cursor camera: critique

Judge the shot as a stranger seeing it in a feed, with the sound off first.
Look at the stress sheets (`out/stress/`), the key-frame and phone sheets of
every shape, the strips at the zoom in, the click and the pull back out, and
the MP4 once for the picture and once for the sound.

## Score each 1–10 (nothing ships under 8)

1. **Proof:** one click, one real result you can see; the caption, if any, says
   what it does for the viewer, and the zoomed frame shows it answered.
2. **Camera:** opens wide long enough to place the control; zooms only for the
   click, fully in before it; holds still through the press; holds the result
   about 1.5 s; pulls back front-loaded and ends wide. No frame edge, wide or
   zoomed, cuts through a line of text.
3. **Cursor:** comes in fast and lands soft; aims and presses on the beat;
   steps off so the result reads; its size follows the zoom.
4. **Readability:** in every shape, the result's text in the zoomed frame is
   2.4% of the short side or more (and reads on the tall phone sheet); a
   caption, if any, is above the floor; nothing is shown past its capture's
   sharpness.
5. **Truth and shapes:** every frame is a real capture with sample data; tall
   shows the phone layout; each shape is laid out for its frame; the first
   frame is clean; a caption, if any, claims only what the zoom shows.
6. **Rhythm and sound:** the click on a downbeat, a breath before it, a sound on
   the click and on each camera move.

## Hunt for

- **Type centred in its container** (pills, buttons, chips, badges, a word beside a mark): the capitals sit on the container's centre line, measured, not by eye. Words that ride high are the usual fault (textBaseline 'middle' and CSS line boxes both centre the font's em box, not the letters); draw with `kit.centreText`, and in HTML use `text-box: trim-both cap alphabetic` with equal padding. The quick test fails canvas text set with 'middle'; captured screens and HTML are checked on the stills.
- **The film's own shapes, finished:** every click has a press state on its visual onset (what's pressed sinks a few percent and lights or darkens, then comes back), and a held control shows it's held; apertures and reveals are clean circles or the product's own shapes, never blades or drawn lines; a shape that becomes another does it in one continuous move, not a chain of in-between shapes; a pulse is one thin ring that thins as it grows; nothing (a check, a label, an icon) vanishes or appears in a single frame at a hand-off: it moves, shrinks or is covered. Check each on a strip of consecutive frames from the MP4.

For each issue write the shape, the time, what's wrong and the exact fix
("tall, 4.6 s: the cursor covers Saved: rest it at 110%, 130%"). Fix the worst
three, review again, score again. After three rounds, report what remains.

With each fix, write what it must keep (the timing, sizes and moves already
right) and the times to look at again; look at them, and at the cuts either
side, before scoring again. If the same problem survives two fixes, stop
fixing it and report it with what you tried. Never loosen a check, a size
floor or the bar to get a pass.
