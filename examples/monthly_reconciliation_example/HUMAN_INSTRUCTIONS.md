# Human Instructions: AR Subledger to GL 1200 Tie-Out

**Owner:** Assistant Controller  **Backup:** J. Chen  **Last updated:** 2026-09-24

*Fictional example. Company, systems and folder names are made up.*

## Purpose

Proves the AR aging agrees to GL account 1200 (AR - Trade) at month-end, after excluding intercompany customers, and lists any difference for review. It is the support for the 1200 balance sheet reconciliation on close day 3.

## Inputs Required

| Input | Source system and how to run it | Format | File name | Save to | Period | Prerequisites |
|---|---|---|---|---|---|---|
| AR open invoice aging | ERP > Receivables > Reports > *Open Invoice Aging*. As-of date = last day of the month. Include credit memos. Export as CSV. | CSV with columns `customer_id, customer_name, invoice_number, invoice_date, due_date, open_balance, intercompany_flag` | `ar_subledger_YYYYMM.csv` (e.g. `ar_subledger_202609.csv`) | `data/` in this folder | The month being closed | AR subledger closed for the month (AR Supervisor confirms in the close tracker) |
| Trial balance | ERP > General Ledger > *Trial Balance*. Period = the month being closed, all accounts. Export as CSV. | CSV with columns `period, account, account_name, balance` | `gl_trial_balance_YYYYMM.csv` | `data/` in this folder | The month being closed | All AR journal entries for the month posted |

**Why the names matter:** the script only accepts files whose name contains the period it is reconciling. `AR Aging FINAL v2.csv` will be rejected. That is on purpose. It stops last month's file being reconciled by accident.

## Before Running

| What | Where to change it | Example |
|---|---|---|
| Reporting month | `sample_code.py`, near the top: `REPORT_MONTH` | `REPORT_MONTH = 10` for October |
| Reporting year | `sample_code.py`, near the top: `REPORT_YEAR` | `REPORT_YEAR = 2026` |
| Input files | Save both new exports into `data/` with the new period in their names | `ar_subledger_202610.csv` |

Tip: open `sample_code.py` in any text editor and search for `PERIOD UPDATE`. That comment marks every line you change each month.

Nothing else normally changes. If the AR account number, the intercompany account or the export layout changes, that is a **change to the workflow**, not a monthly update. Follow [Change Management](../../CHANGE_MANAGEMENT.md).

## How to Run

First time on a new computer only:
1. Install Python 3.10 or later from python.org (or ask IT).
2. Open a terminal in this folder. (In VS Code: File > Open Folder, then Terminal > New Terminal.)
3. Run `pip install -r requirements.txt`

Every month:
1. Save both exports into `data/` with the correct names (see Inputs).
2. Update `REPORT_MONTH` and `REPORT_YEAR` in `sample_code.py`. Save the file.
3. Close any previous copy of the output workbook if it is open in Excel.
4. In the terminal, run `python sample_code.py`
5. When it works, you will see the tie-out figures, a **Result** line (`TIES` or `DOES NOT TIE`) and the path of the output file.

If you see a line starting with `STOPPED:`, the workflow did not run. Read the message. It says what is wrong. See Troubleshooting below.

## Outputs

| Output | File name | Created in | Final reviewed version filed in |
|---|---|---|---|
| Reconciliation workbook | `AR_1200_Recon_YYYYMM.xlsx` | `output/` in this folder | `Close > YYYY > MM Month > Balance Sheet Recs > 1200 AR` (e.g. `Close > 2026 > 09 September > Balance Sheet Recs > 1200 AR`) |

The workbook has three tabs:
- **Recon:** gross subledger, intercompany excluded, adjusted subledger, GL 1200, difference, result. Customer subtotals below.
- **Exceptions:** the tie-out difference (if any) and each intercompany item that was excluded.
- **Control:** workflow name, version, periods, source files, repository location, git commit, run date and a blank **Reviewed by / date** line.

The file in `output/` is a working copy. It is overwritten next time the workflow runs for the same period. Only the reviewed copy in the Close folder is close support.

## Validation

**The workflow running without an error does not mean the accounting result is correct.**

Before filing, the reviewer:

1. **Checks the period.** On the Control tab, Reporting period and both Source periods all show the month being closed.
2. **Agrees the GL figure.** "GL account 1200 balance" on the Recon tab equals account 1200 on the trial balance in the ERP.
3. **Agrees the subledger figure.** "Gross AR subledger total" equals the grand total on the AR aging report in the ERP.
4. **Agrees the record count.** "Records read" on the Control tab equals the number of lines on the AR aging report.
5. **Reviews the intercompany exclusions.** Each excluded item on the Exceptions tab really is an intercompany entity, and the total agrees to GL 1210 on the trial balance.
6. **Clears every exception.** If the Result is `DOES NOT TIE`, the difference must be explained (for example a manual journal entry posted straight to 1200, a cash receipt timing difference or a missing invoice) and either corrected or documented on the reconciliation before sign-off. There is no "small enough to ignore." The tolerance is $0.01.
7. **Signs.** Types their name and the date in **Reviewed by / date** on the Control tab, then files the workbook in the Close folder.

Test evidence and expected figures: [VALIDATION.md](VALIDATION.md).

## Exceptions / Troubleshooting

| What you see | What it means | What to do |
|---|---|---|
| `STOPPED: No 'ar_subledger' file for period 202610. Found: ar_subledger_202609.csv...` | The period in the script and the file names don't match. | Save the new month's export, or update `REPORT_MONTH` / `REPORT_YEAR`. |
| `STOPPED: '...' does not contain a YYYYMM period in its name` | A file in `data/` has no period in its name. | Rename it, e.g. `ar_subledger_202609.csv`. |
| `STOPPED: intercompany_flag must be Y or N. Check invoice(s): ...` | A customer is missing its intercompany flag, often a new customer. | Ask AR to fix the customer master, re-export and re-run. Don't guess the flag in the CSV. |
| `STOPPED: ... is missing column(s)` | The ERP export layout changed. | Check the report settings. If the layout changed permanently, that is a workflow change: tell the owner. |
| `STOPPED: Expected exactly one row for GL account 1200` | The trial balance export is filtered or split by sub-account. | Re-export at account level for all accounts. |
| `STOPPED: Could not write ... Is it open in Excel?` | The output workbook is open. | Close it and re-run. |
| `ModuleNotFoundError: No module named 'pandas'` | The one-time setup hasn't been done on this computer. | Run `pip install -r requirements.txt`. |
| `'python' is not recognized...` | Python isn't installed, or Windows uses a different name. | Try `py sample_code.py`, or install Python. |
| `Result: DOES NOT TIE` | The workflow worked. The accounts don't agree. | This is an accounting question, not a script problem. Follow Validation step 6. |

## Fallback

If the workflow cannot run, the close still happens:

1. Open the AR aging export in Excel.
2. Filter out customers with `intercompany_flag = Y`. Note their total.
3. Sum `open_balance` for the remaining lines.
4. Compare to account 1200 on the trial balance. Investigate any difference.
5. Document the tie-out on the standard reconciliation template, note "prepared manually, workflow unavailable" and tell the owner why it didn't run.

---

© 2026 PythonMuse LLC · MIT License · Educational purposes only, not professional advice.
