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

Only idle cells `r0c0` through `r0c5` changed in the final atlas.

- Dedicated neutral cell `r0c6`: unchanged
- Unused idle cell `r0c7`: unchanged
- Rows 1 through 10: byte-for-byte RGBA pixel-equivalent to the previously installed optimized atlas
- Previous atlas SHA-256: `c8ec4fda9dec4192a2d23abca3f0ea8472f553c7fef0bffbcb2697f170ce2612`
- Final atlas SHA-256: `655cdd26b48e38c3c010309fc94d106691a048baf0510f49f93a089178eaac07`

## Visual artifacts

- [Full contact sheet](../previews/contact-sheet.png)
- [Autonomous idle loop](../previews/idle-autonomous.gif)
- [16-direction QA sheet](../previews/look-directions.png)

The idle loop is intentionally low-distraction: the feet remain planted, the silhouette and baseline stay stable, and motion is limited to eye direction, blinking, and very small head changes.

## Independent visual review

PASS. The autonomous idle visibly but subtly glances left and right with two natural blinks; identity, proportions, and baseline remain stable. No body travel, jumping, props, or effects appear in the idle loop. Rows 1–10 match the intentionally accepted hover-review baseline, and all 16 look directions remain complete and coherent.
