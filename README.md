# Watershed Babylon — build preview

Compiled preview builds, published so they can be opened on a phone or any browser without a local server. **This repository contains no source code**, only the output of a production build.

## Two builds to compare

There is one decision to make by eye, and both sides of it are here.

When there is loose line out, that line has to be drawn somewhere, and the game draws it as a big lazy S-curve. That curve is the only way the angler can tell "I have slack" from "my line is coming tight". The line has two parts: the stretch hanging in the air from the rod tip down to where it meets the water, and the stretch lying on the water.

### [Curve on the whole line](https://y4n3kk.github.io/watershed-babylon-preview/) — the current build

The S-curve is drawn along both parts, including the stretch hanging in mid-air.

- Slack is easy to read: the curve has the whole line to spread across.
- **While mending, the line folds back over itself.** Measured over eight strokes: the drawn line turns past a right angle on 17 of 360 ticks, peaking at 163.5 degrees, and the crease sits in one place for a full second instead of rolling down the line the way a real mend does.

### [Curve on the water only](https://y4n3kk.github.io/watershed-babylon-preview/curve-on-water/) — the candidate

The S-curve is drawn only along the stretch lying on the water. Nothing else differs.

- **No fold at all.** 0 of 360 ticks, peak 57.8 degrees, and the sharp bend now travels down the line as the stroke rolls, which is what a mend does.
- Slack is slightly harder to read: with less line to spread across, the curve comes out about 1 % narrower than the width the readability check requires (0.494 m against 0.5 m at 0.82 m of slack).

**This candidate does not pass the project's checks** — six tests fail on it, two for the readability width above and four for material accounting downstream of it. It is published to be judged by feel, not proposed for merging.

## What to look for

Fish a drift, then mend it, on each build in turn.

- On the current build the line should curl back on itself near the rod during the mend.
- On the candidate it should not, and the curve showing your slack should be a little shallower.

The question is whether that shallower curve still reads clearly enough. If it does, the fold is solved. If it does not, the slack has to be shown some other way, which is a larger change.

## Both builds also include

- **The corner just off the rod tip is gone.** Worst joint turn 45.6 to 24.9 degrees; corners on 22 % of drift ticks down to none.
- **The line no longer draws as dashes** where it crosses the water surface.
- **A mend is a one-second stroke**, not a one-tick jump.
- **The rod bends under the line's own pull**, not only under a fish.

## Known, not fixed, on both

No hands or arms. The line running from the reel down to a floating point and back up is the running line held in the line hand, drawn correctly; there is simply no hand there yet.
