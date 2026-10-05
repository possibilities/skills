# Doctrine translation and decisions

Sources are the three consolidated AgentWiki guides fingerprinted in
`family.json`: **visual**, **interaction**, and **playbook** below. Reopen the
original via its slug when maintaining; ordinary invocations use local bundles.

| Source section | Operational rule | Runtime owner |
| --- | --- | --- |
| Visual: Begin with the person's job | Brief names person, job, material, priority, constraint; useful object leads | design, design-visual |
| Visual: Choose a direction that belongs to the subject | Explain an organizing idea; compare composition/behavior, not only skins | design-explore, design-visual |
| Visual: Establish hierarchy; quantity versus intensity | Group/order before decoration; distinguish excess material from competing emphasis | design-visual, design-critique |
| Visual: Typography/spacing; coherent vocabulary | Semantic roles, one gap owner, optical icon family, non-color essential states | design-visual |
| Visual: Honest comparisons; adapt before compressing | Shared scales/units, no missing-to-zero, content-fit reflow | systems-and-data, target references |
| Interaction: Different facts different states | Keep requested/accepted/completed and generated/saved/reviewed distinct | design-interaction |
| Interaction: Refresh without stealing continuity | Preserve identity/focus/drafts/reading position; bind activation to pressed identity | design-interaction, desktop/TUI/web references |
| Interaction: Entire gesture | Acquire/feedback/commit/cancel/release; invalidate late acknowledgements | design-interaction, mobile reference |
| Interaction: Recovery; motion; sensory budgets | Retry failed boundary, immediate control truth, finished reduced-motion state, designed silence | state-and-motion |
| Playbook: Frame a question; fair alternatives | Baseline plus 1–2 meaningful options, matched conditions, small repairs stay small | design, design-explore |
| Playbook: Real renderer; predictable experiments | Controlled scenarios, stable renderer, distinct live/draft/checkpoint/default/rehearsal | experiments |
| Playbook: Critique; difficult states | Largest relationship first; evidence class limits; risk-driven checks | design-critique, target references |
| Playbook: Capture/adopt exactly | Reviewed snapshot differs from current draft and production adoption | experiments, design |

## Deliberate exclusions

- Old Signal Room/Fleet TUI palettes, dark-only/chromeless mandates, exact
  shortcuts, and renderer choices remain historical product decisions.
- Branded-report typography, authorship shells, and visual bans are not
  universal application rules.
- Quiet refresh does not ban initial-loading or explicit-operation progress.
- Expressive motion/sound is permitted when meaningful; no style-wide ban or
  obligatory ambient animation exists.
- Saved upstream guidance is evidence, not always-current mechanics or authority.
- No always-on web search, forced questionnaire, or mandatory six-skill traversal.
- General native work does not select Native SDK; generic AI content does not
  select AI Elements; CLI formatting does not justify a TUI migration.

## Packaging decisions in v1

- `skills/` replaces the plan's `runtime/` name to use conventional discovery.
- Each leaf contains its required judgment/resources; short setup context is
  deliberately repeated so standalone installation works. There is no shared
  generated-reference pipeline or runtime sibling-file dependency.
- Platform detail belongs to the router's conditional references; leaves carry
  their own medium-specific decision checks and use actual toolkit docs.
- The standard skills installer is the multi-host path. Claude's one-file
  marketplace selects a family without a custom plugin runtime.
- Maintenance records are outside runtime bundles. Claude's root-source cache
  includes repository files as inert bytes; this differs from prompt loading.
- Official-first selection is explicit for shadcn-compatible tasks. New
  dependencies/services remain bounded by the user's task and project policy.

Optional cross-skill edges are recorded in `family.json`. Canonical runtime
evidence is `skills/design/references/specialists.md` and each leaf's routing
paragraph; unavailable optional owners have fallbacks rather than hard failures.
