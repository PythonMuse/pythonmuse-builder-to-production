# Takeover Assessment

The builder has already left. Nobody filled in a handoff. You just found a script, an agent or a flow that the close apparently depends on.

Don't panic, and don't assume it's either brilliant or broken. Work through it in order.

## The path

**Discover → Stabilize → Understand → Decide**

### 1. Discover: what is it and who needs it?

- [ ] **Is it currently running?** On a schedule, manually, or not at all since the builder left?
- [ ] **Who depends on it?** Which reports, reconciliations, people and deadlines use its output?
- [ ] **Can we access it?** The code, agent, prompts, config and output folders. Is any of it in a personal account?

Start a [Workflow Passport](WORKFLOW_PASSPORT.md) now, even with gaps. Write "unknown" freely.

### 2. Stabilize: keep the close running

- [ ] **Are credentials still valid?** Personal logins and API keys often die with the builder's account.
- [ ] **Is there a manual fallback?** If not, write down how the work was done before, while someone still remembers.
- [ ] Take a copy of the code and the last few outputs before anyone changes anything.

The goal of this step is that next month's close happens, with or without the workflow.

### 3. Understand: can we trust it?

- [ ] **Can we reproduce previous results?** Rerun a prior period and compare to the filed output.
- [ ] **Do we understand the business logic?** Exclusions, mappings, thresholds, hard-coded accounts. (This is where AI earns its tokens: ask it to explain the code and list every assumption, then verify what it says.)
- [ ] **Is the underlying technology supported?** Is the platform, library or AI model still available and approved?
- [ ] **Is the documentation sufficient?** Could the [Lottery Test](LOTTERY_TEST.md) be passed today?

### 4. Decide

| Decision | Choose it when |
|---|---|
| **Maintain** | You can reproduce past results, you understand the logic, the technology is supported and someone can own it. |
| **Rebuild** | The logic is sound but the implementation is fragile, undocumented or on an unsupported platform. |
| **Replace** | A standard system feature or an existing company tool now does the same job. |
| **Retire** | Nobody really needs the output any more, or the manual process is safer at this volume. |

Questions to settle before deciding:
- **Can another employee maintain it?** Not "could someone, in theory." Who, specifically?
- **Would rebuilding be safer or cheaper?** Sometimes rebuilding from a clear spec is faster than reverse-engineering someone else's midnight code.

**Keeping it is not the default.** "It's been running, so leave it" is how an unowned workflow becomes an unowned control. Each option needs a reason, including Maintain.

Write down the decision, who made it and why. If you maintain or rebuild, continue with [Production Readiness](PRODUCTION_READINESS.md).

---

© 2026 PythonMuse LLC · MIT License · Educational purposes only, not professional advice.
