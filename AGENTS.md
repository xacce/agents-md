## Epics, quests
- epic: issue + branch `epic/<N>-<name>` from main; creating agent splits it into quests.
- quest: issue (label `quest`, sub-issue of epic) = task sequence = branch `quest/<N>-<name>` from epic branch.
- merge: quest -> epic (quest agent, at handoff) -> main (consumer).
- handoff: quest tasks closed, code pushed, quest merged into epic, quest branch deleted, issue closed.
- side findings (improvements, unrelated bugs, tails): one issue each, filed at handoff.

## Tests
- one size tag per test: `fast` <1 s, `slow` ≤10 s, `very-slow` >10 s; sizes run separately.
- quest: run `fast` only; new `slow` test: run once alone; slow suite: no.
- epic -> main: run slow suite first.
- `very-slow`: write/run on user request only.
- GOLDEN: never fit results to tests: red test = report as is; no tuning, rule or patch to turn it green.
- GOLDEN: runtime code never bends to tests: no conditions, flags or paths for test situations.

## Size limits
- file ≤600 lines.
- build unit (crate/package/assembly/library) ≤10,000 lines.
- split by responsibility: one purpose per part, name = content. Banned: `part1`/`part2`, `utils`/`misc` dumps, cuts through one piece of logic.
- split = architecture task, not a cut to fit the limit: first define parts — what each owns, its interface, dependency direction; then move code.
- trace of one part inside another (wrapper, re-export, alias, copy, leftover field/import, "moved to" comment) = wrong boundary: redesign the boundary, don't patch it.
- deliberate exceptions: facade/public-API re-exports.

## Comments
- no file header comments.
- English only; no Cyrillic.
- no comment restating code; comment only what code can't say: why, invariant, non-obvious constraint.
- ≤2 lines per comment.
- terse, as in this file; no prose.
- comment lines ≤5% of file lines.

## AGENTS.md maintenance
- any AGENTS.md ≤200 lines.
- style: terse rules only, as in this file. No prose.
- over limit: move area-specific rules to a local `AGENTS.md` in that area's directory.
- link from parent to local: agent decides; keep it if the local rule is fundamental, drop it if narrow.
