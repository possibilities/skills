# Maintaining a portable skill collection

## Add a skill

1. Create `skills/<lowercase-kebab-name>/SKILL.md` with YAML `name` matching the
   directory and a concrete `description` explaining when to use it.
2. Write an independently useful workflow. Put needed resources inside that
   directory and link them relatively with a condition for loading. A leaf
   should work when installed without its family. Avoid absolute machine paths,
   host-only substitutions, required sibling files, and implicit tool installs.
3. Keep runtime content focused on the task. Put ownership, provenance,
   compatibility, evolution, and evaluation records in `maintenance/<family>/`.
4. Add the skill to its Claude marketplace family's explicit `skills` list,
   or add a new family entry. This repo has a marketplace-owned manifest; do
   not add a conflicting root `plugin.json`. Future families need not load design.
5. Update README discoverability and installation examples where appropriate.
   Bump the family version for released changes so Claude caches refresh.

The skill's advertised metadata is the discovery surface. Do not create another
runtime mega-catalog, preconfigure dozens of MCPs, or copy upstream skills whose
owners already provide current implementation guidance. Resolve optional skills
through the current host catalog, including namespaced plugin identifiers.

## Check a release

From the repo root:

```sh
npx --yes skills@1.7.0 add . --list
claude plugin validate . --strict --json
git diff --check
```

The native validator checks the marketplace schema, not every skill's behavior
or reference. Inspect YAML frontmatter and Markdown links. Every required local
link must resolve inside the individual bundle. Check all metadata JSON parses
and every manifest path names a complete skill. Keep skill bodies comfortably
below 500 lines and inspect load size rather than rewarding brevity alone.

Exercise the README installer against an **isolated consuming directory/home**
and compare complete installed bundles with source. Verify selecting one leaf
keeps its references, selecting a family excludes unrelated skills, and removal
removes the corresponding owned install. For Claude, inspect plugin details
after an isolated marketplace install. The standalone path excludes maintenance
bytes; the root-source Claude cache includes them but loads only declared skills.
See [the exact lifecycle probe](maintenance/distribution-research.md#disposable-lifecycle-probe).

Use realistic behavioral scenarios for workflow changes. Keep prompts and
expected results under maintenance; store raw local model runs in an ignored
`<family>-workspace/`. Review results with and without the skill where useful.
Assert observable behavior (scope, decisions, evidence honesty, compatibility),
not literal phrases or a preferred aesthetic. Record actual outcomes separately
from proposed cases. Do not claim host/model/device coverage that was not run.

## Evolve deliberately

Reopen source guidance when its fingerprint changes, an adapter fails, a major
release changes APIs, or repeated human corrections expose a general lesson.
Separate project taste from universal defects. Prefer a bounded correction and
a relevant example over accumulating rules. Merge a leaf that becomes only
forwarding boilerplate; split only a genuinely useful independent workflow.

Publishing and live role installation follow their existing owners. Local
authoring does not automatically publish Git changes or alter personal agent
configuration. Keep research snapshots dated and use the release record to
describe current implementation and verification.
