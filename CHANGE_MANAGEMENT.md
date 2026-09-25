# Change Management

The workflow was tested and approved in January. It is now September. Is it still the same workflow?

## How workflows drift

Nobody sets out to change an approved process. It happens one reasonable edit at a time:

- Someone tweaks a prompt so the summary reads better.
- A mapping gets a new account added.
- The ERP export gains a column, and a line of code is adjusted to cope.
- A different AI model is selected because the old one was retired, or because the new one is faster.
- A colleague adds "just one more" exception for a new customer.
- A threshold changes from $0.01 to $5.00 to make a recurring difference go away.

Each change is small. None was retested. By September the workflow in production no longer matches what was tested and approved, and nobody can say exactly when that happened.

Your organization needs to know more than whether an automation exists. It needs to know **which version it is relying on**.

## The loop

**Issue → Diagnose → Change → Retest → Reapprove → Release**

| Step | What it means | Evidence to keep |
|---|---|---|
| Issue | Something broke, drifted, or needs to change. Write it down. | A line in the changelog or an issue |
| Diagnose | Find the cause before touching anything. Was it the workflow, the source data or the process? | A short note of the cause |
| Change | Make the smallest change that fixes it. | The change itself, in version control |
| Retest | Rerun on a period with known results. Compare to the expected figures. | Expected vs. actual |
| Reapprove | The process owner agrees the changed workflow is fit to rely on. Scale this to the change. | Name and date |
| Release | Update the version number, changelog, Human Instructions and Passport. Then use it. | Updated version and docs |

## Keep it proportionate

Not every change needs the full loop.

- **Fixing a typo in the instructions:** change and release.
- **Changing a period, a folder or a file name that the instructions already tell you to change:** that is operating the workflow, not changing it.
- **Anything that could change the accounting answer** (logic, mappings, thresholds, exclusions, prompts, model, source layout): the full loop, every time.

The test: *could this change make the output different for the same inputs?* If yes, retest and reapprove.

## The changelog

A changelog is a running list of what changed, when, why and who approved it. It is how next year's reviewer knows that the $5.00 threshold was a deliberate decision, not an accident.

Blank template: [templates/CHANGELOG_TEMPLATE.md](templates/CHANGELOG_TEMPLATE.md)

Put the version number somewhere the output can show it. The [example workflow](examples/monthly_reconciliation_example/) prints its version and git commit on the Control tab of every workbook. See [Output Traceability](OUTPUT_TRACEABILITY.md).

## Going further

For a controlled change process with formal approvals, see [change management](https://github.com/PythonMuse/accounting_and_finance-ai-governance/blob/main/docs/change-management.md) in the PythonMuse AI Governance repository.

---

© 2026 PythonMuse LLC · MIT License · Educational purposes only, not professional advice.
