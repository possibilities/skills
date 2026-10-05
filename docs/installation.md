# Installation and lifecycle

The canonical unit is `skills/<name>/`, containing `SKILL.md` and all of its
required resources. The same bytes work with Claude Code, Codex, and OpenCode
V2. Select one delivery method per host/scope to avoid duplicate catalog entries.

## Cross-agent standalone installation

From a consuming project, install the family using the README command. Use
`--skill design-critique` for a single leaf, or deliberately use `--skill '*'`
for the entire evolving collection. Avoid `--all`: it also selects all agents.
To discover the source without installing:

```sh
npx --yes skills@1.7.0 add /absolute/path/to/skills --list
```

Use `possibilities/skills` as the source after publishing. The shared
`.agents/skills` directory is visible to any host that supports that convention;
`--agent` is not an isolation boundary. Project installs create `skills-lock.json`.
Global installs use `~/.agents/skills` and Claude's configured personal directory.

### Refresh and remove

For a **local checkout source**, rerun the same `add` command after editing or
updating the checkout. The installer takes a copy; it does not link to this
source tree. Local-source `update` did not refresh in the verified version.

For a **published Git source**, the documented scoped update is:

```sh
npx --yes skills@1.7.0 update \
  design design-explore design-visual design-interaction design-components design-critique \
  --project -y
```

Use `--global` instead for a global Git-source install. Check the command's
result, not just its exit code; hosted update was not exercised before release.

Remove the standalone family from a project with:

```sh
npx --yes skills@1.7.0 remove \
  design design-explore design-visual design-interaction design-components design-critique \
  --agent claude-code codex opencode -y
```

Add `-g` for the global scope. Codex and OpenCode share canonical bytes in this
installation, so removing that shared directory affects both readers.

## Native Claude marketplace

The marketplace offers the design family as one plugin. More families can be
added independently later. For this local checkout:

```sh
claude plugin marketplace add /absolute/path/to/skills --scope user
claude plugin install design@possibilities-skills --scope user
claude plugin details design
```

After publication, replace the absolute path in `marketplace add` with
`possibilities/skills`. Use `--scope project` for project-scoped marketplace and
plugin operations. Start a new session or use `/reload-plugins`.

The reliable qualified invocation is **`/design:design`** (or
`/design:design-critique`). Current Claude also permits an unambiguous bare
skill alias; standalone installation gives the straightforward `/design` path.
The marketplace name is not the skill namespace.

```sh
claude plugin marketplace update possibilities-skills
claude plugin update design@possibilities-skills --scope user
claude plugin uninstall design@possibilities-skills --scope user
```

Removing the marketplace itself can also remove its other installed families;
use plugin uninstall to remove only design.

The manifest selects exactly six runtime skills. Claude's root-source cache
copies the repository, including research/maintenance, but does **not** load
those records as skills or inject them into prompts. The standalone installer
copies only selected bundles. This package distinction avoids a generated
second copy of every source skill.

## OpenCode authoring checkout

Standalone installation needs no configuration. For live development against
a checkout, OpenCode V2 also supports an explicit source in `opencode.jsonc`:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "skills": ["/absolute/path/to/skills/skills"]
}
```

Use the actual path to this repository's `skills/` directory. This V2 field is
an array, not `skills.paths`. HTTP skill sources mean an OpenCode catalog, not
a Git clone; do not put the repository URL here. Update by changing the checkout;
remove the source entry to remove this delivery. Preserve unrelated settings.

## Stack and other curated roles

Role launchers may intentionally exclude ambient standalone skills. In that
case, add the six complete bundle directories to the selected role through its
supported skill-resource interface, then inspect its effective launch preview
and start a fresh session. Include optional existing specialists only where
useful. See [integrations](integrations.md) for MCP definitions.

This repository owns these source skills. AgentStart's current `agent*` source
scan does not discover it automatically. Do not edit generated role resources
or create a parallel synchronizer; use explicit source/role configuration in
the owning system when integrating that distribution path.

## Verified contracts

Packaging research used skills 1.7.0, Claude Code 2.1.285, Codex 0.159.1, and
OpenCode 2.0.16. See [distribution evidence](../maintenance/distribution-research.md)
and the [release record](../maintenance/design/CHANGELOG.md) for actual checks.
Actual-family checks confirmed Claude's plugin inventory and Codex's native
skill catalog. OpenCode loaded all six from `.agents/skills` in a fresh isolated
session with exact source-body readback and no model execution. A cold skill-list
API response alone was insufficient to test its session initialization. Personal
Stack role composition and model routing remain separate integration checks.
Source references: [Claude skills](https://code.claude.com/docs/en/skills),
[Claude marketplace](https://code.claude.com/docs/en/plugins/marketplace-reference),
[Codex skills](https://developers.openai.com/codex/skills),
[OpenCode V2 skills](https://opencode.ai/v2/docs/skills), and
[skills CLI](https://github.com/vercel-labs/skills).
