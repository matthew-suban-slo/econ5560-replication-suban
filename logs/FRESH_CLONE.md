# Fresh-clone verification

Verified on November 8, 2026 (America/Los_Angeles); completed UTC 2026-11-09T03:52:46.761615+00:00. GitHub account used for repository creation, clone, commits, and push: `matthew-suban-slo`.

1. Pushed the final source and dependency pins as commit `29a17829b4ada0b02c78c4d86b170207b983e837`.
2. Cloned `https://github.com/matthew-suban-slo/econ5560-replication-suban.git` into the new folder `/Users/star/replication-verification/econ5560-suban-final-fresh-20261108`, separate from the development folder. The destination did not previously exist.
3. Deleted the sole tracked placeholder inside `outputs/` and verified the directory was empty. No prior generated outputs were copied in.
4. Created a new environment with `uv venv --python 3.12 --seed .venv` and installed this clone's pinned `requirements.txt` with `uv pip install --python .venv/bin/python -r requirements.txt`. `python -m pip check` reported no broken requirements.
5. Started a new Python interpreter from the terminal in the fresh clone, with no restored workspace: `.venv/bin/python run_all.py > logs/run_log.txt 2>&1`. Each analysis stage also ran in its own subprocess. The command exited **0**.
6. Ran `.venv/bin/python -m pip freeze > logs/requirements.txt` in that same environment.
7. Read the complete captured log and checked for tracebacks, errors, and warnings: none were present. All eight stages finished. The master validated samples, one selected alternative per complete choice occasion, finite numeric model tables, all five recreated exhibits, and dashboard data injection. Both primary mixed-logit convergence flags were true. The recorded output manifest was independently checked against every regenerated output file.
8. Committed and pushed the regenerated outputs and captured logs from this fresh clone, with documentation of the observed runtime and limitations. The source commit in the log intentionally identifies the pre-run source; the subsequent results commit adds generated artifacts and documentation without changing analytical code.

**Measured full runtime:** 532.00 seconds, or 8 minutes 52 seconds. **Regenerated outputs:** 39 files. **Environment:** CPython 3.12.12, macOS 27.0.1 arm64, NumPy 1.26.4, pandas 2.3.3, SciPy 1.13.1, statsmodels 0.14.6, Matplotlib 3.9.4. The package freeze includes the transitive dependencies.

Successful execution does not imply exact reproduction of every published number. The README and discrepancy tables explain the remaining published-cell differences and simulation sensitivity. The optional R cross-check and optional notebook were not run for this verification; the master Python pipeline is complete without them. An earlier NumPy 2.0.2 attempt was stopped after matrix-operation warnings, as documented in SOURCE_PROVENANCE.md; no results or logs from that attempt are presented as the final verified run.
