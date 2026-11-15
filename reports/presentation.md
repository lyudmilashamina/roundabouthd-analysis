# Presentation notes

## Approximately 60 seconds

I analyzed vehicle annotations from four cameras monitoring different roundabouts. I used Python to check the records, compare cameras, and plot changes over ten minutes.

The multi-camera file contains 311 vehicle IDs. Camera 3 has the highest annotated count, but this does not necessarily mean it carries the most traffic.

For 74 vehicles observed by all four cameras, I compared the total time represented by annotated frames. An exploratory Friedman test found camera differences with a relatively small effect magnitude.

I also found conflicting records and gaps. Selected vehicles appeared in single-camera annotations but had no matching boxes in the multi-camera file. Therefore, the main result is a comparison of the included observations, with clear limitations on complete traffic counting and travel-time interpretation.

## Five likely questions

**1. Did you train a machine-learning model?**
No. I analyzed supplied annotations. The authors describe model-assisted annotation with manual correction and manual cross-camera association.

**2. Why does camera 3 have more IDs?**
It has more included annotated IDs. Traffic patterns, coverage, and annotation selection are possible explanations, but their contributions were not established.

**3. Why use the Friedman test?**
The same vehicles supply four related measurements. Friedman compares within-vehicle ranks without requiring normality. Vehicle independence may be imperfect, so the result is exploratory.

**4. Do missing boxes mean the dataset is bad?**
Not automatically. Different annotation sources include different records. We documented conflicts and selected missing matches, but did not estimate annotation accuracy or prove each exclusion's cause.

**5. Can this analysis estimate speed or total traffic?**
Not directly. Speed needs verified geometry and timing; total traffic needs validated coverage. Frame time is not journey duration, and the available world-coordinate columns contain placeholders.
