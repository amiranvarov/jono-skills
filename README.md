# jono-skills

Agent skills customized for Jono.

## efficient-fable

The [efficient-fable skill](skills/efficient-fable/SKILL.md) keeps Claude Fable
responsible for orchestration and final judgment. Whenever it delegates to a
subagent, it requires **Grok 4.6** at **High** reasoning effort. If that exact
setting is unavailable, the skill directs Fable to keep the work local or
report that delegation cannot proceed.

## efficient-opus

The [efficient-opus skill](skills/efficient-opus/SKILL.md) follows the same
workflow with **Claude Opus 5.5** as orchestrator and final judge. Every
subagent must use **Grok 4.6** at **High** reasoning effort; if that setting
is unavailable, Opus 5.5 keeps the work local or reports that delegation
cannot proceed.
