# PythonMuse Builder to Production

**I built something useful. What do I need to leave behind so someone else can find it, run it, validate it, maintain it, and eventually take it over?**

This repository answers that question for accounting and finance professionals who build their own tools: Python scripts, AI agents, Claude Code or Codex workflows, Microsoft Copilot agents, Power Automate flows, Excel and Power Query automations. You do not need to be a developer to use it. You need to be someone whose experiment worked.

> **Build freely. Leave enough breadcrumbs for someone else to follow.**

---

## The builder boom

Accountants who would never call themselves developers are now building things. That is good news. The people closest to the close know where the manual work lives, which exceptions matter and where the systems fall short.

Most of what gets built is an experiment. Many experiments end up in the vibe-coding graveyard, next to that brilliant idea from 10:30 p.m. That is fine. Experiments are supposed to fail sometimes.

This repository is about the ones that **don't** fail.

## The problem with success

An abandoned experiment costs nothing when you walk away. A successful one does. Nobody announces "effective today, this script is part of the monthly close." It just happens:

**Experiment → Helpful Tool → Habit → Dependency → Business Process**

That is how dependency *happens*: quietly, one saved hour at a time. Six months later the team relies on the output, and the only person who knows how it works is the person who built it.

> **You may have removed the manual dependency without removing the person dependency.**

The difference between an abandoned experiment and an organizational dependency is not the code. It is whether anyone else would notice if it disappeared.

## Give successful experiments a graduation path

This is how dependency gets *managed*:

**Experiment → Personal Tool → Team Tool → Production Workflow → Managed Asset**

Documentation and control should grow as dependency grows. An experiment needs nothing. A managed asset needs an owner, a backup, validation and a change process. Everything in between is a sliding scale.

### When should a personal tool start graduating?

It has probably stopped being personal when any of these are true:

- Other people rely on its output.
- It touches production financial, customer or employee data.
- A recurring process (close, reporting, a reconciliation) depends on it.
- It has been given system access or runs on someone's personal credentials.
- If it failed, reporting would be late or wrong.

Or the one-question version: **Would the business care if this disappeared tomorrow?** If yes, start graduating it.

## The minimum to leave behind

Not a fifty-page manual. Four breadcrumbs:

1. **A README.** What it does, why it exists, where it lives, what it touches, how it starts. Use [templates/README_TEMPLATE.md](templates/README_TEMPLATE.md).
2. **Business-logic comments in the workflow.** Why intercompany is excluded, where the date gets updated. Not "read Excel file." See [HUMAN_INSTRUCTIONS_GUIDE.md](HUMAN_INSTRUCTIONS_GUIDE.md#comments-inside-the-workflow).
3. **Human Instructions.** Written for the accountant who inherits it, not for a developer. Inputs, what to update, how to run, how to validate. See [HUMAN_INSTRUCTIONS_GUIDE.md](HUMAN_INSTRUCTIONS_GUIDE.md).
4. **A trail from the output back to the workflow.** The reviewed recon in the Close folder should say which workflow made it. See [OUTPUT_TRACEABILITY.md](OUTPUT_TRACEABILITY.md).

Yes, AI can read your code and explain it to the next person. That works surprisingly well. It also uses tokens. At month-end, 87% through your token allowance, with three recs still open, your successor will wish you had written it down.

## What's in here

Start with the Lottery Test. It takes five minutes and tells you which of the other files you need.

| File | Use it when |
|---|---|
| [LOTTERY_TEST.md](LOTTERY_TEST.md) | You want to know if someone else could run your workflow tomorrow. Start here. |
| [WORKFLOW_PASSPORT.md](WORKFLOW_PASSPORT.md) | You need a one-page record so people can find out what exists without reading code. |
| [HUMAN_INSTRUCTIONS_GUIDE.md](HUMAN_INSTRUCTIONS_GUIDE.md) | You are writing run instructions or code comments for a non-developer. |
| [OUTPUT_TRACEABILITY.md](OUTPUT_TRACEABILITY.md) | Your output gets filed as close support or audit evidence. |
| [BUILDER_HANDOFF.md](BUILDER_HANDOFF.md) | You are changing roles, leaving, or handing the workflow to someone. |
| [PRODUCTION_READINESS.md](PRODUCTION_READINESS.md) | A team wants to rely on the workflow every month. |
| [CHANGE_MANAGEMENT.md](CHANGE_MANAGEMENT.md) | The workflow is in use and someone wants to change it. |
| [TAKEOVER_ASSESSMENT.md](TAKEOVER_ASSESSMENT.md) | The builder has already left and you just found the workflow. |

**Blank templates** to copy into your own workflow folder live in [templates/](templates/):
[README](templates/README_TEMPLATE.md) · [Human Instructions](templates/HUMAN_INSTRUCTIONS_TEMPLATE.md) · [Workflow Passport](templates/WORKFLOW_PASSPORT_TEMPLATE.md) · [Validation](templates/VALIDATION_TEMPLATE.md) · [Changelog](templates/CHANGELOG_TEMPLATE.md)

**A worked example** lives in [examples/monthly_reconciliation_example/](examples/monthly_reconciliation_example/): a small AR subledger to GL 1200 tie-out with every breadcrumb filled in. It runs. It also deliberately fails to tie, so you can see what the exception path looks like.

## How to use this repo

1. Run the [Lottery Test](LOTTERY_TEST.md) on one workflow you built.
2. Copy the templates you need into that workflow's folder. Delete the sections that don't apply. Short and true beats long and stale.
3. Fill in a [Workflow Passport](WORKFLOW_PASSPORT.md) so someone can find it.
4. If a team depends on it, walk through [Production Readiness](PRODUCTION_READINESS.md).
5. From then on, changes go through [Change Management](CHANGE_MANAGEMENT.md).

The templates are the same whatever tool you build with. We use the Claude extension in VS Code, but a Copilot agent, a Power Automate flow or a Power Query model needs exactly the same breadcrumbs.

## When you need more than this

This repository is deliberately lightweight. It covers continuity: can someone else find, run, validate and inherit the workflow?

Move to the broader [PythonMuse AI Governance repository](https://github.com/PythonMuse/accounting_and_finance-ai-governance) when you need:

- A risk rating or use-case approval: [risk methodology](https://github.com/PythonMuse/accounting_and_finance-ai-governance/blob/main/docs/risk-methodology.md)
- Rules for what data an AI tool may see: [data classification](https://github.com/PythonMuse/accounting_and_finance-ai-governance/blob/main/docs/data-classification.md)
- Formal review and sign-off: [review and sign-off](https://github.com/PythonMuse/accounting_and_finance-ai-governance/blob/main/docs/review-and-signoff.md)
- A controlled change process with approvals: [change management](https://github.com/PythonMuse/accounting_and_finance-ai-governance/blob/main/docs/change-management.md)
- Security, privacy, legal or contractual review

## Related Article

This repository accompanies PythonMuse LLC Article 40: [You Built an AI Workflow. What Happens If You Win the Lottery?](https://github.com/PythonMuse/ai-ledger/tree/main/articles/40-builder-to-production/)

You do not need to read the article to use the templates. But it is short, and it has jokes.

---

This repository is for educational purposes only. It is not accounting, tax, legal or other professional advice. All company, customer and financial data in the example is fictional. Human review owns the final call on any accounting result.

## License

MIT. See [LICENSE](LICENSE).

## About this repository

Built as a companion to PythonMuse LLC Article 40. ChatGPT (5.5 Sol) helped shape the first draft. Claude Sonnet and Claude Opus reviewed the draft and co-built the repository design. Claude Code (Claude Opus 5.5) implemented, tested and documented it. Human review by PythonMuse LLC.

© 2026 PythonMuse LLC
