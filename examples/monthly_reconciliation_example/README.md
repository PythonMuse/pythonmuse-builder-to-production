# AR Subledger to GL 1200 Tie-Out

**Owner:** Assistant Controller  **Backup:** J. Chen  **Version:** 1.0.0  **Last tested:** 2026-09-24

> This is a worked example. Fernhill Supply Co., its customers and every number here are fictional. The folder shows what "good enough to hand over" looks like for a small workflow. See the [Workflow Passport](../../WORKFLOW_PASSPORT.md#completed-example) for its one-page record.

## What it does

Each month-end, it proves the AR aging (open invoices) agrees to the general ledger AR account, 1200, and lists anything that doesn't for review.

## Why it exists

The old process was an AR aging export, a pivot table, a manual intercompany adjustment and a hand-typed tie-out to the trial balance. It took about 40 minutes and one copy-paste error a quarter. This takes about two minutes, plus the review, which still matters.

## Where it lives

This folder. In real life: the team's shared repository, not anyone's laptop.

## What it touches

- **Inputs:** two CSV exports saved in `data/`
  - `ar_subledger_YYYYMM.csv` (AR open invoice aging)
  - `gl_trial_balance_YYYYMM.csv` (trial balance)
- **Output:** `output/AR_1200_Recon_YYYYMM.xlsx` with three tabs: **Recon**, **Exceptions** and **Control**
- **Systems and access:** none directly. Someone with ERP access runs the two exports.
- **AI model / provider:** none at run time. AI helped write the code, but the workflow calls no AI model.

## How it starts

Manually, once a month, after AR is closed for the period. Full steps: [HUMAN_INSTRUCTIONS.md](HUMAN_INSTRUCTIONS.md).

Short version:

```bash
pip install -r requirements.txt   # first time only
# update REPORT_MONTH / REPORT_YEAR in sample_code.py
python sample_code.py
```

## Key assumptions

- One entity. GL 1200 is AR - Trade. Intercompany receivables are booked to GL 1210.
- Customers flagged `intercompany_flag = Y` in the AR export are excluded. The flag comes from the ERP customer master. If a new intercompany entity is set up without the flag, it will be wrongly included.
- The trial balance export has exactly one row for account 1200.
- Tolerance is $0.01, for rounding only. It is not a materiality threshold.
- The input files carry their period (YYYYMM) in the file name. The script refuses to run on a mismatched period.

## Validation

**The workflow running without an error does not mean the accounting result is correct.** A reviewer checks the output every month. See [VALIDATION.md](VALIDATION.md) for the test evidence and the monthly review checklist.

## What to look at in this folder

| File | What it demonstrates |
|---|---|
| [HUMAN_INSTRUCTIONS.md](HUMAN_INSTRUCTIONS.md) | Run instructions an accountant can follow without knowing Python |
| [VALIDATION.md](VALIDATION.md) | Hand-calculated expected results, and what the reviewer checks |
| [sample_code.py](sample_code.py) | `BUSINESS RULE`, `PERIOD UPDATE` and `VALIDATION` comments, plus one deliberately poor comment with an explanation |
| `data/` | Synthetic inputs, seeded with one intercompany customer and one small unexplained difference |
| `output/` (created on run) | The workbook, with a Control tab tracing it back to this workflow |

The sample data **deliberately does not tie**: GL 1200 is $12.50 higher than the adjusted subledger. That is so you can see the exception path. Please don't "fix" the data.

## Change history

Version 1.0.0: first production version. The version is set in `WORKFLOW_VERSION` at the top of `sample_code.py` and printed on the Control tab. A real workflow would also keep a `CHANGELOG.md` ([template](../../templates/CHANGELOG_TEMPLATE.md)).

---

© 2026 PythonMuse LLC · MIT License · Educational purposes only, not professional advice.
