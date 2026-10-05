# Next discussion: personal Stack role composition

**Operator direction, 2026-09-29:** this repository owns the design skills and
any reusable MCP/CLI connective definitions. Plug those resources into the
operator's personal manager and worker roles. Investigate whether a personal
role can amend a core role; additive personal composition is a required capability
for this integration, even if Stack needs support added.

The portable family is usable independently today. This handoff captures the
next integration decision; it is not a claim that Stack amendments or resource
bindings have been implemented.

## Desired ownership

- **This repository:** canonical skills, family selection, reusable optional
  adapter definitions/contracts, compatibility probes, maintenance provenance.
- **Personal Stack configuration:** which family/adapters each manager/worker
  role selects, personal additions/overrides, and project bindings.
- **Stack:** role composition and validation, credentials, effective capability
  inventory, immutable launch snapshots, process lifecycle, and launch delivery.
- **Application repository:** actual UI dependencies, components/tokens, selected
  registries, project CLI version and app directory.

Prefer a source reference/import through Stack's supported resource system
over hand-maintained copies. A launched role should expose an inspectable
effective set plus source/revision provenance. Updating source should have an
explicit refresh path for future launches; running snapshots retain their
known generation.

## Questions to resolve against current Stack

1. Can a personal role extend/amend a core manager or worker role? How do base
   updates, resource identity, same-name collisions, and removal/disable work?
2. Can a role bind a skill family from this checkout or a pinned Git source,
   including supporting files, without copying its maintenance records into
   model context? How does a user inspect the resolved source/version?
3. Should manager and worker both receive all six skills, or a common family
   with different optional tool access? Keep useful direct leaf invocation.
4. Where does a project-bound stdio process get its real cwd and package runner?
   Could shared discovery plus explicit per-task CLI execution remain simpler?
5. How are optional HTTP/stdio MCP definitions referenced, enabled, refreshed,
   and inspected in launch preview? How are personal secrets kept out of this
   repository's reusable definitions?

## Recommended first binding to discuss

- Design family in the personal manager and worker effective skill sets.
- Existing official shadcn MCP for bounded official-first discovery, if already
  available; version-aware CLI execution in the consuming app for full inspection
  and changes.
- Optional Shoogle HTTP MCP for a named gap. Avoid duplicating an existing
  connection just because the family is installed.
- Existing Brain/search/scrape and browser/native/PTY capability owners reused
  when present. Xcom and external skill catalogs stay conditional discovery.

The [integration guide](integrations.md) contains verified definition shapes
and the [research notes](../research_notes/Design%20skill%20architecture/shadcn-stack.md)
record earlier source-level role observations. Recheck current implementation
and live resources before deciding amendment semantics: the earlier Roles socket
was unavailable, and its absence establishes no conclusion about inheritance.

Acceptance for the follow-up: inspect the resolved personal manager/worker
roles, verify exactly the selected resources and their provenance in fresh
launches, run one official component discovery with project-base inspection,
and demonstrate one additive amendment plus clean removal without losing
unrelated personal resources or silently replacing core defaults.
