# Evaluation scope

The initial executed set is cases 1–4: bounded web repair, native event identity,
CLI/TUI contract separation, and standalone component selection. Each runs once
with the relevant family guidance and once without it, using identical evidence
and no live app/network actions. Case 4 loads only `design-components` and its
own references. Raw results/reviewer files live in ignored `design-workspace/`.

## Why these checks

The independent contracts are user scope, existing stack/public interfaces,
truthful evidence, interaction identity, and component compatibility. Credible
regressions include unnecessary framework replacement, decorative redesign of
a bounded bug, accepting a stale gesture acknowledgement, breaking machine
output, copying an incompatible MCP example, and reporting unperformed tests.
No existing behavioral evaluation in this new family covers these boundaries.
The checks operate on task answers and require no test-only production seam.

Assertions describe observable recommendations and claims, not required phrases
or implementation structure. Agent grading is a review aid, not proof that an
app works or that a human will prefer its design. One run per configuration is
a smoke comparison, not a variance study. Prompts deliberately expose the key
constraints, so strong baselines may pass too; do not claim uplift from ties.

Cases 5–8 are planned coverage. Cases 6 and 7 require real evidence fixtures
before execution; case 8 belongs in a host trigger evaluation. The initial
comparison is explicit skill loading through file access, not a claim of
automatic triggering or end-to-end model use in every host.

For a fuller iteration, add an actual implementation fixture, real screenshots,
native/PTY interactions, a less-scaffolded component discovery task, and human
preference review. Preserve the baseline and record failures before revising.
