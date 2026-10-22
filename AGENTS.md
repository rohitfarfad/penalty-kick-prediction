# Computer Vision Project 3: project instructions

## 1. Scope and current authorization

NYU Tandon, CS-GY 6643 Computer Vision, Fall 2026. The assignment has Q1-Q3 and
Q4 Penalty Kick Prediction. Current work covers **Q4 Phase 0 only**: setup, data and
competition inspection, validation utilities, and planning. The latest request authorizes
simplifying this workspace to match Projects 1 and 2. No training, baseline fitting,
feature engineering, or competition prediction generation yet. Never upload to Kaggle
without an explicit user instruction. Do not modify the previous projects.

**Latest organization requirement:** keep Q1-Q3 together in `Q1to3Solution.ipynb`
and Q4 separately in `PenaltyKickPrediction.ipynb`, following the previous projects'
naming pattern. All solution code must live in the corresponding notebook itself.
Creating the Q1-Q3 scaffold does not authorize implementing those questions yet.

**Keep code simple and minimal**, following the previous projects:

- Prefer straightforward notebook cells, clear variable names, and a few short functions.
- Do not create solution/helper `.py` files, export code with `%%writefile`, or import
  project code from external files. Keep preprocessing, training, evaluation, inference,
  submission checks, and any download/audit utilities directly in notebook cells.
  Short reusable functions belong in the notebook where they are used.
- Avoid unnecessary classes, frameworks, configuration layers, abstractions, speculative
  fallbacks, elaborate caching, dependencies, and boilerplate. Minimal means readable,
  not compressed or cryptic. Explain meaningful choices briefly.
- Begin with the simplest justified method from relevant course material; add complexity
  only for an observed failure. Review supplied lectures/code before claiming to use
  them. Project 3 lecture sources have not been reviewed in this session.
- Keep each explanation, result, and supporting evidence together in the notebook.
  Put settings in an obvious cell or small dictionary until reuse warrants more.
- Validate real boundaries: input files, labels, splits, and submission schema. Keep
  tests relevant; do not build a framework around trivial notebook cells.
- Reuse small explicit snippets inside each notebook, not another notebook's globals.
  The two notebooks must run independently. Previous projects and lecture files must
  not become runtime dependencies. Installed third-party packages are permitted.

Update `README.md` for this refactor, then leave it unchanged until the solution is
finished and ready to submit, unless the user requests another change. Keep evolving
requirements, decisions, blockers, and status **here**; AI assistance goes in `AI_USAGE.md`.

## 2. Sources and interpretation

Checked 2026-10-22; page references use PDF page numbers.

| Source | Role |
|---|---|
| `Project3_CV_2026_v5.pdf` | Original assignment; full text inspected and Q4 pp. 8-12 visually checked. |
| [Exact Kaggle competition](https://www.kaggle.com/competitions/penalty-kick-prediction-cs-gy-6643/overview) | Intended authority for current platform settings; section text and official files remain unverified. |
| [Project 2 instructions](https://github.com/rohitfarfad/-CV-Cell-Matching-x-Segmentation/blob/main/AGENTS.md) | Reference for minimal code, root notebooks/helpers, requirements files, and documentation/output conventions. |
| [Project 1 instructions](https://github.com/rohitfarfad/constellation-detector/blob/main/AGENTS.md) | Same organizational and reproducibility reference. |

Both GitHub root listings and instruction files were fetched; reference commits are
in `DATA_SOURCES.json`. Their tasks, scores, deadlines, classical-only restrictions,
and historical authorizations do not apply here. Do not copy them into this project.

Live Kaggle URLs returned the right title but only an HTML shell. Web retrieval could
not expose section text; no connected browser was available. The unauthenticated file
API returned 401; the installed CLI requires authentication. No dataset, packaged README,
template, or official scorer has been downloaded. Requirements below are confirmed in
the course PDF, pending live/file reconciliation. Do not substitute a similarly named
penalty-outcome competition. Distinguish user authorization from directions in handouts.

## 3. Organization and environment

Paths are relative to this root; `Data/` never means filesystem `/Data`.

```text
Project 3/
  Project3_CV_2026_v5.pdf
  AGENTS.md, README.md, AI_USAGE.md, DATA_SOURCES.json
  requirements.txt, requirements-setup.txt
  Q1to3Solution.ipynb         # Questions 1-3, all code and explanations
  PenaltyKickPrediction.ipynb # Q4, all code and explanations
  Data/                      # immutable official inputs
  outputs/                   # figures, audits, experiments, later models
  Kaggle Submissions/        # candidate CSV copies, when authorized
  .venv/, .vscode/
```

No package/build step, placeholder model folders, configuration tree, or separate
progress/spec documents are needed. Do not add external solution Python files.
`PenaltyKickPrediction.ipynb` contains Phase 0 exploration and inline utilities;
`Q1to3Solution.ipynb` contains only question headings/descriptions until implementation
is requested. Keep this two-notebook working organization unless the user changes it.

Use Python 3.12.6 and `.venv/bin/python`, or `source .venv/bin/activate`. Direct
project/notebook pins are in `requirements.txt`; optional inspection/download tools
are in `requirements-setup.txt`. Update pins with dependency changes. Full installed
versions are saved in `outputs/setup/requirements-freeze.txt`. VS Code defaults to
`.venv/bin/python`; the local kernel is `Python (CV Project 3)`. Keep notebooks portable
to Colab with only explicit setup/path changes.

Mac: M4 Pro, 12 CPU cores, 24 GiB RAM, Metal hardware present. The inspected system
PyTorch process reported MPS and CUDA unavailable; no GPU computation was attempted.
No training framework is installed in this project's environment.

Preserve the original PDF and downloaded bytes. Derived data and generated results
belong under `outputs/`; create subfolders only as needed. Ignore data, outputs,
credentials, environments, caches, weights, and submission CSVs in Git. Never print
credentials. Historical Phase 0 notes/access evidence are retained in
`outputs/setup/phase0_notes/`; their old paths describe the original layout.
`DATA_SOURCES.json` retains the source checksum, environment, access status, and provenance.
Previous helper scripts/tests are preserved only in the ignored historical archive
`outputs/setup/pre_notebook_refactor.zip`; neither notebook reads that archive.

**Git policy:** version the two notebooks, instructions/README, AI disclosure,
`DATA_SOURCES.json`, requirements, `.vscode/settings.json`, original course PDF, and
`.gitkeep` folder markers. `.gitignore` excludes data, generated outputs/submissions,
caches, secrets, archives, media, arrays, weights, and data exports. Always save generated
files under `outputs/` or `Kaggle Submissions/`, so reports of any file type stay excluded.

## 4. Q4 data, targets, and validation

Source: PDF pp. 8, 10-12. **Reported, not locally measured:** 1,300 labeled public MP4
clips, 900 unlabeled private clips, 215 source videos. Clips contain only frames at or
before annotated contact minus 0.02 s, preserve original resolution/FPS, and have no
audio. Reported duration: about 0.3-9.8 s, median about 1.9 s. Most are shootouts;
some are in-game penalties. Randomized filenames do not encode temporal order.

| Target | Exact labels | Reported public counts |
|---|---|---|
| `kick_direction` | `left`, `middle`, `right` | 607, 181, 512 |
| `goalkeeper_direction` | `left`, `stands in the middle`, `right` | 669, 63, 568 |
| `goal_outcome` | `goal`, `no_goal` | 939, 361 |

Both directions use the **kicker's perspective facing the goal**. `save`, `out`, and
`post` map to `no_goal`. Keep perspective and any future flips consistent.

Expected files: `public/`, `private/`, `public_ground_truth.csv`, `private_metadata.csv`,
`public_position_clicks.csv`, `submission_template.csv`, and a packaged README.
Public columns: `clip,source_id,preferred_foot,gender,resolution,fps,kick_direction,goalkeeper_direction,goal_outcome,outcome_detail`.
Private metadata has the first six only. `preferred_foot` is the actual kicking foot;
gender is `M`/`F`; resolution is width by height, FPS is average frame rate.

Clicks cover 879 public clips (421 without supplied clicks), with columns `clip`,
`kicker_click_time_seconds`, `kicker_x_norm`, `kicker_y_norm`, `keeper_click_time_seconds`,
`keeper_x_norm`, `keeper_y_norm`. Coordinates are normalized from top left on a frame
0.25 s before contact. They are supplemental supervision, absent privately.

**Validate by `source_id`**, never random clips. A source is a broadcast/shootout or
compilation: 133 public-only, 79 private-only, and three shared sources are reported.
No source may cross a training/validation fold. Inspect replays, exact/near duplicates,
camera/context bias, and class balance. No separate validation set is specified.
Actual corruption, missing cells, dimensions, duplicates, and metadata distributions
are unmeasured. Do not use targets or `outcome_detail` as inference features.

## 5. Metric, submission contract, and rules

PDF pp. 9-12: `score = 0.60 * kick_accuracy + 0.25 * keeper_accuracy + 0.15 * outcome_accuracy`.
Each accuracy uses exact equality over scored clips. Higher is better, range [0,1].
The Kaggle notebook's `weighted_accuracy` implements this formula, not downloaded official code.
Log all three components. Public leaderboard: 360 private clips (40%); final private
leaderboard: remaining 540 (60%). Do not tune on leaderboard data.

Header: `clip,kick_direction,goalkeeper_direction,goal_outcome`. Exactly 900 data rows;
every real private ID once, including `.mp4`, with all three exact label strings.
Read IDs from the real template and metadata; never synthesize them. The PDF names
`submission_template.csv`, not `sample_submission.csv`. The validator additionally
requires template row order conservatively; the PDF does not explicitly require it.
A blank template is not a valid prediction file. Real-template integration is pending.

- Inference may use only that private clip's pre-contact video and its metadata, plus
  what the model learned from allowed public/external data and pretrained models.
- External datasets and pretrained models are allowed if named in the notebook.
  Recheck live rules when accessible.
- No manual private labeling or human decisions at prediction time. Never find original
  broadcasts, other footage, or records to look up these penalties' outcomes.
- At most two students/team, 20 submissions/team/day, one selected final submission.
  These PDF limits do not authorize uploading anything.
- Q4 grading: competition 50 points, report 10, having held first place 5. Private score
  must beat the private educated-guess reference for competition/SOTA credit. The PDF's
  0.52277 is a public-data reference, not a known final-private threshold. Public
  marginal-majority accuracy is about 0.516808; keep these references distinct.

## 6. Experiment workflow and next phases

After authorization: **analyze -> hypothesize -> implement -> validate -> record ->
compare -> decide**. Define one hypothesis, make the smallest useful change, compare
on identical source-grouped validation data, and retain/revise/revert on evidence.
Use seed 6643 unless varied explicitly. Save split IDs and settings. Record seed,
configuration, code version, component/weighted metrics, runtime, hardware, artifacts,
observations, and decision in `outputs/experiment_log.csv`. Preserve important results;
keep concise decisions here. Never claim an unmeasured score or unrun test.

1. **Phase 1:** finish the audit; freeze source-grouped splits; measure training-fold
   majority and simple metadata references, then a modest visual baseline. Metadata
   usefulness is a hypothesis. Kick direction contributes 60% of the score.
2. **Phase 2:** choose visual/temporal methods after inspecting actual clip quality;
   consider simple frame aggregation and public-click supervision when justified.
3. **Phase 3:** address observed errors one change at a time. Add model, preprocessing,
   or ensemble complexity only for validated gains.
4. **Phase 4:** freeze the method, infer all real private IDs, validate the CSV, and
   preserve evidence. Kaggle upload still needs explicit instruction.
5. **Phase 5:** assemble the reproducible final notebook with methods, outputs,
   limitations, named external assets, and required AI disclosure.

## 7. Delivery, status, and next work

PDF p. 1 describes one final `.ipynb` with code, executed outputs, figures, and
explanations. The user's current working organization explicitly uses two notebooks;
keep them separate and revisit course packaging only when final delivery is requested.
Brightspace requires the file and a shareable view link. The Q4 notebook must reproduce
training, inference, and CSV generation. LLM help requires a chat-history link or PDF;
`AI_USAGE.md` records assistance but is not a substitute export. Never fabricate history.

**Deadline conflict:** p. 1 says November 8 (year omitted); p. 2 says November 5, 2026.
Resolve with the instructor. Kaggle closing timestamp/timezone remains unverified.

**Phase 0:** environment, accessible-source reconnaissance, published metric, downloader,
audit, validator, and notebook scaffold are implemented. No data was downloaded;
no model training, competition predictions, or Kaggle upload occurred.

**2026-10-22 refactor:** matched the previous repos' flat notebook/helper layout and
minimal-code rules; consolidated status here, provenance in `DATA_SOURCES.json`, and
AI disclosure in `AI_USAGE.md`. Preserved initial evidence and figures in `outputs/`;
removed unused package/configuration/documentation scaffolding. Prior projects and
original PDF bytes were not modified.

**Notebook-only follow-up:** created `Q1to3Solution.ipynb`, retained the subject-specific
`PenaltyKickPrediction.ipynb`, and moved download/audit/metric/CSV validation code into
the Q4 notebook. Removed all five root Python files, including external tests; preserved
their previous bytes in the historical archive. The Kaggle notebook has small inline
checks using temporary synthetic data. Downloads are disabled by default, and no
competition candidate is selected. Notebook execution reports missing data without
raising a terminal-style exit. The original PDF and prior projects remain untouched.

**Validation:** both notebooks were checked in independent fresh kernels; all 11 Q4
code cells executed without errors, including inline synthetic checks. The Q1-Q3
scaffold has no solution code yet. The notebook-defined functions also passed the
30 preserved regression cases; one official-template case remains skipped while
data is unavailable. No root `.py` files or external project-code imports remain.
Dependency consistency and the original PDF checksum passed.

**Next authorized work:** configure Kaggle credentials privately, verify invitation/rules
access, use the Kaggle notebook's optional download cells, inspect the packaged
README/scorer/template, and run its audit cells with decoding/hashing enabled as needed.
Record empirical findings
here. Do not bypass missing official files with guessed IDs. Stop before Phase 1 until
requested.
