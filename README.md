# Watershed Babylon — line comparison

Four builds of the same game, differing only in how the fly line behaves. Published to be judged by feel on a phone. **This repository contains no source code**, only build output.

All four are the current build (`c3847d6`) with one line change each. Every number below is measured on the same deterministic drift.

## The four

### [Current](https://y4n3kk.github.io/watershed-babylon-preview/)

What ships today. The line is drawn with 46 points, smoothed at the touchdown join.

Worst joint turn **25.1 deg** · bow collapse **4.7x** an ordinary tick · passes every test.

### [A — reference 0's drawing resolution](https://y4n3kk.github.io/watershed-babylon-preview/line-a/)

The only change is how finely the line is drawn: **20 points instead of 46**, which is what reference 0 used. The shape maths is untouched.

Worst joint turn **40.3 deg** · bow collapse **3.6x**, the calmest of the four.

The higher joint figure is the same curve sampled more coarsely, not a new bend.

### [B — reference 0's resolution and its shape maths](https://y4n3kk.github.io/watershed-babylon-preview/line-b/)

A, plus reference 0's own line-shape function: a plain half-sine bow rather than its square, a linear descent into the water with no rounded join, and the S-waves confined to the wet run.

Worst joint turn **56.1 deg** · bow collapse **3.3x**.

Reintroduces a corner where the line meets the water. That corner is the one visible in the owner's phone recording and removed in PR #91.

### [D — the full reconstruction](https://y4n3kk.github.io/watershed-babylon-preview/line-d/)

B, plus reference 0's rule for how much line lies on the water (a linear touchdown slide rather than a rooted one).

Worst joint turn **113.6 deg** · bow collapse **18.5x**.

## The thing to know before judging

Reference 0's line is **the snapping line**. Its measured bow-collapse rate is 18.0x an ordinary tick; D reproduces that at 18.5x, against 4.7x for what ships today.

That collapse is what the owner originally reported: the line going "from belly to straight in seemingly one tick when fully tensioned". It is a property of reference 0, and reconstructing reference 0's line brings it back.

D is in fact slightly worse than reference 0 on this, because it puts reference 0's line under the current build's much more energetic rod and mend. Those two were never designed together.

So "make it like reference 0" and "stop it snapping" pull in opposite directions. This lineup exists so the owner can decide which they actually want, by feel rather than by argument.

## What to look for

Fish a drift on each, and mend it.

- **Line texture.** A, B and D draw a coarser, more faceted line. Current draws a smoother one. This is the most immediately visible difference.
- **Where the line meets the water.** B and D put a corner there. Current and A do not.
- **Coming tight.** Watch the belly as the line straightens. On D it should give way suddenly. On current it should ease.

## Test status, honestly

None of A, B or D passes the project's checks as they stand.

- **A** fails one test, `line-kink`, which asserts no joint ever turns past 30 degrees. That test was written against a 46-point line and inflates when the line is drawn with 20. That is a fault in the test, not in A.
- **B** fails the same one test.
- **D** fails two: the same one, and a bound on how fast the bow may collapse.

These are published for judgement, not proposed for merging. Whichever is chosen gets done properly.
