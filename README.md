# Watershed Babylon — build preview

Compiled builds, published to be judged by feel on a phone. **This repository contains no source code**, only build output.

## The three

### [Current](https://y4n3kk.github.io/watershed-babylon-preview/)

What ships today.

### [Reference 0](https://y4n3kk.github.io/watershed-babylon-preview/reference-0/)

The preserved build at `bfe73b45237790a88188e2a1f01c010c7e395041`, built unchanged. Not a reconstruction: the actual thing. It predates the finite mend stroke, the current fish and hooking model and the current material accounting, so the game around the line differs too.

### [Line lifted](https://y4n3kk.github.io/watershed-babylon-preview/line-lifted/) — issue 94, the dashed line

The current build with **one number changed**: a floating line now rides 0.12 m above the film instead of 0.04 m.

The drawn river is displaced in the vertex shader, and its wave amplitude reaches about 0.14 m in shallow turbulent water:

```
wsWaveAmp = 0.14 * smoothstep(0.28, 0.8, turbulence)
                 * smoothstep(1.1, 0.35, depth)
          + 0.01 * turbulence
```

The line rode 0.04 m. So wave crests rose over it, in patches, wherever a crest happened to be along its length, moving as the waves move. A line intermittently swallowed along its own length is a dashed line — and it explains why it is only sometimes, and only in places.

**This is a stopgap and should be judged as one.** A floating line ought to RIDE the displaced surface, rising and falling with each wave, rather than hovering at a fixed height above the mean. That needs the shader's wave displacement to be available where the line's height is decided, and it is not today. Lifting the line trades a line that vanishes in patches for a line that may sit visibly too high in calm water.

**What to look for:** whether the dashes are gone, and whether the line now looks like it is floating above the water rather than on it. If both, the real fix is worth the work.

Two earlier candidates for this were ruled out by measurement: the water-film ownership PR #90 addressed (measured correctly inert for a floating line), and per-vertex opacity (smooth along the fly line, so it cannot band it).

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
