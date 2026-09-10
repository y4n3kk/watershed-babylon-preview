# Asset Provenance

All files under `public/assets/textures/` in this tranche:

- Source: Poly Haven (polyhaven.com), asset pages https://polyhaven.com/a/<slug>
  where <slug> is the filename before `_diff_2k`.
- License: CC0 1.0 Universal (public domain dedication). Attribution not required;
  recorded here per project policy. Creators credited on each Poly Haven asset page.
- Downloaded: 2026-08-23, 2K JPEG diffuse maps, via dl.polyhaven.org.
- Selection governed by BABYLON_ASSET_MANIFEST.md (owner-approved curated process).

Files: river_small_rocks, dry_river_pebbles, ganges_river_pebbles, rocks_ground_01,
rock_face_03, cliff_side, gray_rocks, forest_floor, bark_brown_01 (each `_diff_2k.jpg`).

## Catch-card photographs (p63, banded p65)

Shown on the catch card when the angler holds a landed fish (R). Four files
under `public/assets/photos/`, selected by length and sex in
`src/client/catchPhoto.ts`:

| File | Band | Owner's note |
| --- | --- | --- |
| `cutthroat-small.jpg` | under 12" | smallest fish, held in hand |
| `cutthroat-mid.jpg` | 12" to 16" | orange stripe, held in hand |
| `cutthroat-adult-female.jpg` | 16" to 20", and any female above | 18-20" female, in the net |
| `cutthroat-large-male-red.jpg` | 20"+ males | 20-24" hard-coloured male |

- Source: OWNER-SUPPLIED. Placed in the repository 2026-08-25; all four are
  JPEG, 1089-1438 px wide. The card uses object-fit: cover, so aspect ratios
  differing between them (1.33 to 2.00) crop rather than distort.
- License: **UNVERIFIED — must be confirmed before any public build ships.**
  The texture tranche here is CC0 by deliberate policy. Photographs of real
  fish are very unlikely to be CC0 unless the owner took them; if any came from
  a web search or a stock site, each needs a license permitting redistribution
  in a shipped game. At least one of the four appears to be image-generated
  rather than photographic, which carries its own provenance question.
- The client resolves each file at runtime and hides the image if it is absent,
  so the card renders correctly with or without them, and nothing is bundled
  until the files are placed here deliberately.

## 1k variants (2026-09-05)

Every `*_1k.jpg` beside a `*_2k.jpg` is that same file halved in each dimension by `harness/resizeTextures.mjs` (headless Chrome canvas, no new dependency). Same source, same licence, same provenance line as its 2k original; the phone tier loads the 1k set (PERF-12).
