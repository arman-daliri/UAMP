# Allergen & Fuzzy Deep Learning Analysis

Model benchmarking, explainability, and differential allergen expression analysis for the ICBME project.

## Project structure

```
.
├── data/                                  # input data (not tracked in git — see below)
│   ├── mRMR_30f.csv
│   └── H5AD/
│       └── adata_ranked_proteins.h5ad
├── notebooks/
│   ├── Evaluation.ipynb                   # trains & benchmarks CNN, WHFDL, FDNN, FAE, NF-RVFL
│   ├── Explainability_WHFDL.ipynb         # SHAP & LIME explainability for WHFDL
│   └── Differential_Allergen_Analysis.ipynb  # boxplots, bubble plot, heatmap, volcano plot
├── results/                                # generated outputs (not tracked in git)
├── requirements.txt
└── README.md
```

## Setup

```bash
python -m venv env
source env/bin/activate        # Windows: env\Scripts\activate
pip install -r requirements.txt
```

## Data

Place the following files under `data/` (paths are relative to the repo root):

| File | Used by | Path |
|---|---|---|
| `mRMR_30f.csv` | Evaluation.ipynb, Explainability_WHFDL.ipynb | `data/mRMR_30f.csv` |
| `adata_ranked_proteins.h5ad` | Differential_Allergen_Analysis.ipynb | `data/H5AD/adata_ranked_proteins.h5ad` |

If you keep your data somewhere else, set the `DATA_DIR` environment variable instead of moving files:

```bash
export DATA_DIR=/path/to/your/data     # Windows (PowerShell): $env:DATA_DIR="C:\path\to\your\data"
```

## Running the notebooks

Launch Jupyter from the repo root so the notebooks' relative paths (`../data`, `../results`) resolve correctly:

```bash
jupyter notebook notebooks/
```

Each notebook creates its own subfolder under `results/` for its outputs (model checkpoints, evaluation reports, figures).

## Notebooks

- **Evaluation.ipynb** — trains and evaluates 5 models (CNN, WHFDL, Original FDNN, FAE, NF-RVFL) on the mRMR-selected feature set; writes per-model metrics and a summary comparison report to `results/`.
- **Explainability_WHFDL.ipynb** — trains a WHFDL model and generates SHAP (global) and LIME (local) explanations; writes figures to `results/Explainability/`.
- **Differential_Allergen_Analysis.ipynb** — generates boxplots, a bubble plot, a heatmap, and a volcano plot of differentially abundant allergen proteins (cancer vs. healthy); writes figures to `results/Figures/`.
