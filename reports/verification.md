# Verification and corrections

## Source and execution

- Original user notebook inspected: `analysis.ipynb`, blob `6d33ca7b372867c936cebfff7806e97df1be28fe`, repository commit `bcc07df28d598ed985dd4624fb812e7b77fc2d23`.
- The final notebook retrieves original public annotation files from the Bath ZIP via HTTP byte ranges. No video files or full dataset archive are required.
- The final notebook is run from a fresh kernel with all cells in order. The generated `results/environment.json` records package versions; `results/source_manifest.json` records exact source-member names, sizes, and SHA-256 hashes.
- Checks reconcile raw rows, distinct keys, camera counts, track counts, frame counts, one-minute means, and matched-subset size. They test analysis consistency, not annotation completeness.

## Corrections to the original exploration

1. **Outdated hard-coded statistics:** Earlier prose reported 72 matched IDs and different test results even though an executed calculation returned 74. The final report is generated from computed variables.
2. **Unsupported missing-box explanations:** The original source-check cell printed empty lists but later prose asserted that vehicles were filtered or outside active zones. That output did not establish those claims. The final notebook locates each source explicitly and fails if a file cannot be found.
3. **Red car in camera 4 / frame 4500:** The actual SCT file contains local ID 174 at pixel coordinates `(2570.84, 869.99, 2875.28, 1014.78)`. It is not absent from SCT. Detection GT has a matching box. Its exclusion from the MC file has no established cause.
4. **Other targeted cases:** Camera 2 / frame 1 white van is SCT local ID 4. Camera 1 / frame 1 includes local IDs 1 and 5. Exact source rows and geometric comparison results are exported in the targeted-audit files.
5. **File identity:** `labels_GT.zip` is described by the archive README as reviewed/corrected detection labels; `labels_xy.zip` as raw YOLO detections; `labels_test.zip` as baseline annotations. They are not interchangeable. The inspected detection-GT lines contain six fields: class, xmin, ymin, xmax, ymax, score.
6. **Local versus global counts:** The workbook contains four camera-specific sheets, with 262, 244, 279, and 257 rows. The first-sheet preview did not demonstrate a 512-vehicle global list. Local IDs cannot be compared numerically with MC global IDs without a mapping.
7. **Raw versus distinct observations:** MC contains 177,782 rows but 177,756 unique observation keys. SCT also contains repeated keys. The final scope table presents both measures.
8. **Geography:** The supplied contact sheets show distinct roundabouts. Camera 3's higher annotated count is not evidence that it is a central view of a shared roundabout or that it has the highest true traffic flow.
9. **Time and gaps:** Camera 3 / ID 553 has observations at frames 599 and 5378 separated by 4,778 missing frames. Exit/re-entry, occlusion, and an identity error are possible explanations; none was proved. Annotated frame time does not measure continuous visibility or travel time.
10. **Interpretation of the test:** Friedman is an omnibus rank-based comparison, not a causal test or a pairwise camera test. Possible traffic dependence is acknowledged rather than asserted to have been measured. No speed differences are inferred.

## Limits of this verification

The final run uses source annotation records and the earlier contact-sheet examples. It does not decode videos again, perform a representative manual audit of all vehicles, establish identity correctness, or estimate detector precision/recall. A box match at IoU 0.5 is only a reproducible audit criterion. It is not the authors' matching threshold.

The published association script is consistent with exporting selected associated tracks, but its current source is not proof of the exact generation history of every row in the released archive. Discrepancies between the paper's 512 overall IDs / 310 multi-camera IDs and the analyzed file's counts remain unresolved. Full traffic counting requires additional coverage validation.
