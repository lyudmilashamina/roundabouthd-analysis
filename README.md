# RoundaboutHD: exploring vehicle annotations

I used this project to explore how vehicles are recorded by four cameras at different roundabouts. I wanted to understand what the data contains, compare the cameras, and check whether the annotations are suitable for further analysis.

The project uses the existing RoundaboutHD annotations. I did not train a new machine-learning model.

## My questions

- How many annotated vehicles appear in each camera, and how does the number change over time?
- Are there missing observations or conflicting records?
- For vehicles seen by all four cameras, does annotated observation time differ between cameras?

## What I did

I used Python, pandas, NumPy, Matplotlib, and SciPy to inspect the files, check repeated records, summarize observations, and create three charts. I also compared the single-camera and multi-camera annotations for selected vehicles that appeared without boxes in the contact sheets.

For the statistical comparison, I selected the same 74 vehicle IDs in all four cameras and applied a Friedman test. I measured annotated frame time by dividing the number of distinct annotated frames by 15 frames per second.

## What I found

The multi-camera file contains **311 unique vehicle IDs** and **177,782 rows**. These are the IDs included in this file, not a confirmed count of every vehicle passing through the area.

| Camera | Unique annotated IDs | Average annotated IDs per frame |
| --- | ---: | ---: |
| 1 | 179 | 3.98 |
| 2 | 222 | 5.54 |
| 3 | 243 | 5.85 |
| 4 | 189 | 4.38 |

Camera 3 has the highest annotated count. I could not establish whether this comes from traffic patterns, camera coverage, or which vehicles were included in the annotations.

I found **26 conflicting observation keys**: the same vehicle ID has different boxes in the same camera and frame. For time and count calculations, I counted each key once and kept the original records for inspection.

The Friedman test found differences between cameras (**p ≈ 0.000033**), with a relatively small effect size (**Kendall's W ≈ 0.106**). This is an exploratory result: the selected vehicles may not represent all traffic, and observations of different vehicles may be related.

![Unique annotated IDs per camera](figures/unique_annotated_ids.svg)

## What the results do not tell me

Some visible vehicles have records in single-camera annotations but no matching boxes in the multi-camera file. This does not automatically mean the dataset is badly annotated. The sources include different records, and the reason for each exclusion is still unclear.

Annotated frame time is also different from travel time: a vehicle can disappear from the records and reappear later. I therefore did not use it to calculate vehicle speed. The difference between the 311 IDs in this file and the published overall count of 512 remains unresolved.

## Files to open

- [Final analysis notebook](final_analysis.ipynb) — the complete analysis with saved outputs.
- [Short report](reports/final_report.md) — the findings and limitations.
- [Presentation notes](reports/presentation.md) — a one-minute explanation and five questions with answers.
- [Checks and corrections](reports/verification.md) — details behind the data-quality findings.
- [Results](results/) and [figures](figures/) — the exported tables and charts.

`analysis.ipynb` is my earlier working notebook. Use `final_analysis.ipynb` for the final results.

## Run the notebook in Google Colab

[Open the final notebook in Colab](https://colab.research.google.com/github/lyudmilashamina/roundabouthd-analysis/blob/main/final_analysis.ipynb), then select **Runtime → Run all**. If the repository is private, sign in and allow Colab to access it.

The notebook loads only the annotation files it needs. It does not download the full 8 GB dataset or videos. Everything runs in the cloud; no dataset download to my computer is needed. If the full archive is already in the Colab session, the notebook can reuse it.

Generated files are saved under `/content/analysis_results/final`. Colab storage is temporary, so save the notebook back to GitHub if you want to keep new notebook outputs. The results already included in this repository can be read without rerunning the analysis.

## Sources

- [RoundaboutHD dataset — University of Bath](https://researchdata.bath.ac.uk/1574/)
- [Authors' GitHub repository](https://github.com/siri-rouser/RoundaboutHD)
- [RoundaboutHD paper](https://arxiv.org/html/2507.08729v2)
- [Authors' multi-camera annotation script](https://github.com/siri-rouser/multi_camera_tracking_labelling_tool/blob/main/MCVT_data_creation.py)
