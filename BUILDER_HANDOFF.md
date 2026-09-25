# Builder Handoff

Use this when you hand a workflow to someone else: you are changing roles, leaving, going on long leave, or simply want a second person able to run it.

Fill it in, then **walk through it with the new owner while you can still answer questions**. A handoff document written on your last afternoon and emailed at 4:55 p.m. is technically a handoff.

Short answers are fine. Link to the README, Human Instructions and Passport rather than repeating them.

---

**Workflow:**
**Handed over by:**                         **To:**                         **Date:**

| Question | Answer |
|---|---|
| **What does this do?** In one or two sentences, in accounting terms. | |
| **Why was it built?** What was the manual process, and what problem did it solve? | |
| **Who currently depends on it?** People, teams, reports, deadlines. | |
| **Where does it live?** Code, agent, prompts, config, documentation. | |
| **How is it triggered?** Manually, on a schedule, by a file arriving? | |
| **What systems does it access?** | |
| **What credentials are needed?** Whose are they? Do any need moving from a personal account to a service account? | |
| **What assumptions are embedded?** Account numbers, entity lists, mappings, thresholds, file layouts. | |
| **What are the known failure points?** What has broken before, and what fixed it? | |
| **How is the output validated?** Link to VALIDATION.md or describe the tie-outs. | |
| **What changes regularly?** Dates, periods, mappings, new entities, new customers. | |
| **Who can operate it if the builder is unavailable?** Have they actually run it? | |
| **What is the fallback process?** | |

**Before you sign off, check:**
- [ ] The new owner has run it at least once, unassisted, using only the documentation.
- [ ] Access and credentials have been transferred or replaced. Nothing runs on the departing person's login.
- [ ] The [Workflow Passport](WORKFLOW_PASSPORT.md) shows the new owner and backup.
- [ ] Open issues and planned changes are written down, not just remembered.

Handed over: ______________________  Received: ______________________

---

If the builder has already gone and nobody filled this in, use the [Takeover Assessment](TAKEOVER_ASSESSMENT.md) instead.

© 2026 PythonMuse LLC · MIT License · Educational purposes only, not professional advice.
