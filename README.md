# ECON 5560: Individual replication repository

GitHub account: **matthew-suban-slo**. This is Matthew Suban's individual version-control assignment using Team 3's existing replication project. Repository: https://github.com/matthew-suban-slo/econ5560-replication-suban.

## Paper and scope

Eppink, Florian V., Matthew Winden, Will C. C. Wright, and Suzie Greenhalgh. 2016. "Non-Market Values in a Cost-Benefit World: Evidence from a Choice Experiment." *PLOS ONE* 11(10): e0165365. https://doi.org/10.1371/journal.pone.0165365.

The paper studies whether monetary information changes New Zealand councillors' and council staff's choices over development, water quality, and cultural heritage. This package runs the team's Python replication from the authors' unchanged Stata data through sample construction, descriptive tables, conditional logit, mixed logit and sensitivity analysis, an offline dashboard, slide figures, paper exhibits, and discrepancy checks. The master runs all eight stages without manual intervention or a saved workspace. It does not download data or install packages during analysis.

## Data source

The data are the authors' public **S1 Table: Choice experiment responses**, linked from the article's Supporting Information. Direct URL: https://journals.plos.org/plosone/article/file?id=10.1371/journal.pone.0165365.s001&type=supplementary. I downloaded the file again on **November 8, 2026** for this package and verified that it is byte-identical to the existing team copy. The team's historical download date is unknown. The unchanged file is `data/raw/S1Table.DTA`; its checksum and attribution appear in [DATA_SOURCE.md](DATA_SOURCE.md). It is approximately 5.3 MB, below the assignment's 50 MB limit. The raw file has 2,160 rows and 180 respondents; the complete-choice analytical sample has 1,968 rows and 164 respondents, including 123 councillors (1,476 rows).

## Exact commands after cloning

Use **Python 3.12** and a terminal. No R, Stata, Jupyter, or internet connection is needed for the pipeline after the Python packages are installed. From a new working folder on macOS or Linux:

```bash
git clone https://github.com/matthew-suban-slo/econ5560-replication-suban.git
cd econ5560-replication-suban
python3.12 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
mkdir -p logs
python run_all.py > logs/run_log.txt 2>&1
python -m pip freeze > logs/requirements.txt
```

On Windows PowerShell, replace virtual-environment setup and activation with `py -3.12 -m venv .venv` and `.\.venv\Scripts\Activate.ps1`, create logs with `New-Item -ItemType Directory -Force logs`, and run `python run_all.py *> logs\run_log.txt`. Then run `python -m pip freeze > logs\requirements.txt`. The Windows command is provided for portability; this submission's recorded verification was on macOS.

For the assignment's fresh-clone check, delete everything **inside** `outputs/` before running. The scripts recreate every required subdirectory. Start the terminal command in a new Python process, not an interactive notebook or a restored IDE session. `run_all.py` resolves data, code, and output locations relative to itself and starts each stage in a fresh subprocess. It exits with an error if a stage fails, verifies the raw checksum and essential output invariants, and appends software/environment information as its final 20 lines. Inspect `logs/run_log.txt` before trusting a run. The commit recorded in the log identifies the source checked out before outputs/logs were committed.

## Software and packages

The verified environment uses Python **3.12.12** on macOS. Direct requirements are pinned in `requirements.txt`: NumPy **1.26.4**, pandas **2.3.3**, SciPy **1.13.1**, statsmodels **0.14.6**, and Matplotlib **3.9.4**. Their exact observed versions appear at the end of the run log; `logs/requirements.txt` is the actual `python -m pip freeze` output, including transitive packages. To recreate the recorded full package set, install from that file instead of the direct requirements. A virtual environment keeps these separate from other coursework.

The walkthrough notebook is optional and is not needed by `run_all.py`; install `requirements-notebook.txt` to use it. The optional independent R check requires R and `survival`; run `Rscript scripts/crosscheck_clogit.R` after the Python pipeline. This optional check is outside the recorded Python run and is not claimed as newly verified here.

## Runtime and fresh-clone evidence

The verified full run took **532.00 seconds (8 minutes 52 seconds)** on macOS 27.0.1 arm64 with Python 3.12.12 and regenerated **39 output files**. Both primary mixed-logit models converged; the log contains no warnings or errors. The completed run's elapsed seconds, source commit, completion timestamp, output count, and validation results are recorded in `logs/run_summary.json` and the final 20 log lines. The full mixed-logit sensitivity analysis is included (2,000 primary draws, plus twenty 500-draw fits per sample), so runtime depends on CPU speed and can take several minutes. `logs/FRESH_CLONE.md` records the measured runtime and the exact fresh-clone procedure after verification. Every committed result in `outputs/` is regenerated from raw data during that run; no previous results are used as inputs.

## Files and outputs

- `run_all.py`: master entry point, stage execution, output validation, timing, and environment summary.
- `requirements.txt`: pinned direct Python dependencies for the complete pipeline.
- `requirements-notebook.txt`: optional notebook dependencies, not required for the pipeline.
- `README.md`: citation, provenance, commands, environment, runtime, results, and limitations.
- `DATA_SOURCE.md`: original download URL, retrieval date, raw checksum, and attribution.
- `SOURCE_PROVENANCE.md`: upstream code attribution and packaging changes.
- `FILES.md`: one-line inventory of every committed project file.
- `data/raw/S1Table.DTA`: unchanged author-provided raw data.
- `scripts/common.py`: shared paths, published comparison numbers, and estimators.
- `scripts/01_parse_data.py`: parse the raw file, reconstruct samples, and create analysis variables.
- `scripts/02_descriptives.py`: respondent characteristics, card response counts, and treatment choice rates.
- `scripts/03_conditional_logit.py`: Table 3 models 1 and 2, card-pooled and respondent-choice specifications.
- `scripts/04_mixed_logit.py`: Table 3 models 3 and 4, primary and sensitivity estimates, and posterior effects.
- `scripts/05_build_dashboard.py`: build an offline HTML dashboard from newly estimated results.
- `scripts/06_slide_figures.py`: generate presentation figures from the current run's results.
- `scripts/07_paper_figures.py`: rebuild all five paper exhibits and side-by-side comparisons.
- `scripts/08_debug_discrepancies.py`: compute evidence about unmatched published cells.
- `scripts/crosscheck_clogit.R`: optional independent conditional-logit cross-check.
- `scripts/replication_walkthrough.ipynb`: optional narrated team analysis, with saved execution state cleared.
- `scripts/REPLICATION_LOG.md`: historical team decisions and hypotheses; see the qualifications below.
- `scripts/dashboard/template.html`: source template used by the dashboard builder.
- `scripts/replication-targets/`: original published exhibit reference images and their guide.
- `outputs/data/`: parsed choice rows, respondent data, design cards, and sample-flow information.
- `outputs/tables/`: descriptive, coefficient, comparison, and discrepancy CSV tables.
- `outputs/results/`: machine-readable descriptive and model results.
- `outputs/figures/`: regenerated descriptive, posterior-effect, and sensitivity figures.
- `outputs/slides/`: regenerated presentation figures.
- `outputs/paper_figures/`: recreated published exhibits, numerical comparisons, and side-by-side images.
- `outputs/dashboard/index.html`: generated dashboard; open directly in a browser.
- `logs/run_log.txt`: captured stdout and stderr from the complete fresh-clone run.
- `logs/requirements.txt`: exact package freeze from the verification environment.
- `logs/run_summary.json`: timing, software versions, validation results, and convergence flags.
- `logs/output_sha256.txt`: checksums of the regenerated outputs.
- `logs/steps/01_parse_data.log`: parsing and sample-construction diagnostic log.
- `logs/FRESH_CLONE.md`: verification procedure and measured runtime.
- `.gitignore`: excludes local environments, Python caches, and operating-system files.

Open `outputs/tables/table3_cl.csv`, `outputs/tables/table3_ml.csv`, and `outputs/tables/discrepancy_diagnosis.csv` for model comparisons. All five published exhibits are recreated under `outputs/paper_figures/`; `outputs/dashboard/index.html` presents the same newly generated results interactively without a server.

## What does not reproduce exactly

A successful pipeline run means the package executes and regenerates outputs; it does not mean every published estimate matches. The team's code reproduces the reported sample sizes and compares each published table entry against its reconstruction. Conditional-logit results match much more closely when choices are pooled by design card, whereas the conventional person-by-card specification yields materially different magnitudes and uncertainty. The authors' original analysis code is unavailable in this package, so this numerical match does not establish their exact implementation.

Several published conditional-logit cells and the town-size descriptive shares do not match the reconstruction. `outputs/tables/discrepancy_diagnosis.csv` records numerical evidence for possible reporting or sample-history explanations. These are hypotheses, not confirmed author errors; compatibility with a larger sample denominator does not establish that such a sample existed. Some historical team prose and chart labels are more categorical and should be read with this qualification.

Mixed-logit coefficients and inference depend on the simulated integration draws and optimizer behavior. Fixed seeds make our implementation repeatable within the recorded software environment, but do not reproduce Stata's unpublished draw sequence or guarantee identical floating-point results on other systems. The package reports primary fits, convergence flags, and a 20-seed sensitivity range. Published Figure 2 does not align fully with the described model; the code provides both model-based variants for comparison. We have not verified the original Stata implementation, contacted the authors, or resolved the publication's undocumented analysis choices. See the recorded convergence flags for numerical limitations in this particular run.

## Attribution and AI assistance

The analysis is based on Team 3's existing ECON 5560 replication code, not a new claim of sole authorship. [SOURCE_PROVENANCE.md](SOURCE_PROVENANCE.md) identifies the upstream project and inherited materials. AI assistance (OpenAI Codex) materially helped inspect the assignment, package the existing pipeline, make paths portable, pin dependencies, prepare documentation, run and inspect fresh-clone verification, and prepare the Canvas submission text. The statistical estimators and published comparison targets are inherited from the team project; packaging verification does not independently certify every methodological interpretation.
