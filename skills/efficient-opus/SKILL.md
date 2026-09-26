---
name: efficient-opus
description: Use when running Claude Opus 5.5 on codebase-heavy or token-heavy work and the user wants Opus 5.5 to orchestrate research, coding, and testing with Grok 4.6 High subagents.
---

# Efficient Opus 5.5

Use Claude Opus 5.5 as the orchestrator, architect, synthesizer, and final judge.
For every subagent delegated under this skill, select **Grok 4.6** with
**High** reasoning effort. Do not use another model or reasoning level for a
subagent. If that exact combination is unavailable, keep the work with Opus 5.5
or explain that delegation cannot proceed; do not silently substitute a model.

## Where Opus 5.5 Shines

Reserve Opus 5.5 for:

- Decomposing ambiguous work into clean parallel slices.
- Architecture, product, and safety tradeoffs.
- Reading conflicting subagent reports and deciding what matters.
- Integrating partial implementations into one coherent plan.
- Final review, risk assessment, and user-facing synthesis.

## Delegation Pattern

1. Identify work that benefits from delegation: large repo searches, long
   logs, broad docs, repetitive edits, or targeted validation.
2. Split independent work into bounded tasks before reading everything
   yourself.
3. Start each subagent with Grok 4.6 at High reasoning effort for research
   scans, inventory, search summaries, narrow bug hunts, browser or testing
   passes, test output reduction, and bounded code edits.
4. Ask subagents for concise evidence: files, line references, commands run,
   diffs, uncertainties, and stop conditions they hit.
5. Spend Opus 5.5 tokens on the decision layer: compare results, resolve
   conflicts, choose the implementation path, and review the final patch.

Prefer parallel Grok 4.6 High subagents when the slices do not depend on each
other. Keep blocking or highly coupled work local.

## Handoff Packets

Write delegated prompts as if the subagent has no useful chat context. Include
only the context it needs:

- The repo path and exact objective.
- The files, packages, or surfaces in scope and anything explicitly out of
  scope.
- The evidence format to return: files, line refs, commands, diffs, failures,
  screenshots, and uncertainty.
- The verification commands or browser flows to run, plus what success should
  look like when that is knowable.
- Stop conditions: if the code does not match the prompt, a command fails
  after a reasonable retry, or the task needs out-of-scope files, stop and
  report instead of improvising.

## Vetting Delegated Work

Treat subagent reports as leads, not facts. Before using a high-impact
finding, opening a PR, or telling the user the work is done, Opus 5.5 should
reopen the important cited files, confirm the relevant line refs or failures,
and review the final diff against the task.

## Common Scenarios

Treat these as soft defaults, not rigid rules:

- Research: ask Grok 4.6 High subagents to scan docs, prior art, APIs, and
  repo surfaces; Opus 5.5 decides what evidence changes the plan.
- Coding: give Grok 4.6 High subagents bounded edits or candidate patches;
  Opus 5.5 owns shared-file coordination, integration, and final review.
- Testing: have Opus 5.5 suggest the validation direction and the scripts or
  browser checks that matter. Let Grok 4.6 High subagents run targeted tests,
  browser flows, screenshots, and log reduction, then report exact commands,
  failures, likely causes, and whether failures look flaky, environmental,
  or real.
- Debugging: use Grok 4.6 High subagents to cluster logs, reproduce issues,
  and try small fixes; Opus 5.5 decides which diagnosis is most trustworthy.

If a task is tiny or the validation itself needs delicate judgment, keep it
with Opus 5.5.
