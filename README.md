# One Capability or Many? — Testing the Economic Validity of Frontier AI Benchmarks
**Student ID: 240020141** · Department of Statistics, LSE · ME315 Assessed Coursework

Reproducibility bundle for the submitted paper. All results trace to the SHA-256-pinned data snapshots
via a single Jupyter notebook.

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

## Dataset
- **548** model configurations parsed → **421** retained (≥8 of 13 kept benchmarks).
- **12 primary benchmarks** across 5 taxonomy blocks (Economic, Academic, Scientific-coding,
  Long-context, Instruction-following); MMMU-Pro held for sensitivity; APEX-Agents dropped (<60 models).
- Economic-dense subset: **103** models carry GDPval Elo + Terminal-Bench v2.1 + τ³-Banking (Task-2 grid).
