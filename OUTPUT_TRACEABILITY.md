# Output Traceability

Your workflow creates a reconciliation. Someone reviews it and files it in the September Close folder. Six months later, an auditor opens that file and asks: how was this produced?

The output should answer that itself. **Final accounting support should not become disconnected from the process that created it.**

## What the output should say

At minimum, every filed output should identify:

- **Workflow name**
- **Reporting period**
- **Workflow or repository location**
- **Workflow version or commit**
- **Source period** (of each input file)
- **Run date**
- **Human reviewer** (and date)

With that, someone can find the workflow, rerun it on the same inputs, get the same answer, and run it again next month, even if the builder is now enjoying lottery winnings somewhere without Wi-Fi.

## A Control tab

The simplest way in Excel: add a tab called **Control** (or Provenance, or About) to every output. Here is the one the [example workflow](examples/monthly_reconciliation_example/) writes automatically (commit, run date and user are illustrative; yours will differ):

| Field | Value |
|---|---|
| Workflow name | AR Subledger to GL 1200 Tie-Out |
| Workflow version | 1.0.0 |
| Reporting period | 202609 |
| Source period (AR subledger file) | 202609 |
| Source period (GL trial balance file) | 202609 |
| Source files | ar_subledger_202609.csv; gl_trial_balance_202609.csv |
| Records read / excluded / included | 10 / 1 / 9 |
| Repository location | https://github.com/PythonMuse/pythonmuse-builder-to-production/tree/main/examples/monthly_reconciliation_example |
| Git commit | 3f9c2ab |
| Run date | 2026-10-03 09:14 |
| Run by | jchen |
| Result | DOES NOT TIE - review Exceptions tab |
| Reviewed by / date | *(left blank for the reviewer)* |

A few details that matter:

- **Reviewed by / date is blank on purpose.** The workflow cannot review itself. A person fills that in.
- **Source period is separate from reporting period.** They should match. When they don't, someone ran September's recon on August's file, and the Control tab shows it.
- **The commit is a fingerprint of the exact code version.** If the code has local edits that were never committed, the example says so ("uncommitted changes present"), so a modified copy can't pass as the approved one. Not using git? A version number that matches your [changelog](templates/CHANGELOG_TEMPLATE.md) does the same job.

## Not Excel?

Same idea, different place:

- **PDF or Word output:** a footer or a final "About this document" block.
- **Power BI:** a small provenance card on the report page, or an "About" page.
- **AI agent output:** have the agent end every summary with the workflow name, version, period and source files it used.
- **Journal entry support:** put the workflow name and version in the JE description or attachment.

## Where does the reviewed version go?

Traceability runs both ways. The output points to the workflow. The [Human Instructions](HUMAN_INSTRUCTIONS_GUIDE.md) should point to where the reviewed output is filed. A recon that only ever lived in `output/` on one person's laptop was never really filed.

---

© 2026 PythonMuse LLC · MIT License · Educational purposes only, not professional advice.
