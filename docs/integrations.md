# Optional design capabilities

The family has no required MCP server. Start with tools already available and
project docs. Skill installation and tool configuration are separate: the
marketplace carries no hooks, executable launchers, or MCP auto-configuration.

## Official shadcn

Use one official server for catalog discovery, not one server per registry.
The portable skills explicitly query `@shadcn`, then inspect actual project
context and source through its CLI. A shared server's cwd is not the app's cwd;
even a project-bound server needs base/style verification on the observed release.

For a pnpm application with shadcn already installed, the process command is:

```sh
pnpm --dir /absolute/path/to/app exec shadcn mcp
```

Host setup examples (replace the app path):

```sh
# Claude: project scope
claude mcp add --scope project shadcn -- pnpm --dir /absolute/path/to/app exec shadcn mcp

# Codex: native personal MCP configuration
codex mcp add shadcn -- pnpm --dir /absolute/path/to/app exec shadcn mcp

# OpenCode V2: project scope
opencode mcp add shadcn -- pnpm --dir /absolute/path/to/app exec shadcn mcp
```

If the CLI is not installed, follow the project's package-manager/version
policy and [official MCP setup](https://ui.shadcn.com/docs/mcp). A tool-discovery
task does not require initializing a shadcn app. Launching `mcp --cwd <app>` was
not sufficient to retarget handlers in the inspected 4.21.0 release; actual
process cwd matters. For monorepos, the application package can differ from
repository root. Verify `info`, base-specific docs, and full `view` output.

## Shoogle HTTP MCP

Verified endpoint: `https://mcp.shoogle.dev/mcp`. Its two tools search item names
globally or within returned registry identifiers. Semantic/layout search is
not established for this MCP. Use it only when a named requirement remains
after official/configured sources. Serialize bounded calls and inspect errors.

```sh
# Claude: project scope
claude mcp add --scope project --transport http shoogle https://mcp.shoogle.dev/mcp

# Codex: native personal MCP configuration
codex mcp add shoogle --url https://mcp.shoogle.dev/mcp

# OpenCode V2: project scope; add --global for user scope
opencode mcp add shoogle --url https://mcp.shoogle.dev/mcp
```

Check each host's MCP connection/catalog after setup. On the verified snapshot,
Shoogle required no authentication. These setup commands were checked against
CLI help/docs; they are instructions, not claims of changes to your settings.
Source: [Shoogle connection docs](https://shoogle.dev/mcp/other-mcp-clients).

WebMCP is a future optional route only if a useful page actually exposes tools
and the current browser can enumerate them. No Shoogle WebMCP dependency or
guessed page API is shipped here.

## Stack Role definitions

For the operator's Stack integration, the intended owner is this repository,
composed into personal manager and worker roles. The next step is to verify
additive role-amendment support; see the
[personal role integration handoff](stack-integration-handoff.md).

Stack Roles support these external MCP definition shapes (normal Role resource
metadata such as name/enabled is managed by the Role interface):

```json
{
  "type": "stdio",
  "command": "pnpm",
  "args": ["--dir", "/absolute/path/to/app", "exec", "shadcn", "mcp"]
}
```

```json
{
  "type": "http",
  "url": "https://mcp.shoogle.dev/mcp"
}
```

A shared role can use project-independent official discovery and execute
project CLI work with an explicit app directory. Stack's inspected stdio schema
has no `cwd` field; `pnpm --dir` supplies process context. Do not invent a
project interpolation field. Preview effective skills/MCPs using the supported
`role_launch_preview` contract before a fresh launch; `cwds` there is for trust
matching, not MCP rebinding. Existing launch snapshots do not hot-reload.

Live Role deployment was not established by the research; the Roles socket was
absent. These are source-verified integration definitions, not installed resources.
Use Stack's supported resource owner rather than `shadcn mcp init` writing a
second host configuration underneath it.

## Other routes

Existing `shadcn`, `ai-elements`, `ai-sdk`, React guidance, `native-sdk`, web
audits, `desktop`, and `terminal-control` remain optional specialist owners.
Browser/device/PTY capabilities determine what can be verified. Brain supplies
saved evidence; search/scrape supply current sources. Xcom and UI Skills can
nominate useful discoveries, but no service is assumed to exist and fetched
guidance is not automatically installed. The runtime
[discovery reference](../skills/design-components/references/discovery.md)
contains the bounded selection workflow.
