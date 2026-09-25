# The Lottery Test

You won the lottery. You are not coming in Monday.

(Or you are on vacation, out sick, promoted, or working somewhere else. The lottery is just the most pleasant version.)

It is the third day of close. Someone on your team opens the Close folder and sees last month's reconciliation, the one your workflow produces. Now they need this month's.

Could they do it without calling you?

## The chain

**Find it → Prepare the inputs → Run it → Find the output → Validate it → Reproduce it next month**

Every link has to hold. A perfect script nobody can find fails at link one.

## The checklist

Answer for one workflow at a time. Be honest. Nobody is grading this.

**Find it**
- [ ] Someone other than me knows this workflow exists.
- [ ] It lives in a company-accessible location, not my laptop, my personal OneDrive or my personal AI account.
- [ ] The location is written down somewhere a teammate would look (a [Workflow Passport](WORKFLOW_PASSPORT.md), the close checklist, the team wiki).

**Prepare the inputs**
- [ ] Every input is listed: which report, from which system, which parameters.
- [ ] The required file names and formats are written down (for example `ar_subledger_YYYYMM.csv`).
- [ ] It says where to put the files.

**Run it**
- [ ] Everything that changes each month (dates, periods, entity names, folder paths) is listed, with where to change it.
- [ ] The run steps are written for an accountant, not a developer.
- [ ] It does not depend on my personal login, API key or token.

**Find the output**
- [ ] It says what the output is called and where it appears.
- [ ] It says where the reviewed, final version gets filed.

**Validate it**
- [ ] It says exactly what must tie, and to what.
- [ ] It says what to do with exceptions and differences.
- [ ] It says clearly that finishing without an error is not the same as being right.

**Reproduce it next month**
- [ ] Someone could rerun last month and get the same answer.
- [ ] The output identifies which workflow and version produced it ([Output Traceability](OUTPUT_TRACEABILITY.md)).
- [ ] There is a written manual fallback if the workflow won't run.

## What your answers mean

There is no score. A score would let a workflow "pass" with the one box that matters left empty.

Look at which link broke first. That is where to start:

| First broken link | Start with |
|---|---|
| Find it | [Workflow Passport](WORKFLOW_PASSPORT.md) |
| Prepare, Run, Find the output | [Human Instructions](HUMAN_INSTRUCTIONS_GUIDE.md) |
| Validate it | [Validation template](templates/VALIDATION_TEMPLATE.md) |
| Reproduce it | [Output Traceability](OUTPUT_TRACEABILITY.md) and [Change Management](CHANGE_MANAGEMENT.md) |

**Best test of all:** hand your documentation to a colleague and watch them run it. Don't help. Every question they ask is a missing sentence.

A README that technically exists but that nobody can run from is not documentation. It is a souvenir.

---

© 2026 PythonMuse LLC · MIT License · Educational purposes only, not professional advice.
