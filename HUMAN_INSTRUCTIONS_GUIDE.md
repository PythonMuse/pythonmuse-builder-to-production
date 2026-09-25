# Writing Human Instructions

Human Instructions are the most important thing you leave behind. They are how an accountant who has never seen your code runs your workflow at month-end and knows whether to trust the answer.

Blank template: [templates/HUMAN_INSTRUCTIONS_TEMPLATE.md](templates/HUMAN_INSTRUCTIONS_TEMPLATE.md)
Worked example: [examples/monthly_reconciliation_example/HUMAN_INSTRUCTIONS.md](examples/monthly_reconciliation_example/HUMAN_INSTRUCTIONS.md)

They can live in the README or in a separate `HUMAN_INSTRUCTIONS.md`. Separate is easier to find.

## Who you are writing for

Picture a capable staff accountant who joined last month. They know what a GL tie-out is. They do not know Python, what a virtual environment is, or why the file has to be called `ar_subledger_202609.csv` and not `AR Aging Sept FINAL.csv`.

Write for them. If a step needs a developer, you have not finished writing it.

## The sections, and what makes each one good

**Purpose.** One or two sentences in accounting language. "Ties the AR aging to GL 1200 and lists differences." Not "processes CSV inputs via pandas."

**Inputs required.** Every input, with:
- the report name and the system it comes from, including the parameters to run it with
- the required format (CSV, XLSX, columns)
- the required file name, with the period in it (`_YYYYMM`)
- where to save it
- which period it should cover
- anything that must happen first ("run after AR is closed for the month")

The most common month-end failure is a correct workflow run on last month's file. Naming conventions with the period in them are cheap insurance.

**Before running.** Everything that changes between runs, and exactly where to change it: dates and periods, entity names, account numbers, source system names, folder locations, configuration settings. "Update the period" is not enough. "Open `sample_code.py` and change `REPORT_MONTH = 9` near the top" is.

**How to run.** Numbered steps. One action per step. Say what they should see when it works.

**Outputs.** What gets produced, what it is called, where it first appears, and where the final reviewed version is filed. The last one matters most. An output left in a working folder is not close support.

**Validation.** Specific checks, not "review for reasonableness." For example:
- tie the output to the GL balance
- compare record counts to the source report
- agree totals to the source report
- review every item on the exception report
- investigate any difference above a stated threshold

Say it plainly, in these words:

> **The workflow running without an error does not mean the accounting result is correct.**

A script that runs perfectly on the wrong file produces a perfectly formatted wrong answer.

**Exceptions and troubleshooting.** The errors you have actually seen, what they mean and what to do. Every time someone asks you a question about the workflow, the answer belongs here.

**Fallback.** The manual process if the workflow cannot run. The close still has to happen.

## Comments inside the workflow

The Human Instructions explain how to *run* the workflow. Comments inside the code explain *why* it does what it does. Both are for the next accountant.

A comment should capture business reasoning or a future-change point, not repeat what the code says.

**A poor comment:**

```python
# Read Excel file
```

It tells you nothing the code doesn't already say. It is also easy to get out of date: in our [example](examples/monthly_reconciliation_example/sample_code.py) it sits above a line that reads a CSV. Nobody can learn the business rules from it.

**Comments worth leaving:**

```python
# BUSINESS RULE:
# Intercompany customers are excluded because they are
# reconciled separately under the intercompany close process.
```

```python
# PERIOD UPDATE:
# Update REPORT_MONTH and REPORT_YEAR before each monthly run.
# Input files must use YYYYMM in the filename.
```

```python
# VALIDATION:
# Final AR balance must agree to GL account 1200 within $0.01.
# Differences are written to the exception file for manual review.
```

The labels are a simple habit that pays off. Someone new can search the file for `PERIOD UPDATE` and find every line they must touch before a run. Searching for `BUSINESS RULE` shows the accounting decisions baked into the code, which is often the part an auditor or a new controller wants to see.

The same idea applies outside Python. Put business-rule notes in a Power Query step description, a Power Automate action note, a Copilot agent's instructions, or a clearly labelled "Notes" tab in the workbook.

## Let AI draft it, then fix it

Your co-pilot is good at a first draft. Try something like:

> Read this workflow and draft a HUMAN_INSTRUCTIONS.md for an accountant who does not code. List every input file, every value that must change each month and where it is, and how to run it. Flag anything you are unsure about.

Then review it like any other draft. AI can describe what the code does. Only you know which checks prove the answer is right, and where the reviewed file gets filed.

---

© 2026 PythonMuse LLC · MIT License · Educational purposes only, not professional advice.
