# CI Rehab Analysis Pipeline

This project contains a full data analysis pipeline for the CI Rehab voice cloning discrimination experiment.

## Overview

The project includes two notebooks:

- `analysis.ipynb`: core five-stage pipeline
- `extended_analysis.ipynb`: grouped analyses by institution, familiarity, demographics, topic, AI familiarity, auditory sensitivity, and recording equipment

The core pipeline in `analysis.ipynb` follows five stages:

1. Data ingestion and validation
2. Feature engineering
3. Accuracy analysis and signal detection theory (SDT) metrics
4. Consistency analysis
5. Factor analysis (exploration + statistical modeling)

## Data Layout

The notebook expects a `Data/` directory in the project root.

Expected files per participant (`P026` to `P050`):

- `AI_VoiceTask_<PID>_results.csv`
- `AI_VoiceTask_<PID>_survey.json`
- `AI_VoiceTask_<PID>_checkpoint.json`

Ground truth rule used in the analysis:

- `Model == 1` -> human recording (`IsAI_true = 0`)
- `Model in {2, 3}` -> AI clone (`IsAI_true = 1`)

## Environment (uv)

This project uses `uv` for environment and dependency management (`pyproject.toml`).

### 1) Sync dependencies

```bash
uv sync
```

### 2) Start Jupyter

```bash
uv run jupyter notebook
```

Then open `analysis.ipynb` and run all cells from top to bottom.

## Outputs

`analysis.ipynb` exports summary tables to a timestamped run directory:

- `outputs/runs/<YYYYMMDD_HHMMSS>/`

Each run contains:

- `per_participant_accuracy.csv`
- `sdt_per_participant.csv`
- `consistency_per_participant.csv`
- `accuracy_by_speaker.csv`
- `accuracy_by_model.csv`
- `accuracy_by_confidence.csv`
- `accuracy_by_replaycount.csv`
- `survey_criteria.csv`

For convenience, `outputs/latest` is also updated to point to the latest run
(as a symlink when supported, otherwise as a copied directory).

`extended_analysis.ipynb` exports to:

- `outputs/runs/extended_<YYYYMMDD_HHMMSS>/`

For convenience, `outputs/latest_extended` is updated to the latest extended run.

## Quick Run Checklist

1. Ensure `Data/` is available and points to the dataset directory.
2. Run `uv sync`.
3. Run `uv run jupyter notebook`.
4. Execute all cells in `analysis.ipynb` and/or `extended_analysis.ipynb`.
5. Check `outputs/latest` or `outputs/latest_extended` for result tables.
