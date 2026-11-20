# Data preparation and cleaning

I prepared the multi-camera annotations for counting vehicles and comparing annotated observation time. I used pandas and NumPy, kept the original files unchanged, and generated separate working tables.

## What I checked and changed

- Checked column structure, missing/non-finite values, integer IDs and frames, valid camera/frame ranges, and positive box dimensions. These checks passed for the multi-camera file.
- Checked for completely identical rows: **0 removed**.
- Found **26 conflicting observation keys**, involving **52 rows**. I retained and flagged the different box candidates instead of choosing one arbitrarily.
- Created a table with **177,756 unique observations** from **177,782 input rows**. Each camera–vehicle–frame combination contributes once to counts and timing; all **311 vehicle IDs** remain.
- Converted world-coordinate placeholders (`-1`) to missing values in the working annotations. I did not use these columns to calculate speed.
- Added relative seconds and minute intervals using 15 FPS. Frame 1 starts at zero seconds.
- Flagged **13 gaps across 5 tracks**. I kept these tracks and did not fill the missing frames. Long gaps are not evidence of continuous observation.

## Files and limits

The notebook creates `data/processed/annotations_prepared_with_flags.csv` and `data/processed/observations_for_counts_and_timing.csv` in the cloud runtime. Summary counts and gap diagnostics are saved in `results/`. Raw and processed datasets are excluded from Git commits; the notebook regenerates them.

The observation table is suitable for counting included annotations and calculating annotated frame time. It is not a corrected bounding-box training dataset. Conflicting boxes, selected missing matches, and the reasons for exclusions remain unresolved. I did not claim that this cleaning recovers all traffic or establishes annotation accuracy.

## How I would explain it

I checked the annotation format, handled placeholder coordinates, and made sure repeated observations were counted only once. I kept uncertain records visible instead of guessing how to fix them. This gives me a consistent basis for the analysis while preserving the dataset's limitations.
