# Tribological & Thermal Evaluation of Surface-Textured Automotive Brake Pads

**Author:** Nizam Ahmed (K22016355)  
**Supervisor:** Dr Sorin-Cristian Vlădescu  
**Module:** 6CCE3EEP — Final-Year Engineering Dissertation, King's College London  

MATLAB analysis pipeline for processing Bruker UMT TriboLab rotary pin-on-disc tribometer data from friction and thermal tests on Trimat MN1070 brake-pad specimens with dimpled surface textures.

---

## Repository Structure

```
EEP_Submission_Code/
│
├── Complete_One_Click_Runner.m      ← ENTRY POINT — run this
├── run_brakepad_analysis.m          ← Core pipeline
├── run_additional_visualisations.m  ← Supplementary plots
│
├── brk_default_config.m            ← All configurable parameters
├── brk_import_bruker_csv.m         ← Bruker CSV importer
├── brk_infer_condition.m           ← Texture/environment label inference
├── brk_segment_by_thresholds.m     ← Steady-state segment detection
├── brk_compute_metrics.m           ← μ, ΔT, distance metrics per segment
├── brk_summarise_conditions.m      ← Per-condition aggregation
├── brk_evaluate_success_criteria.m ← Pass/fail evaluation
├── brk_two_way_anova.m             ← Two-way ANOVA + effect sizes
├── brk_plot_summary.m              ← Summary bar charts
├── brk_plot_timeseries.m           ← Time-series diagnostic panels
├── brk_export_figure.m             ← PNG/PDF figure export
├── brk_merge_wear_log.m            ← Optional mass-loss wear data
│
├── TEST1-NOTEXTURE-DRY-REPETITION-25N-1000to800RPM.csv
├── TEST1-NOTEXTURE-WET-REPETITION-25N-1000to800RPM.csv
├── TEST2-ONE-HOLE-TEXTURE-DRY-REPETITION-25N-1000to800RPM.csv
├── TEST2-ONE-HOLE-TEXTURE-WET-REPETITION-25N-1000to800RPM.csv
├── TEST3-TWO-HOLE-TEXTURE-DRY-REPETITION-25N-1000to800RPM.csv
├── TEST3-TWO-HOLE-TEXTURE-WET-REPETITION-25N-1000to800RPM.csv
├── wear_log_template.csv
│
├── analysis_out/                    ← Generated output
│   ├── figures/                     ← PNG + PDF exports of all plots
│   ├── results_perSegment.csv       ← One row per braking repetition (18 rows)
│   ├── results_perCondition.csv     ← Condition-level means ± SD (6 rows)
│   ├── success_criteria.csv         ← Pass/fail evaluation
│   ├── analysis_workspace_core.mat  ← Core variables for quick reload
│   └── analysis_workspace_full.mat  ← Full workspace snapshot
│
├── Initial tests/                   ← Preliminary single-run data (not used in analysis)
│   ├── TEST1-NOTEXTURE-DRY.csv
│   ├── TEST1-NOTEXTURE-DRY-REPETITION.csv
│   └── TEST1-NOTEXTURE-WET-REPETITION.csv
│
└── Misc/                            ← Supporting files
```

---

## Requirements

- **MATLAB R2018b or newer**
- Statistics and Machine Learning Toolbox (for `anovan`)
- No third-party toolboxes required

---

## How to Run

1. Clone or download this repository.
2. Open MATLAB and navigate to the `EEP_Submission_Code/` folder.
3. Run:
   ```matlab
   Complete_One_Click_Runner
   ```
   This verifies all required files are present, then executes the full pipeline.
4. All outputs are written to `analysis_out/`. Pre-computed results from the dissertation are already included in that folder.

---

## Pipeline Overview

The pipeline processes six Bruker CSV files (3 texture configurations × 2 environments), each containing 12 steps from 3 braking repetitions. It automatically:

1. **Imports** raw CSV data, handling Bruker-specific encoding and metadata (track radius, step numbering).
2. **Segments** each file into 3 braking events using load/speed thresholds.
3. **Computes** per-segment metrics: mean friction coefficient (μ), temperature rise (ΔT), sliding distance, nominal contact pressure.
4. **Aggregates** segment-level results into condition-level statistics (mean ± SD across repetitions).
5. **Evaluates** against dissertation success criteria (|Δμ| ≤ 5 % vs flat baseline; wear reduction ≥ 15 %).
6. **Performs** two-way ANOVA (texture × environment) with partial η² and Cohen's f effect sizes.
7. **Exports** all figures (PNG at 300 DPI + vector PDF) and result tables (CSV).

---

## Test Parameters

| Parameter | Value |
|-----------|-------|
| Normal load | 25 N |
| Speed range | 1000 → 800 RPM |
| Track radius | 0.1298 m (from Bruker metadata) |
| Specimen area | 10 × 10 mm |
| Repetitions per condition | 3 |
| Dimple diameter | 2 mm |
| Dimple depth | ~1.5 mm |
| Friction material | Trimat MN1070 |

---

## Licence

This repository accompanies an academic dissertation and is provided for examination and reproducibility purposes.
