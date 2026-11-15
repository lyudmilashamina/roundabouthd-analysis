# RoundaboutHD analysis

A reproducible analysis of **annotation coverage**, camera observations, and data quality. The final materials are in English and designed for a short student presentation.

## Start here

- **[Final notebook](final_analysis.ipynb)** — clean execution order, source loading, validation, three figures, and an exploratory Friedman test.
- **[Short report](reports/final_report.md)** — the main findings and limitations.
- **[Presentation notes](reports/presentation.md)** — a one-minute script and five Q&A answers.
- **[Verification and corrections](reports/verification.md)** — what was checked and what remains unresolved.
- **[Results](results/)** and **[figures](figures/)** — generated tables and exportable SVG charts.

`analysis.ipynb` is the original exploratory notebook. It is preserved for history and contains superseded narrative claims and redundant cells. Use `final_analysis.ipynb` for the final analysis and presentation.

## Run entirely in the cloud

In Google Colab, choose **File → Open notebook → GitHub**, select this repository and the branch containing the final notebook, and open `final_analysis.ipynb`. A private repository requires authorization in Colab. Run all cells in order.

The notebook retrieves selected annotations from the University of Bath ZIP using verified HTTP byte ranges. **It does not download the complete 8 GB archive or any videos.** If `/content/RoundaboutHD.zip` already exists, it reuses that archive. If range requests are unsupported, it stops rather than silently downloading the full dataset. Nothing is automatically downloaded to your computer or mounted from Drive.

On Colab, inputs are cached in `/content/roundabouthd_annotations` and outputs are saved in `/content/analysis_results/final`. These locations are temporary runtime storage. Save the notebook back to GitHub to preserve updated notebook outputs; generated standalone files require separate persistence if changed.

The standard analysis libraries are normally available in Colab. If imports fail, install `requirements.txt` in the runtime. Outside Colab, use a Python environment with `pip install -r requirements.txt`; the notebook uses `data/raw/` as its annotation cache and writes output folders in the working directory. A restart-and-run-all validation also needs `nbclient` and `ipykernel`.

## What is being measured?

- One MC row is an annotation, not a distinct vehicle or video frame.
- The analyzed MC file has 311 global IDs. They are not a verified census of all road traffic.
- SCT IDs are local to each camera and may represent fragmented tracks. Their sum is not a global vehicle count.
- Annotated frame time is the number of unique annotated frames divided by 15 FPS. It differs from elapsed first-to-last observation span and travel time.
- Counts include only the analyzed annotations. The reason camera 3 has the most included IDs remains unresolved.
- The Friedman test uses the same 74 global IDs in all four cameras. It is exploratory; dependence between vehicles and matched-subset selection limit generalization.

## Quality and scope findings

The notebook keeps raw records, exports the conflicting rows, and uses unique camera–vehicle–frame keys for counts. It distinguishes raw rows from unique observations in both SCT and MC. Missing input files cause explicit errors rather than silently becoming zeros.

The four targeted missing-box examples are found in SCT and detection GT but do not have matching MC boxes at the audit threshold. This does not prove why they were excluded. The audit threshold is a geometric comparison rule, not a threshold used by the authors' association pipeline. No detector precision or recall is claimed.

The archive workbook has four camera-specific sheets. Source filenames differ from examples in the README: the archive uses `Multi_CAM_Ground_Turth.txt` and `imagesc00x/SCT/SCT_GT.txt`. The notebook handles these names and records exact paths and SHA-256 hashes in `results/source_manifest.json`.

## Sources

- [University of Bath dataset, DOI 10.15125/BATH-01574](https://researchdata.bath.ac.uk/1574/)
- [Author repository](https://github.com/siri-rouser/RoundaboutHD)
- [Paper, version 2](https://arxiv.org/html/2507.08729v2)
- [Published association-file creation script](https://github.com/siri-rouser/multi_camera_tracking_labelling_tool/blob/main/MCVT_data_creation.py)

Source videos and full annotation files are excluded from Git. The repository contains the notebook, small derived tables, report, and figures.
