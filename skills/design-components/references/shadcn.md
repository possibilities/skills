# Official-first shadcn workflow

Use the project's actual app directory, package manager, CLI version policy,
and installed component owner. Read `components.json` and project guidance;
use `info` for resolved context. Match primitive base, style, aliases, icons,
framework/RSC, Tailwind version, and CSS file before adopting examples.

## Discover with an explicit registry

If the official MCP is available, discover its actual schemas. The verified
tool family includes project registries, list/search, view, examples, add-command
text, and an audit checklist. Useful read shapes are:

```json
{"registries":["@shadcn"],"query":"sidebar","types":["block"],"limit":5}
```

```json
{"registries":["@shadcn"],"query":"combobox","types":["ui"],"limit":5}
```

These are inputs for `search_items_in_registries` on the inspected server;
confirm the current tool name/schema through the host. Use the exact returned
item names. Search behavior, not a vague aesthetic adjective. Omitted registry
lists can exclude the built-in official registry, so keep `@shadcn` explicit.

The MCP is optional. CLI discovery can work without initializing an app; do
not run `init` just to search. Example commands below assume an already
installed pnpm project CLI. Substitute the project-approved runner (such as
`pnpm dlx shadcn@latest`, `npx shadcn@latest`, or `bunx --bun shadcn@latest`)
when appropriate, and inspect version/help before relying on a newer flag.

```sh
pnpm exec shadcn --version
pnpm exec shadcn info --json
pnpm exec shadcn search @shadcn -q sidebar -t block -l 5 --json
pnpm exec shadcn search @shadcn -q combobox -t ui -l 5 --json
pnpm exec shadcn view @shadcn/combobox
pnpm exec shadcn docs combobox
```

Fetch the returned docs URLs before implementing. They establish actual API
usage; a docs command that lists URLs is not the content itself.

## Resolve project context through the CLI

Shared MCP processes need not run in the current app. Changing the agent's
directory does not move their working directory. Inspect full item payloads,
file contents, registry dependencies, targets, and docs through the app's CLI.
For pnpm, `pnpm --dir /absolute/app exec shadcn …` binds the command to the app.

In the 2026-09-29 investigation, local CLI 4.21.0 respected project context,
while the MCP path dropped base/style, returned fallback Radix-style examples,
omitted source in view summaries, and emitted broken add strings in search
results. Its `mcp --cwd` also failed to retarget handlers using process cwd.
Treat these as dated compatibility observations: check current behavior, and
prefer inspected project output over copying command strings or APIs blindly.

Base UI `render` and Radix `asChild` are not interchangeable. No-project results
use fallback configuration and require re-resolution for the selected project.
Raw `view` payloads can contain template imports/icon placeholders; they are
not already transformed installation output.

## Expand without configuring a registry universe

Name the official gap, then inspect a configured source or discover a candidate.
Use a verified namespace, catalog URL, or supported GitHub registry address.
A homepage is not a registry payload: search/list needs a catalog; view/add
needs an item. Do not construct item paths from a provider name alone.

Current CLI supports `owner/repo` catalogs and `owner/repo/item` addresses when
the repository has a valid registry, optionally with `#ref`. Dependencies need
their own provenance; pinning the parent does not pin every transitive item.
Verify current help/docs for the chosen source form.

Search/view can resolve directory-listed namespaces in memory on the inspected
version. Unknown namespaces may not resolve through MCP the same way. Use CLI
or a verified direct URL rather than editing config just to explore. Persist a
namespace only for an adopted recurring/private source that needs configuration.

## Install and inspect

For selected `@shadcn/combobox`, examples of a preview and install are:

```sh
pnpm exec shadcn add @shadcn/combobox --dry-run
pnpm exec shadcn add @shadcn/combobox
```

Use version-supported `--diff`/`--view` for affected files and preserve local
modifications. Blocks can add routes and a dependency tree; select or adapt the
needed parts within the app's existing architecture. Inspect the transformed
files for aliases, icon family, base APIs, missing imports/subcomponents,
semantic tokens, labels, focus, and client/server boundaries. Verify the actual
rendered task and project checks. Use the MCP audit checklist when available
as an implementation aid, not evidence that the UI passed.

Official sources: [MCP](https://ui.shadcn.com/docs/mcp),
[CLI](https://ui.shadcn.com/docs/cli),
[namespaces](https://ui.shadcn.com/docs/registry/namespace),
[GitHub registries](https://ui.shadcn.com/docs/registry/github),
[dynamic search](https://ui.shadcn.com/docs/registry/dynamic-search).
Dynamic search means server-side catalog filtering, not universal semantic
discovery or a design-quality score.
