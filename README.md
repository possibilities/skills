# Skills

Portable, independently usable agent skills for **Claude Code, Codex, and
OpenCode**. This is a collection: new skills and families live alongside the
first family, **design**.

## Install

Use the standard [skills CLI](https://github.com/vercel-labs/skills) from the
project where you want the skills. With this checkout available locally:

```sh
npx --yes skills@1.7.0 add /absolute/path/to/skills \
  --skill design design-explore design-visual design-interaction design-components design-critique \
  --agent claude-code codex opencode -y
```

Replace the path with this repository's actual location. Add `-g` for a
user-wide installation. After these files are published to GitHub, the same
command can use `possibilities/skills` instead of the local path. Version 1.7.0
is the installer exercised for this collection; `@latest` follows its upstream.

The installer copies the selected complete bundles into `.agents/skills` and
links Claude's skill directory to them. Codex and OpenCode read the shared
directory. No application runtime, custom loader, or required MCP is involved.

| Agent | Invoke the entrypoint |
| --- | --- |
| Claude Code, standalone install | `/design` |
| Codex | `$design` or select it through `/skills` |
| OpenCode | `/design` / skill ID `design` |

Use a fresh session after installation if the current catalog does not refresh.
For updates, removal, a native Claude plugin, and role-based delivery, see
[installation](docs/installation.md).

## Design family

| Skill | Use it for |
| --- | --- |
| [design](skills/design/SKILL.md) | Entry point: frame the job, route the next decision, implement/review, and verify |
| [design-explore](skills/design-explore/SKILL.md) | Compare a baseline and meaningful alternatives |
| [design-visual](skills/design-visual/SKILL.md) | Hierarchy, composition, type, spacing, color, data, and visual systems |
| [design-interaction](skills/design-interaction/SKILL.md) | Truthful state, focus, gestures, cancellation, continuity, motion, and recovery |
| [design-components](skills/design-components/SKILL.md) | Find, inspect, and adopt compatible components/blocks |
| [design-critique](skills/design-critique/SKILL.md) | Prioritized evidence-backed findings and bounded repairs |

The router loads only useful specialists and platform references. Each leaf
also works alone. It preserves existing frameworks, accepted design choices,
and public contracts, and asks for evidence appropriate to mobile, desktop,
CLI, TUI, or web rather than treating every app as a website.

Examples (use your agent's invocation form):

```text
/design explore a one-handed capture flow for this Android app
/design repair the wrong-item first click in this macOS arrival panel
/design make jobs list readable without changing JSON or pipe behavior
/design audit this Ratatui view at 48 columns and shallow height
/design build a filter bar using our existing Base UI components
/design-critique review this screenshot; give findings before editing
```

### Dynamic component discovery

The default ladder is **existing project → official library → vetted sources
for a named gap → broader discovery → source inspection → scoped adoption**.
For matching shadcn projects, official means explicit `@shadcn` searches, with
the project CLI resolving actual base/style/dependencies and file targets.
Shoogle's HTTP MCP is an optional broader name-search adapter. Awesome lists,
Brain, Xcom, and skill catalogs supply leads, with upstream verification.

[Optional tools and MCP setup](docs/integrations.md) covers official shadcn,
Shoogle, Stack Roles, and fallbacks. The skills work with available capabilities;
installing this collection does not configure services or add UI dependencies.

The next Stack integration discussion is captured in the
[personal manager/worker role handoff](docs/stack-integration-handoff.md): this
repo owns the resources, and personal roles should compose them additively.

## Maintaining the collection

Canonical runtime bundles are in `skills/`. [Maintenance records](maintenance/README.md)
live separately: provenance, versions, source validation, routing decisions,
evaluation cases, and outcomes. They are not linked into ordinary skill loading.
See [contributing](CONTRIBUTING.md) for adding a skill or releasing a family.

The [original architecture plan](reports/Design%20skill%20architecture.md) and
[research notes](research_notes/Design%20skill%20architecture/) preserve the
reasoning and dated probes behind v1. Current implementation and validation
status is recorded in [the design release record](maintenance/design/CHANGELOG.md).
