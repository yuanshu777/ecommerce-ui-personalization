# E-commerce UI Personalization Impact Analysis

[![Python](https://img.shields.io/badge/Python-3.10+-3776AB)](https://www.python.org/)
[![ML](https://img.shields.io/badge/Modeling-Logistic%20%2B%20XGBoost-0EA5E9)](#)
[![Stats](https://img.shields.io/badge/Inference-A%2FB%20Style-16A34A)](#)

A product analytics project evaluating whether non-default UI variants increase high-intent user behavior in e-commerce sessions.

## TL;DR
- Session-level sample: **100,282 sessions**.
- Control (default UI) high-intent conversion proxy: **4.5577%**.
- Treatment (non-default UI) conversion proxy: **7.8789%**.
- Uplift: **+3.3212 percentage points** (about **+72.9% relative lift**).
- Two-proportion z-test: **z = 13.65, p < 0.001**.

## Business Question
Do non-default/personalized UI variants produce measurable engagement uplift compared with the default interface?

## Why This Matters
If uplift is robust, product teams can prioritize:
- rollout sequencing for high-performing variants,
- follow-up randomized experimentation,
- guardrail monitoring to avoid UX regressions.

## Data
- File: `data/session_level.parquet`
- Unit of analysis: session-level behavioral summary
- Key fields:
  - `ui_group`
  - `converted_hi`
  - `n_events`
  - `session_duration_sec`
  - `is_non_default`
  - `is_bounce`

## Methodology
1. Build/validate session-level analysis table.
2. Define `default` as control and non-default variants as treatment.
3. Compare conversion proxy rates with two-proportion z-test.
4. Run variant-level diagnostics and sensitivity checks.
5. Fit follow-up predictive models (Logistic Regression + XGBoost) for robustness and interpretation support.

Detailed rationale: `docs/analysis_design.md`.

## Key Findings
| Metric | Default UI | Non-default UI |
|---|---:|---:|
| High-intent conversion proxy | 4.5577% | 7.8789% |
| Sample size | 91,866 | 8,491 |

Interpretation: non-default variants are associated with materially higher high-intent behavior in this observational dataset.

## Repository Structure
```text
ui_ds-main/
  README.md
  docs/
    analysis_design.md
  notebooks/
    00_project_overview.ipynb
    01_eda1.ipynb
    02_ab_experiment1.ipynb
    03_variant_level_analysis1.ipynb
    04_modeling1.ipynb
  data/
    session_level.parquet
```

## Reproducibility
```bash
python -m venv .venv
# Windows
.\.venv\Scripts\activate
pip install -r requirements.txt
jupyter notebook
```

Run notebooks in order: `00_project_overview -> 01_eda1 -> 02_ab_experiment1 -> 03_variant_level_analysis1 -> 04_modeling1`.

## Limitations
- Observational logs, not randomized assignment.
- Possible allocation and selection bias.
- Conversion is a proxy metric (`selectSize`, `miniCart`-style intent), not checkout completion.

## Recommended Next Step
Run a controlled randomized A/B test for top-performing variants, with guardrails on bounce and session quality.
