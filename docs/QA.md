# QA report

## Automated checks

- Atlas format: WebP RGBA
- Sprite version: 2
- Dimensions: 1536×2288
- Grid: 8 columns × 11 rows
- Cell size: 192×208
- Transparent RGB residue: 0 pixels
- Validator errors: 0
- Validator warnings: 0
- Frame-inspection errors: 0
- Frame-inspection warnings: 0

## Change isolation

Only idle cells `r0c0` through `r0c5` changed in the hair-outline repair.

- Dedicated neutral cell `r0c6`: unchanged
- Unused idle cell `r0c7`: unchanged
- Rows 1 through 10: byte-for-byte RGBA pixel-equivalent to the previously published optimized atlas
- Previous published atlas SHA-256: `655cdd26b48e38c3c010309fc94d106691a048baf0510f49f93a089178eaac07`
- Final repaired atlas SHA-256: `f8a554134d97de4c5328afab6c91127a29a7e3b1153535f84d08cfc28dbc9526`

## Hair-outline repair

- All six idle frames reuse the exact clean original hair silhouette and alpha channel.
- Open-eye gaze is produced only inside the two original eye apertures with a two-pixel horizontal shift.
- Every pixel outside the eye apertures is identical to its clean source frame.
- Light- and dark-background edge checks show a single stable hair contour with no generated matte fringe.

## Visual artifacts

- [Full contact sheet](../previews/contact-sheet.png)
- [Autonomous idle loop](../previews/idle-autonomous.gif)
- [16-direction QA sheet](../previews/look-directions.png)

The idle loop is intentionally low-distraction: the feet remain planted, the silhouette and baseline stay stable, and motion is limited to eye direction, blinking, and very small head changes.

## Independent visual review

PASS. On both light and dark backgrounds, all six idle frames show one crisp stable hair outline with no halo, doubled contour, blur, or afterimage. Left/right gaze, two blinks, identity, body registration, rows 1–10, and v2 validation all pass; all 16 look directions remain complete and coherent.

## Failed-row transition repair

Only failed cells `r5c3`, `r5c4`, and `r5c5` changed from the hair-outline release.

- Approved failed frames 0, 1, 2, 6, and 7: unchanged
- All other rows and all 16 look directions: unchanged
- Middle-frame subject widths: `130 / 136 / 145` → `111 / 113 / 115` pixels
- Middle-frame subject heights: `198 / 198 / 198` → `181 / 171 / 167` pixels
- Previous atlas SHA-256: `f8a554134d97de4c5328afab6c91127a29a7e3b1153535f84d08cfc28dbc9526`
- Final atlas SHA-256: `eec2484eddc9f750ec98323683c7f8605fa54072ae8bde4e1a36b46e9f6af229`
- [Optimized failed preview](../previews/failed-optimized.gif)

Independent visual review: PASS. Frames 3–5 now form a smooth `181 → 171 → 167` pixel slump into unchanged frame 6; proportions, identity, edges, directions, and dark-background cleanup remain stable. The repair removes the unintended camera-zoom effect while preserving the palette, pixel-art identity, and failed-state semantics.

## Failed-row ghosting correction

The first transition-repair assembly alpha-pasted the new transparent sprites over uncleared atlas cells. Transparent regions therefore exposed pixels from the older, larger character underneath and produced a visible double image while crouching.

- Rebuilt from the clean pre-transition atlas instead of the faulty composite.
- Cleared the complete `r5c3`, `r5c4`, and `r5c5` cells before compositing the approved replacement sprites.
- Each finalized repaired cell is pixel-identical to its replacement-only source.
- Extra visible pixels outside each replacement sprite: `0 / 0 / 0`.
- Transparent RGB residue: `0` pixels.
- Changed cells versus the clean pre-transition atlas: exactly `r5c3`, `r5c4`, and `r5c5`.
- Faulty composite SHA-256: `eec2484eddc9f750ec98323683c7f8605fa54072ae8bde4e1a36b46e9f6af229`.
- Ghost-free atlas SHA-256: `0a5c40e02271b1fe7d714d90e00fb74288c11e7cbd8a3e50c5ec00ea997d35b8`.

Independent visual review: PASS. Frames 3–5 show single clean silhouettes with no ghosting or doubled outlines, transition smoothly from frame 2 through frame 6, and preserve Violet's identity and every other animation row. The v2 atlas validator also passes with no errors or warnings.

## Idle blink stability and crouch-edge repair

Two additional motion defects were corrected without regenerating or changing the approved poses.

### Idle stability

- `r0c0` supplies the complete stationary sprite, transparency, silhouette, body, clothing, feet, and baseline for all six idle frames.
- Only two fixed eye apertures are copied from each original frame, preserving the autonomous left glance, blink, right glance, blink, and neutral sequence.
- Every idle frame now has the same alpha mask and `37,5–154,203` bounding box.
- Pixels outside the two eye apertures differ from `r0c0` by exactly `0` in every idle frame.

### Failed-row outline clarity

- Only bright pixels on the one-pixel visible boundary of `r5c3`, `r5c4`, and `r5c5` were darkened moderately.
- Pose geometry, alpha, bounding boxes, and visible-pixel counts are unchanged.
- Boundary dark-pixel ratios increased from `0.808 / 0.775 / 0.732` to `0.930 / 0.878 / 0.890`.
- All other cells remain pixel-identical to the previous ghost-free release.

- Previous atlas SHA-256: `0a5c40e02271b1fe7d714d90e00fb74288c11e7cbd8a3e50c5ec00ea997d35b8`.
- Final atlas SHA-256: `edade1ca721d73d21b75588a6dd89cb0cc766f7f5230696adc368ad417cc302a`.

Independent visual review: PASS. The idle blink loop holds a stable silhouette and baseline with natural eye motion and no eye-patch seam. The failed crouch transition has crisp readable edges on dark and light backgrounds, without a harsh halo, added jagged outline, ghosting, blur, or pose change. All other animation rows and look directions remain intact, and v2 validation passes with no errors or warnings.
