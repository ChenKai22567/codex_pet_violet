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
