# Evaluating Multi-Variant UI Personalization on E-commerce Engagement

## Project Summary
This project evaluates whether non-default UI variants improve high-intent engagement behavior compared with the default e-commerce UI.

## Business Question
Do personalized/non-default UI variants produce measurable uplift in conversion-proxy behavior?

## Dataset
- `data/session_level.parquet`
- Session-level table with 100,282 sessions and 11 columns
- Core fields: `ui_group`, `converted_hi`, `n_events`, `session_duration_sec`, `is_bounce`

## Methodology
- Event-to-session aggregation and quality checks
- Default vs non-default treatment split
- Two-proportion z-test for conversion-proxy uplift
- Variant-level comparisons
- Follow-up predictive modeling (logistic + tree-based workflows)

## Key Findings
- Default conversion proxy: **4.5577%**
- Non-default conversion proxy: **7.8789%**
- Two-proportion z-test: **z = 13.65, p < 0.001**

Interpretation: non-default variants show significant uplift in high-intent behavior in observational logs.

## Repository Contents
- `docs/analysis_design.md`: experiment and metric rationale
- `notebooks/00` to `04`: complete analysis pipeline
- `data/session_level.parquet`: analysis-ready session dataset

## How to Reproduce
```bash
python -m venv .venv
# Windows
.\.venv\Scripts\activate
pip install -r requirements.txt
jupyter notebook
```

Run notebooks in order from `00_project_overview.ipynb` to `04_modeling.ipynb`.
