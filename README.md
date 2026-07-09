# One Capability or Many? — Testing the Economic Validity of Frontier AI Benchmarks
**Student ID: 240020141** · Department of Statistics, LSE · ME315 Assessed Coursework

Reproducibility bundle for the submitted paper. All results trace to the SHA-256-pinned data snapshots
via a single Jupyter notebook.

## Folder layout
```
aa_benchmark_validity/
├── README.md                     # this file
├── GITHUB_SETUP.md               # how to publish this bundle + compile on Overleaf
├── requirements.txt              # pinned Python environment
├── paper/                        # LaTeX source (compile on Overleaf with pdfLaTeX)
│   ├── paper_singlecol.tex       # single-column build (NeurIPS-like)
│   ├── paper_twocol.tex          # two-column build (ICML/IEEE-like)
│   ├── frontmatter.tex body.tex appendix.tex   # shared content
│   ├── thebibliography.tex references.bib       # references (embedded + BibTeX)
│   ├── alg_lobo.tex tab_*.tex    # algorithm box and result tables
│   ├── STYLE_SPEC.md LINT_REPORT.md             # style decisions + structural lint
│   └── references.json           # 21-entry reference list (source of the .bib)
├── notebook/
│   └── ME315_240020141.ipynb     # single notebook: extraction, EDA+Task1, Task2, all figures
├── data/
│   ├── raw/                      # timestamped, SHA-256-pinned source snapshots = THE SUBMITTED DATASET
│   │   ├── aa_leaderboards_models_snapshot.html
│   │   ├── epoch_notable_ai_models_snapshot.csv
│   │   ├── aa_snapshot_manifest.json / epoch_snapshot_manifest.json
│   │   └── aa_models_raw_parsed.csv               # all 548 configs, flattened
│   └── processed/                # analysis set + every result table (see below)
│       ├── aa_analysis_models.csv                 # n=421 analysis-ready dataset
│       ├── loadings_raw.csv / loadings_residualised.csv
│       ├── task1_structure_results.json / hypothesis_adjudication.csv / parallel_analysis.csv
│       ├── cluster_validation.csv / model_cluster_profiles.csv / benchmark_hclusters.csv
│       ├── lobo_rung_summary.csv / lobo_metrics_full.csv / h4_bootstrap_dmse.csv
│       ├── lobo_hyperparameters.csv (+ _full.csv) / task2_prediction_results.json
│       ├── task2_explainability.csv / task2_shap_gdpval.csv / task2_error_analysis_gdpval.csv
│       └── density_audit.csv / overlap_matrix.csv / benchmark_taxonomy.csv
├── figures/
│   ├── fig1_eda.png fig2_loadings.png fig3_clusters.png fig4_prediction.png fig5_diagnostics.png
│   ├── fig1_eda … fig5_diagnostics.png            # five main-text figures
│   ├── suppl_scree_parallel.png suppl_benchmark_dendrogram.png suppl_eda_distributions.png appxfig_density.png  # appendix figures
│   └── figA1_scree.png figA2_dendrogram.png fig_eda_distributions.png fig_phase1_density.png  # notebook-generated source renders
└── PHASE{1,2,3}_REPORT.md        # per-phase methodology and adjudication records (working notes)
```

## Reproducibility
Open `notebook/ME315_240020141.ipynb` and run all cells. It reproduces the entire pipeline from the pinned
snapshots in `data/raw/` — extraction and the coverage gate, EDA, the Task-1 structure analysis, and the
Task-2 LOBO prediction — regenerating every figure (`figures/`) and result table (`data/processed/`).
No live network call or model re-run is required; all randomness is seeded. Runtime ≈ 20 s on the fast path
(`FULL=False`); set `FULL=True` to sweep all four learners in the LOBO loop.

**GitHub:** the complete bundle will be released at
`https://github.com/Looloo-dot/frontier-ai-economic-validity` (linked in the appendix).

## Data provenance (transparency)
| Source | URL | License | Role | Snapshot (UTC) |
|---|---|---|---|---|
| Artificial Analysis — Models Leaderboard | https://artificialanalysis.ai/leaderboards/models | site terms; public page | Dense core (scores) | 2026-07-06 |
| Epoch AI — Notable AI Models | https://epoch.ai/data/notable_ai_models.csv | CC-BY 4.0 | Periphery / compute metadata | 2026-07-06 |

Every downstream number traces to the pinned raw snapshots via `notebook/ME315_240020141.ipynb`.
The AA Data API requires a key (HTTP 401); the notebook uses the public-page extraction route and stores
the exact bytes so results are stable regardless of live-page drift.

## Dataset at a glance
- **548** model configurations parsed → **421** retained (≥8 of 13 kept benchmarks).
- **12 primary benchmarks** across 5 taxonomy blocks (Economic, Academic, Scientific-coding,
  Long-context, Instruction-following); MMMU-Pro held for sensitivity; APEX-Agents dropped (<60 models).
- Economic-dense subset: **103** models carry GDPval Elo + Terminal-Bench v2.1 + τ³-Banking (Task-2 grid).

## Status
- [x] **Phase 1** — extraction, access & licensing audit, density gate → **PASS**
- [x] **Phase 2** — EDA + Task-1 unsupervised structure (PCA / ML-EFA / clustering; date residualisation)
      → **RQ1 adjudicated**: H1 supported (74.5%), H2(i) supported (logistic-fit date-R²=0.505; OLS 0.477), H2(ii) not met
      (14.9pp < 15pp), H3 supported under over-extraction (PA retains k=1). See `PHASE2_REPORT.md`.
- [x] **Phase 3** — Task-2 predictive validity (LOBO regression, nested 5×5 CV, 4 learners)
      → **H4 SUPPORTED**: k-factor beats single mean-index on pooled economic block (ΔMSE +0.037,
      95% CI [+0.019,+0.055]) and 3/4 economic columns; far larger gain over date/scale. See `PHASE3_REPORT.md`.
- [x] **Phase 4** — paper written as **LaTeX** in two column layouts (`paper_singlecol.tex`,
      `paper_twocol.tex`) sharing one body, appendix, and bibliography. Times New Roman via newtx,
      clickable numeric citations via hyperref, booktabs tables, one-per-line equations. Byline
      **Student ID: 240020141** only. Structure: title + abstract, ToC + lists, body (intro→conclusion),
      references, appendix (math derivations, coverage audit, hyperparameter grid, robustness, provenance,
      supplementary figures). Compile on Overleaf with pdfLaTeX (see `GITHUB_SETUP.md`).

## Deliverables for submission
1. `paper/paper_singlecol.tex` and `paper/paper_twocol.tex` — the manuscript in both layouts, with
   shared `body.tex`, `appendix.tex`, `frontmatter.tex`, `thebibliography.tex`, `references.bib`, and
   float files. Compile with pdfLaTeX on Overleaf.
2. `notebook/ME315_240020141.ipynb` — the single consolidated notebook, with all outputs and figures
   rendered inline.
3. `data/raw/` — SHA-256-pinned data snapshots (the dataset); `data/processed/` — all result tables.
4. `PHASE{1,2,3}_REPORT.md` — per-phase methodology and adjudication records (supporting working notes).
