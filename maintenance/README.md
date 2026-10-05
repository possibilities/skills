# Non-runtime maintenance records

This directory is for authors and maintainers. Ordinary skill invocations use
`skills/` only; no runtime instruction asks agents to load the history/catalog
here. Standalone distribution copies complete selected bundles; the optional
root-source Claude cache contains this directory as files but does not load it.

Each family owns:

- `family.json`: source owner, version/status, members, route boundaries,
  optional capability edges, provenance fingerprints, and evolution triggers.
- `sources.json`: source/adapter lifecycle and the exact scope/date of evidence;
  candidate status is separate from whether a read-only probe worked.
- `rule-map.md`: source doctrine → operational rule → deliberate exclusions.
- `CHANGELOG.md`: decisions and actual implementation/validation outcomes.
- `evals/evals.json`: realistic scenarios, expected results, and assertions when
  defined. Planned cases are not passing tests.
- `evals/results.json`: only actual runs, grading, limits, and review status.

JSON records carry `schema_version`; update it if meanings change. Distinguish
family version, upstream revision, observed tool version, and verification date.
Do not invent owner approval, license conclusions, performance gains, or test
results. Keep raw model transcripts and generated review workspaces out of
runtime distribution and normal Git history.

The [distribution research](distribution-research.md) records the packaging
contracts and isolated probes used for the initial collection. Design's
[original research](../research_notes/Design%20skill%20architecture/) is a dated
evidence snapshot, not a live inventory or mandatory invocation prerequisite.
