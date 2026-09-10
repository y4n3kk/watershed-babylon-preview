# Asset Provenance

All diffuse and normal-map files under `public/assets/textures/` in this tranche:

- Source: Poly Haven (polyhaven.com), asset pages https://polyhaven.com/a/<slug>
  where <slug> is the filename before `_diff_2k`.
- License: CC0 1.0 Universal (public domain dedication). Attribution not required;
  recorded here per project policy. Creators credited on each Poly Haven asset page.
- Downloaded: 2026-08-23, 2K JPEG diffuse maps and the listed 1K OpenGL normal maps, via
  dl.polyhaven.org.
- Selection governed by BABYLON_ASSET_MANIFEST.md (owner-approved curated process).

Files: river_small_rocks, dry_river_pebbles, ganges_river_pebbles, rocks_ground_01,
rock_face_03, cliff_side, gray_rocks, forest_floor, bark_brown_01 (each `_diff_2k.jpg`).

Normal maps present: bark_brown_01, dry_river_pebbles, forest_floor,
ganges_river_pebbles, gray_rocks, river_small_rocks, and rocks_ground_01 (each
`_nor_gl_1k.jpg`). The selected renderer currently references bark_brown_01,
ganges_river_pebbles, gray_rocks, river_small_rocks, and rocks_ground_01. Presence does not imply
runtime use; this inventory exists so future asset audits can distinguish unused files from missing
provenance.

### Runtime texture integrity (SHA-256, audited 2026-09-02)

| File | Bytes | SHA-256 |
| --- | ---: | --- |
| `bark_brown_01_diff_2k.jpg` | 2667267 | `0cdd066f34d357fdbf7eb99159e668a6dc346bb7fd093a9e27058eb827d09b9a` |
| `bark_brown_01_nor_gl_1k.jpg` | 1226534 | `9d1537b3429579436a62890bb7c5050a0172a15ce768787eacde81c5ccefc9cc` |
| `cliff_side_diff_2k.jpg` | 3387348 | `bc6f92d72eb6383ecc3a1094ed9f5b37efb36ccf83cf29699bb5990e6775afee` |
| `dry_river_pebbles_diff_2k.jpg` | 3251744 | `f3d3b581bffc78be28b1eb4b73101bff574841944fb6867be901b3bc03d1bda7` |
| `dry_river_pebbles_nor_gl_1k.jpg` | 1137689 | `6e266f6cde5ed79b103533bd14bb4a29fbb5966c00782790bd5db41d12ab4e97` |
| `forest_floor_diff_2k.jpg` | 5452936 | `308bc5f916dcc113bf276cbfdc411bed48b6a9ce5e3bc0c228faa3d54acf125d` |
| `forest_floor_nor_gl_1k.jpg` | 1380104 | `681f3de8c756c4d19bcda33039f953295498f38b1425ce9d56b37d6f97f6e518` |
| `ganges_river_pebbles_diff_2k.jpg` | 3264787 | `4284c19b6a546c8536a2d5383e5dcdbbae83ab6c2c337c7a0fb25284b0bea419` |
| `ganges_river_pebbles_nor_gl_1k.jpg` | 1212799 | `80ea9d0cf01402632e1161def4d4f4efc99df21c5382de90c8c16ee827ea7735` |
| `gray_rocks_diff_2k.jpg` | 4036501 | `01de284f33b6c075386aea11f053df4f64cd4a42cb39e6d14d6adcc22d021ffa` |
| `gray_rocks_nor_gl_1k.jpg` | 1266242 | `1922b18e09a95bb782794163117ea47d62771dd59501085cc95ab10081107a9d` |
| `river_small_rocks_diff_2k.jpg` | 3908784 | `656a20860f5960cc0f442dd425bfe4607052ab1749efdde35d60c5df9639beac` |
| `river_small_rocks_nor_gl_1k.jpg` | 1365737 | `983f99bd61cdcdeb3d2ebe0cbba851fd58f249d38f9e76a25084a558ee56e8e6` |
| `rock_face_03_diff_2k.jpg` | 3814362 | `644ee79df7ffbf5f6afc330b64dd3f33794bab8820915fe61ffe0c88ecfd7ece` |
| `rocks_ground_01_diff_2k.jpg` | 2654230 | `3397689c36be4fda00da2649fd81983fbcd6f5664189086a42ad404d6281bd48` |
| `rocks_ground_01_nor_gl_1k.jpg` | 1394176 | `3e4b405b57d3515169e585e005a0b8d6155a169350e6190124669ca6ed334c51` |

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
