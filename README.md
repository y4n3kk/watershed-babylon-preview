# Watershed Babylon — build preview

A compiled preview build of Watershed Babylon, published so it can be opened on a phone or any browser without a local server. **This repository contains no source code**, only the output of a production build.

Current build: `integration/vertical-slice` at `c3847d6`, with four line and rod changes merged. Every number below is measured on the same deterministic 420-tick drift through the selected donor fixture, against the preserved `rod-line-reference-0` build.

## What this build changes

**The corner just off the rod tip is gone.** The bow that puts the belly in the line was faded in with a half-sine, which is at its steepest exactly where the line first touches the water, so the first wet segment left the straight airborne run sideways at full slope. That is a corner, not a curve. Squaring the sine flattens both ends of the fade, and the arc length a bow adds is identical either way, so nothing had to be retuned.

| | reference 0 | before | after |
| --- | --- | --- | --- |
| worst joint turn | 94.3 deg | 45.6 | **24.9** |
| joints ever over 30 degrees | 19 | 19 | **0** |
| drift ticks showing a corner | 10 % | 22 % | **0 %** |

**The line no longer draws as dashes.** The river surface is wave-displaced in the shader while the line's height comes from Core, so a strand lying on the water crosses the drawn film repeatedly along its own length — measured at 0 to 4 mm of apparent submergence. Ownership between the above-water pass and the underwater capture was a hard threshold on the strand's centreline, so every crossing deleted a whole cross-section. It is now a share handed across a 2 cm band, measured from the strand's own top surface, summing to exactly one at every depth.

**A mend is a one-second stroke, not a jump.** It used to assign the rod's working lift outright, moving the rod tip 1.3434 m in a single tick against 0.016 to 0.029 m either side.

**The rod bends under the line, not only under a fish.** Rod bend median and peak went from a flat 0.033 to 0.044, to 0.120 and 0.223.

## What to look for

Fish a drift. The line should read as one continuous strand with no gaps, and no sharp corner a short way out from the tip.

## Known, not fixed

**While mending, the line still folds back on itself.** Measured through eight strokes: the drawn chain turns past a right angle on 17 of 360 ticks, peaking at 163.5 degrees, and the sharp bend sits on one joint for a full second instead of travelling down the line the way a real mend loop does. Reference 0 does not do this; it peaks at 58 degrees and never folds.

The cause is understood and measured. The fix is not a patch at the point of drawing: three attempts each broke something the build is right to protect — material conservation through a mend, or the slack readability cue. It needs a decision about how a landed line's slack budget is partitioned. Tracked on issue 89.

**No hands or arms.** The line running from the reel down to a floating point and back up is the running line held in the line hand, drawn correctly; there is simply no hand there yet. Tracked on issue 36.
