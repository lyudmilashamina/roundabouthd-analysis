
I analyzed vehicle annotations from four cameras monitoring different roundabouts. I used Python to check the records, compare cameras, and plot changes over ten minutes.

The multi-camera file contains 311 vehicle IDs. Camera 3 has the highest annotated count, but this does not necessarily mean it carries the most traffic.

For 74 vehicles observed by all four cameras, I compared the total time represented by annotated frames. An exploratory Friedman test found camera differences with a relatively small effect magnitude.

I also found conflicting records and gaps. Selected vehicles appeared in single-camera annotations but had no matching boxes in the multi-camera file. Therefore, the main result is a comparison of the included observations, with clear limitations on complete traffic counting and travel-time interpretation.

## Research Questions, Methods, and Findings

### 1. How many vehicles are represented, and which camera records the most?

**Method:** I counted unique vehicle IDs using pandas.

**Finding:** The multi-camera file contains 311 unique IDs. Camera 3 has the highest count, with 243. These figures describe the included annotations, not necessarily all traffic.

### 2. How do observations change over time?

**Method:** I counted annotated IDs in each frame and calculated one-minute averages.

**Finding:** Counts varied during the recording. Camera 3 had the highest overall average at 5.85 annotated IDs per frame. The reasons for these differences remain unresolved.

### 3. Does annotated observation time differ across cameras?

**Hypothesis:** There is no systematic camera effect on annotated observation time.

**Method:** I applied the Friedman test to 74 vehicles observed in all four cameras. This test compares related measurements without requiring normality.

**Finding:** The test provided evidence of differences (*p* ≈ 0.000033), with a relatively small effect size (Kendall’s W ≈ 0.106). The result is exploratory because vehicles may not be independent and the selected subset may not represent all traffic. It does not establish the cause of the differences.

### 4. How reliable and complete are the annotations?

**Method:** I checked repeated records, observation gaps, and selected examples across annotation sources.

**Finding:** I found 26 conflicting observation keys. Some vehicles appeared in single-camera annotations but had no matching boxes in the multi-camera file. These findings identify limitations without proving that the entire dataset is poorly annotated.

### 5. Can this analysis estimate speed or total traffic?

**Method:** I checked the available coordinates, timing information, and annotation coverage.

**Finding:** Not directly. Speed requires verified distances and timing, while total traffic requires validated coverage. The world-coordinate columns contain placeholders, and annotated frame time is not journey duration.



## Data preparation and cleaning

I checked the data format and valid values, converted world-coordinate placeholders to missing values in a working copy, and flagged 26 conflicting observation keys. There were no completely identical rows to remove. For counts and timing, I used 177,756 unique camera–vehicle–frame observations instead of counting all 177,782 rows. All 311 vehicle IDs were retained. I kept gaps and conflicting boxes for review rather than filling or resolving them by guesswork.

[Preparation and cleaning details](data_preparation_and_cleaning.md)
