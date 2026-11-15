# RoundaboutHD: annotation coverage and camera comparison

This study examined vehicle annotations from four cameras monitoring different roundabouts. The objectives were to compare annotated observations, assess data quality, and explore whether annotated frame time differs across cameras for the same vehicles.

The multi-camera file contains 177,782 rows and 311 global vehicle IDs. Counting each camera–vehicle–frame key once gives 177,756 distinct observations. Camera 3 has the highest annotated ID count (243), followed by cameras 2, 4, and 1. Its mean annotated count is 5.85 per frame. These quantities describe included records, not verified totals of passing traffic.

The single-camera files contain 1,042 local IDs and 232,945 rows, matching the published SCT totals. Local IDs cannot be summed to count unique vehicles across cameras. Targeted source checks found four selected vehicle boxes in SCT and detection ground truth but without matching multi-camera boxes at an audit IoU threshold of 0.5. The association script supports selection of trajectories, but individual exclusion reasons remain unresolved.

For 74 IDs observed in all four cameras, annotated frame time was calculated as distinct annotated frames divided by 15 FPS. An exploratory Friedman test found evidence of camera differences (Q = 23.4268, p = 0.0000329), with a relatively small effect magnitude (Kendall's W = 0.1055). Possible dependence between vehicles and selection of the matched subset limit interpretation. The test does not establish causes or significant pairwise differences.

The audit identified 26 conflicting keys and annotation gaps. ID 553 has a 318.53-second gap whose cause remains unverified. Annotated frame time is not travel time or speed. The data supports analysis of included observations; complete traffic counting requires coverage validation. Differences from published global-ID totals remain unresolved.
