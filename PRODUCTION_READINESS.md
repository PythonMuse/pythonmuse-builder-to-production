# Production Readiness

Your experiment works. Your team wants to rely on it every month. This checklist is for that moment: moving from **Team Tool** to **Production Workflow**.

It is not a gate designed to stop you. It is the list of things that are painful to discover missing on close day 3.

## The lifecycle

**Build → Prove → Approve → Launch → Adopt → Monitor → Improve → Retire**

| Stage | In plain English |
|---|---|
| Build | You made it work. |
| Prove | You showed it gives the right answer, and kept the evidence. |
| Approve | The process owner agreed to rely on it (with formal approval if your organization requires it). |
| Launch | It moved to a company location, off personal accounts, with documentation. |
| Adopt | Other people were shown how to run and review it. |
| Monitor | Someone notices when it breaks or drifts. |
| Improve | Changes go through [Change Management](CHANGE_MANAGEMENT.md). |
| Retire | When it is no longer needed, it is switched off on purpose, and the documentation says so. |

Retire is part of the lifecycle. A workflow nobody uses, still running on a schedule, still reading data, is not harmless.

## The checklist

Tick what applies. Write "n/a" and a reason for what doesn't. Proportion matters: a workflow that formats a report needs less than one that produces a balance sheet reconciliation.

**Prove**
- [ ] Testing completed on at least one real prior period, and the result agreed to the manual version.
- [ ] Validation evidence retained: what was tested, expected vs. actual, who checked it. ([Validation template](templates/VALIDATION_TEMPLATE.md))

**Ownership**
- [ ] Business owner assigned: the person accountable for the output, not only the code.
- [ ] Backup operator identified, and they have run it using only the documentation.

**Location and access**
- [ ] Personal credentials removed. Nothing depends on one person's login, API key or AI subscription.
- [ ] Company-accessible location established (team repository, shared drive, approved platform).
- [ ] Source and version control established, so you can tell which version produced which output.

**Documentation**
- [ ] README completed. ([template](templates/README_TEMPLATE.md))
- [ ] Human Instructions completed. ([guide](HUMAN_INSTRUCTIONS_GUIDE.md))
- [ ] Workflow Passport completed and filed where people look. ([passport](WORKFLOW_PASSPORT.md))

**Control**
- [ ] Human review defined: who reviews, what they check, where they sign off.
- [ ] Fallback process documented and still workable.
- [ ] Logging and evidence considered: the output carries a trail back to the workflow. ([Output Traceability](OUTPUT_TRACEABILITY.md))
- [ ] Change process established, with a changelog. ([Change Management](CHANGE_MANAGEMENT.md))

## When this checklist is not enough

Stop and bring in the broader [PythonMuse AI Governance repository](https://github.com/PythonMuse/accounting_and_finance-ai-governance) (and the right people in your organization) if the workflow:

- sends confidential, customer or employee data to an AI model or outside service ([data classification](https://github.com/PythonMuse/accounting_and_finance-ai-governance/blob/main/docs/data-classification.md))
- makes or drives decisions about customers, employees or financial reporting ([risk methodology](https://github.com/PythonMuse/accounting_and_finance-ai-governance/blob/main/docs/risk-methodology.md))
- needs formal approval, a control owner or sign-off evidence ([review and sign-off](https://github.com/PythonMuse/accounting_and_finance-ai-governance/blob/main/docs/review-and-signoff.md))
- supports a SOX or other key control
- raises security, privacy, legal or contractual questions

This repository is about continuity. Those questions are about risk, and they deserve the fuller treatment.

---

© 2026 PythonMuse LLC · MIT License · Educational purposes only, not professional advice.
