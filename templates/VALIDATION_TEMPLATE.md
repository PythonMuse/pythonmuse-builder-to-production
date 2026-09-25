# Validation: [Workflow name]

<!-- Two jobs: (1) prove the workflow works, once, before relying on it;
     (2) tell the monthly reviewer what to check every run. -->

**The workflow running without an error does not mean the accounting result is correct.**

## 1. Test evidence

Tested on period:            Tested by:            Date:            Version / commit:

Expected results were worked out independently (by hand, or from the manual process) **before** running the workflow.

| Check | Expected | Actual | Agrees? |
|---|---|---|---|
| | | | |

Differences found and how they were resolved:

## 2. Monthly review checklist

Each run, the reviewer confirms:

- [ ] Output is for the right period (Control tab / provenance matches the reporting period)
- [ ] Total agrees to <!-- GL account / source report -->
- [ ] Record count agrees to source (<!-- report name -->)
- [ ] Every exception reviewed and explained or escalated
- [ ] Differences over <!-- threshold --> investigated
- [ ] Reviewer name and date added to the output

## 3. What to do when it doesn't tie

<!-- Who to tell, where to record it, whether the output can still be filed. -->
