# Workflow Passport

A one-page record of a workflow. It lets someone find out what exists, who owns it and what it touches **without reading the code**.

Think of it as the fixed asset register entry for something your team built. It doesn't explain how the asset works. It proves the asset exists, says where it is and who is responsible for it.

## When to fill one in

- When a tool becomes a **Team Tool**: someone other than you relies on it.
- Update it whenever the owner, location, version or data changes.
- Keep all passports in one place (a folder, a SharePoint list, a spreadsheet). A passport nobody can find defeats the purpose.

Blank version: [templates/WORKFLOW_PASSPORT_TEMPLATE.md](templates/WORKFLOW_PASSPORT_TEMPLATE.md)

## Completed example

This passport is for the [monthly reconciliation example](examples/monthly_reconciliation_example/) in this repo. Fernhill Supply Co. is fictional.

| Field | Entry |
|---|---|
| Workflow name | AR Subledger to GL 1200 Tie-Out |
| Business purpose | Proves the AR aging agrees to GL 1200 at month-end and lists differences for review |
| Builder | A. Rivera, Senior Accountant |
| Business / process owner | Assistant Controller |
| Backup owner | J. Chen, Staff Accountant (has run it twice with the instructions) |
| Current users | GL team; Controller reviews output |
| Business process supported | Month-end close, balance sheet reconciliations (close day 3) |
| Location of code / agent | Team repository: `examples/monthly_reconciliation_example/` |
| Platform / tools | Python 3.10+, pandas, openpyxl. Built with help from Claude Code in VS Code |
| Model / provider | None at run time. AI helped write the code, but the workflow itself calls no AI model |
| Systems accessed | None directly. Reads two exported CSV files |
| Data used | Customer names and open invoice balances (internal, confidential) |
| Input locations | `data/ar_subledger_YYYYMM.csv`, `data/gl_trial_balance_YYYYMM.csv` |
| Output locations | Created in `output/AR_1200_Recon_YYYYMM.xlsx`. Reviewed copy filed in `Close > YYYY > MM > Balance Sheet Recs > 1200 AR` |
| Human validation required | Yes. Reviewer ties totals to source reports and clears exceptions. See VALIDATION.md |
| Credentials / access dependencies | ERP access to run the two exports. No personal credentials in the code |
| Frequency | Monthly |
| Current version | 1.0.0 |
| Last tested date | 2026-09-24 |
| Last updated date | 2026-09-24 |
| Fallback / manual process | Tie the AR aging total to the trial balance in Excel (see HUMAN_INSTRUCTIONS.md, Fallback) |
| Known limitations | Single entity. Expects one GL 1200 row. Intercompany flag must be maintained in the ERP customer master |
| Instructions | [HUMAN_INSTRUCTIONS.md](examples/monthly_reconciliation_example/HUMAN_INSTRUCTIONS.md) |
| Validation | [VALIDATION.md](examples/monthly_reconciliation_example/VALIDATION.md) |

Notice what isn't here: how the code works. That belongs in the README and the comments. The passport only needs to answer "what is it, where is it, who do I ask?"

---

© 2026 PythonMuse LLC · MIT License · Educational purposes only, not professional advice.
