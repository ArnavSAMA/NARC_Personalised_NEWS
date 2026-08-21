# Dead / archived backend code

Nothing in this folder is imported by the live backend (`server.py` and everything it pulls
in from the repo root). Kept for reference only.

## `main.py`, `api/`, `core/`, `services/`

An earlier FastAPI "walking skeleton" (HCL Hack60 Day-1 scaffold). It imports
`app.core.*` and `app.api.*` / `app.services.*` — there is no `app/` package in this
repo, so **this code cannot run as-is**. Even with the import paths fixed, most of it
is stub logic (`RandomVectorEncoder`, `RandomRetriever`, `RandomBandit` in
`core/registry.py`) that was never wired up to the real models. Superseded by
`server.py` + `rl_env.py`.

Extra dependencies only this code needs: `faiss-gpu`, `mabwiser`, `redis`, `pandas`.
Not required to run the real backend.

## `archived_v1_pipeline/` (`recommender.py`, `news_encoder.py`, `infer6.py`)

An earlier generation of the *working* pipeline, built around the MIND dataset
(256-dim vectors, `news_vectors.pkl`) as described in `DESIGN.md`. Superseded by the
`google_news_5000.json` / 768-dim pipeline described in `PIPELINE_V2.md`.

- `recommender.py` — cosine pre-filter as a standalone module; logic now lives inline
  in `rl_env.py::_candidate_pool`.
- `news_encoder.py` — **currently broken**: imports `VEC_DIM`, `DISTILBERT_DIM`,
  `ENCODER_SEED` from `config.py`, none of which exist in the current `config.py`.
- `infer6.py` — standalone experimental script, not imported by anything.
