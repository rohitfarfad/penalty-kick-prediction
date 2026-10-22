# AI assistance record

2026-10-22: Codex assisted with Phase 0 workspace inspection, Python environment setup,
reading and visually checking course PDF pp. 8-12, exact-competition access checks,
dependency declarations/lock, documentation, notebook scaffold, downloader, read-only
audit utility, published metric implementation, submission validator, and tests.
No model was trained, no private data labeled, no predictions generated for the
competition, and no Kaggle submission uploaded. Synthetic test labels are temporary
software fixtures only.

Access limitations and unmeasured statistics are recorded in `AGENTS.md`.
The original course PDF is unchanged. Credentials were checked for presence only.

The course requires a shareable link or PDF of the LLM conversation with the final
submission. This file is an assistance summary and does **not** satisfy that export
requirement by itself. User action at final delivery: export/share this conversation
and attach the resulting link or PDF. No fabricated chat-history artifact is provided.

## 2026-10-22 - Simplify layout to match previous projects

User request: "This project structure is too verbose, check the code repo for the
previous projects and refactor this one accordingly, check and refactor the AGENTS.md
file especially to closely match the previous projects, especially the rules on code,
refactor the project structure to simplify like these two projects" followed by the
Project 2 and constellation-detector GitHub links.

Codex inspected both GitHub root listings, instruction files, and dependency conventions,
and compared the local copies. Adopted root notebooks/helpers, `Data/`, `outputs/`,
`Kaggle Submissions/`, pinned requirements files, and small readable code. Consolidated
status in `AGENTS.md`, provenance in `DATA_SOURCES.json`, and disclosure here. Preserved
initial evidence under `outputs/setup/phase0_notes/`, original PDF bytes, and existing
checks. No previous project was modified; no model training, competition predictions,
or Kaggle upload occurred. Old project-specific restrictions were not imported.

Refactor validation: 30 tests passed, one real-template integration test skipped;
the root notebook executed in a fresh project-local kernel, and dependency checks,
original PDF checksum, and Git exclusions passed.

## 2026-10-22 - Two notebooks, all solution code inline

User request: "We will keep the solution to first 3 questions in on notebook and
solution of the kaggle competition in saperate one, all the code should be in the
notebook itself, don't make extra python files for the solution, name them according
to the previous projects".

Created `Q1to3Solution.ipynb` with Q1-Q3 headings/descriptions only. Kept
`PenaltyKickPrediction.ipynb` for Q4, moving all existing download, audit, metric,
submission validation, and lightweight checks into its cells. Removed the five root
Python files after preserving them in an ignored historical ZIP. Updated persistent
instructions to prohibit external solution/helper Python files and cross-notebook
runtime dependencies. This replaces the previous helper-file convention. No question
was solved, model trained, private label inferred, or Kaggle submission uploaded.

Validation: both notebooks checked independently in fresh kernels; all 11 Q4 code
cells and inline checks passed. Notebook-defined functions passed the 30 preserved
regression cases, with the official-template case skipped because data is unavailable.
No external project-code imports or root Python files remain.

## 2026-10-22 - Git ignore rules

Updated `.gitignore` to exclude official inputs and generated outputs/submissions,
including common data exports, media, arrays, weights, archives, caches, and secrets.
Retained notebook code, documentation, provenance, requirements, editor settings,
the original course PDF, and `.gitkeep` markers for the directory structure.
