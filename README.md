# Watershed Babylon — build preview

Compiled builds, published to be judged by feel on a phone. **This repository contains no source code**, only build output.

## The three

### [Current](https://y4n3kk.github.io/watershed-babylon-preview/)

What ships today.

### [Reference 0](https://y4n3kk.github.io/watershed-babylon-preview/reference-0/)

The preserved build at `bfe73b45237790a88188e2a1f01c010c7e395041`, built unchanged. Not a reconstruction: the actual thing. It predates the finite mend stroke, the current fish and hooking model and the current material accounting, so the game around the line differs too.

### [Line visibility](https://y4n3kk.github.io/watershed-babylon-preview/line-visible/) — issues 94 and 99

The current build with **one change**: a floor under how faint a strand may be drawn.

Every vertex of the drawn chain carries its own opacity, computed from that vertex's own distance and its strand's own diameter, through a function called with **no minimum at all**. So the line faded out along its own length. Measured over a 424-tick drift from the angler's eye:

| | before | after |
| --- | --- | --- |
| faintest vertex opacity | 0.018 | **0.400** |
| frames with a near-invisible vertex | 424 of 424 | **0 of 424** |
| worst jump between neighbouring vertices | 0.277 | **0.030** |
| frames with a cliff edge over 0.25 | 20 % | **0 %** |

Opacity along the chain before the change, with cliff edges at both junctions:



This is upstream of the water entirely: a floating line, a sunk line and a line in the air were all subject to it. It is a separate cause from the film ownership PR #90 addressed, which was measured and found correctly inert for a floating line.

**The trade to judge:** beyond the near fly line everything now sits at the floor, so the taper from fly line to leader to tippet is flattened. A finer strand should still read as finer. If the line now looks uniform, the floor is too high; if it still breaks up, too low.

### [Rod cast load](https://y4n3kk.github.io/watershed-babylon-preview/rod-load/) — the test version

The current build with **one change**: the rod now loads against the line's mass while it is being swung.

## What the test version changes, and why

The owner's judgement was that reference 0 has the better rod actuation and cast, and the current build the better drift and strip. Measuring the rod through a cast on the same deterministic scenario found the reason, and it is not subtle:

| rodBend01 | reference 0 | current | test version |
| --- | --- | --- | --- |
| **through a cast** | **0.650** | **0.037** | **0.608 peak, 0.342 median** |
| drift | 0.079 | 0.119 | 0.116 |
| retrieve | 0.120 | 0.066 | 0.064 |

The current build's rod deflection is drawn from a hooked fish, or from the line's tow while drifting or retrieving. **There was no term at all for the rod being swung.** Through a whole cast the reaction was therefore zero and the blank had nothing left but its fixed 0.048 m gravity droop — a straight stick with a millimetre of sag, by construction.

Reference 0 takes it from the stroke's own energy, `clamp(0.1 + energy01 * 0.55, 0.1, 0.7)`, which is the right quantity: a cast IS the rod loading against the line's mass as the angler accelerates it. The test version uses that same mapping.

Only the casting branch is added. Fighting, drifting and retrieving keep exactly the reaction they had.

## The drift is not traded away

Measured over the same 425-tick drift:

| | current | test version |
| --- | --- | --- |
| worst joint turn | 25.1 deg | **19.4 deg** |
| drift ticks showing a corner | 0 % | 0 % |
| bow collapse | 4.7x | 4.8x |
| rod bend, median | 0.119 | 0.116 |

One thing did move: the fly now drifts at 1.14 times the water speed where it was 1.08, and the rod tip's peak speed during a drift rose from 7.15 to 14.52 m/s. That is the loaded rod unloading as the cast settles, which is a rod doing what a rod does, but it is a real behaviour change and worth watching for.

## What to look for

Cast on each build in turn and watch the rod itself, not the line.

- On **current**, the blank should stay essentially straight through the stroke.
- On **reference 0** and the **test version**, it should bow under the load and come back.

Then fish a drift on the test version and check the line still behaves the way you preferred — that part is meant to be untouched.

## Test result, and its cost

Full suite on the test version: **1067 passed, 2 failed**. Neither failure is a line or a rod test:

- `hookable resident encounters (p41)` — a drift engages a resident fish through its own full encounter while the hero never notices
- `production player QA scenarios` — two-cast revisions to terminal debriefs across seeds

Both are fish-encounter tests. The rod change shifts the simulation trajectory: the fly drifts at 1.14 times the water speed where it was 1.08, so it arrives in different places, so fish engage differently and the scripted scenarios reach different outcomes.

That is the honest cost of this change. The rod loading is physically right and the drawn line is untouched, but it moves where the fly goes, and this project guards fish outcomes deliberately. Whether that is acceptable depends on whether the new drift speed is more correct or merely different, which is not yet established.

Published for feel, not proposed for merging.

## Also not addressed

Reference 0 draws its rod as two pieces, a fixed handle and a flexing shaft, which can visibly part company. That is a separate matter from whether the rod loads, and is not touched here.
