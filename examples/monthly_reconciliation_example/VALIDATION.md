# Validation: AR Subledger to GL 1200 Tie-Out

**The workflow running without an error does not mean the accounting result is correct.**

## 1. Test evidence

**Tested on period:** 202609  **Tested by:** Claude Code, checked by PythonMuse LLC  **Date:** 2026-09-24  **Version:** 1.0.0

The expected figures below were worked out by hand from the files in `data/` **before** the script was run. Then the script was run and its output compared.

### Hand calculation

AR subledger, `data/ar_subledger_202609.csv`:

| Customer | Invoice | Open balance | Intercompany? |
|---|---|---:|:---:|
| C001 Bramblewood Hardware | INV-9101 | 12,450.00 | N |
| C001 Bramblewood Hardware | INV-9118 | 3,275.50 | N |
| C002 Copperline Builders | INV-9104 | 8,920.25 | N |
| C002 Copperline Builders | CM-0412 (credit memo) | (450.00) | N |
| C003 Driftwood Cafe Group | INV-9109 | 1,540.00 | N |
| C003 Driftwood Cafe Group | INV-9122 | 2,310.75 | N |
| C004 Evergreen Property Management | INV-9112 | 15,600.00 | N |
| C005 Foxglove Landscaping | INV-9115 | 4,088.40 | N |
| C900 Fernhill Supply Canada Ltd | INV-9120 | 6,500.00 | **Y** |
| C006 Granite Peak Schools | INV-9125 | 9,735.10 | N |
| **Total (10 lines)** | | **63,970.00** | |

GL, `data/gl_trial_balance_202609.csv`: account 1200 = **57,482.50**. (Account 1210, Intercompany Receivable, = 6,500.00, which agrees to the excluded intercompany item.)

| Line | Expected |
|---|---:|
| Gross AR subledger total | 63,970.00 |
| Less: intercompany excluded (C900) | (6,500.00) |
| Adjusted AR subledger total | 57,470.00 |
| GL account 1200 balance | 57,482.50 |
| **Difference (subledger - GL)** | **(12.50)** |
| Result at $0.01 tolerance | DOES NOT TIE |
| Records read / excluded / included | 10 / 1 / 9 |

### Expected vs. actual

| Check | Expected | Actual (script output) | Agrees? |
|---|---:|---:|:---:|
| Gross AR subledger total | 63,970.00 | 63,970.00 | Yes |
| Intercompany excluded | (6,500.00) | (6,500.00) | Yes |
| Adjusted AR subledger total | 57,470.00 | 57,470.00 | Yes |
| GL 1200 balance | 57,482.50 | 57,482.50 | Yes |
| Difference | (12.50) | (12.50) | Yes |
| Result | DOES NOT TIE | DOES NOT TIE | Yes |
| Records read / excluded / included | 10 / 1 / 9 | 10 / 1 / 9 | Yes |
| Customer subtotals (6 customers) sum to adjusted total | 57,470.00 | 57,470.00 | Yes |
| Exceptions tab | 1 tie-out difference + 1 intercompany item | Same | Yes |
| Control tab fields present, "Reviewed by / date" blank | Yes | Yes | Yes |

### Negative tests (the workflow should refuse to run)

| Scenario | Expected | Actual |
|---|---|---|
| `REPORT_MONTH = 10` with only 202609 files in `data/` | Stops: no file for 202610 | Stopped with that message |
| AR file renamed to `ar_subledger_final_v2.csv` | Stops: no YYYYMM in file name | Stopped with that message |
| Intercompany flag blanked on INV-9120 | Stops: flag must be Y or N | Stopped with that message |
| GL 1200 changed to 57,470.00 | Runs, Result = TIES, no tie-out exception | As expected |
| Run outside a git repository | Control tab Git commit = "unknown (not a git repository)" | As expected |

### About the $12.50

The difference is seeded on purpose, and it is **unexplained**. That is realistic: at this point the reviewer does not know the cause. It might be a manual journal entry posted straight to 1200, a cash receipt applied in the GL but not the subledger, or an invoice missing from the aging. The workflow's job is to surface it, not explain it. Explaining it is the accountant's job.

## 2. Monthly review checklist

Each run, the reviewer confirms:

- [ ] Control tab: Reporting period and both Source periods are the month being closed
- [ ] Gross AR subledger total agrees to the ERP AR aging grand total
- [ ] GL 1200 balance agrees to the ERP trial balance
- [ ] Records read agrees to the AR aging line count
- [ ] Intercompany exclusions are genuinely intercompany and agree to GL 1210
- [ ] Every item on the Exceptions tab is explained, corrected or escalated
- [ ] Reviewer name and date typed into "Reviewed by / date" on the Control tab
- [ ] Reviewed workbook filed in `Close > YYYY > MM Month > Balance Sheet Recs > 1200 AR`

## 3. What to do when it doesn't tie

Don't file it as reconciled. Investigate the difference. Record the cause and any correcting entry on the reconciliation. If it can't be resolved by close day 3, escalate to the Assistant Controller with the amount and what has been ruled out. Do not raise the tolerance to make it go away. That is a [workflow change](../../CHANGE_MANAGEMENT.md), and a bad one.

---

© 2026 PythonMuse LLC · MIT License · Educational purposes only, not professional advice.
