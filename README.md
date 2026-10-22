# Computer Vision - Project 3

NYU Tandon, CS-GY 6643, Fall 2026.

## Notebooks

- `Q1to3Solution.ipynb`: Questions 1-3 together: CNN feature visualization, multi-car
  speed estimation, and person/dog tracking. Currently a scaffold; implementation pending.
- `PenaltyKickPrediction.ipynb`: Q4 Kaggle competition, including all exploration,
  download/audit utilities, scoring, and submission checks. Current scope is Phase 0;
  no models have been trained and data access still requires Kaggle authentication.

All solution code lives in the notebooks themselves. There are no external project
Python helpers to import, and neither notebook depends on the other. Keep code small,
readable, and organized with explanations and outputs beside the relevant cells.

## Workspace

- `Data/`: immutable competition inputs.
- `outputs/`: figures, audit reports, experiment log, and later model artifacts.
- `Kaggle Submissions/`: candidate CSVs when authorized.
- `AGENTS.md`, `DATA_SOURCES.json`, `AI_USAGE.md`: instructions, provenance, disclosure.

## Environment

Python 3.12 with the project-local environment:

```bash
python3.12 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
python -m pip install -r requirements-setup.txt  # optional download/PDF tools
python -m ipykernel install --sys-prefix --name cv-project3 --display-name "Python (CV Project 3)"
```

Select **Python (CV Project 3)** in VS Code and run the relevant notebook from top to
bottom. The Kaggle notebook includes inline synthetic metric/submission checks.

Configure Kaggle credentials privately before enabling its optional download cell.
`RUN_DOWNLOAD` defaults to `False`; use `LIST_ONLY = True` to verify access first,
then `LIST_ONLY = False` to download. Input files are never overwritten. Enable video
decoding/hashing in the audit cell only as needed. Leave `SUBMISSION_PATH = None`
until a real candidate exists; validation requires the actual official template and
metadata. No Kaggle upload is authorized.

**Documentation policy:** leave this README unchanged until final delivery unless
explicitly requested. Keep interim status and decisions in `AGENTS.md`.
