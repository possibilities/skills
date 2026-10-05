# Official shadcn discovery, MCP/CLI, and Stack integration for `/design`

Research date: **2026-09-29**. Read-only investigation; no installs, project/config edits, builds, deployments, or runtime skill files. Local Stack inspection used `/Users/arthack/code/stack/AGENTS.md`. Official source was inspected at commit **`08ab84f7d1952cc1f36055aa8931213a86b01bbd`**, returned by GitHub as current `main`, committed **2026-09-29T17:23:29Z**. The already-installed Stack UI CLI reports **4.21.0**. The live session MCP is launched through AgentStart's floating `shadcn@latest`; its precise package version was not exposed by the session tool catalog. A separately launched local 4.21.0 MCP reports protocol `serverInfo.version: "1.0.0"`, which must not be mistaken for the CLI package version. [Official source snapshot](https://github.com/shadcn-ui/ui/tree/08ab84f7d1952cc1f36055aa8931213a86b01bbd); [local package](file:///Users/arthack/code/stack/packages/ui/package.json); [current launcher](file:///Users/arthack/code/agentstart/scripts/agentstart)

## 1. What official discovery and MCP capabilities actually work today?

### Takeaway

**Use the official MCP for bounded discovery, and the project-local CLI for complete, project-compatible inspection and installation.** The MCP has useful explicit registry/type/pagination searches, but observed shortcomings make it unsuitable as the sole source of install commands, full payloads, or Base UI examples.

### Cited Findings

- **Prior knowledge searched first:** `agentbrain.context({query:"shadcn MCP registry Stack",limit:4,"max-chars":8000})` returned adjacent material, not a direct answer: document 517/chunk 7874, *A curated list of exceptional resources and tools related to shadcn/ui*, source `https://github.com/bytefer/awesome-shadcn-ui`; document 917/chunk 13703, *json-render*, source `https://github.com/vercel-labs/json-render`; document 731/chunk 10627, *Inside v0 Design Systems 2.0*, source `https://x.com/i/status/2075589636227735902`. These were background only; claims below rely on current official material and local observations. [Saved curated source](https://github.com/bytefer/awesome-shadcn-ui); [saved renderer source](https://github.com/vercel-labs/json-render)
- **Seven actual MCP tools were discovered in this session**, matching the current source: `get_project_registries`, `list_items_in_registries`, `search_items_in_registries`, `view_items_in_registries`, `get_item_examples_from_registries`, `get_add_command_for_items`, `get_audit_checklist`. There is **no install tool and no `init_project` tool** in that inventory, despite tool descriptions mentioning `init_project` and docs describing installation through natural language. The add-command tool returns text; the agent must separately execute a CLI command to install. [MCP implementation][mcp-source]; [official MCP docs][mcp-docs]
- The current search schema accepts optional registry strings, a required query, optional type strings, and pagination. Types advertised are `lib`, `block`, `component`, `ui`, `hook`, `page`, `file`, `theme`, `style`, `item`, `base`, `font`. There is no semantic requirement-fit, accessibility, performance, license, or maintenance filter. Static catalogs are fuzzy-matched locally against name/title/description. [Search implementation][search-source]; [MCP schema][mcp-source]

Actual exposed tool signatures, discovered through this harness's Code Mode catalog:

```ts
tools.shadcn.get_project_registries(): Promise<unknown>
tools.shadcn.search_items_in_registries({
  registries?: string[], query: string, types?: string[],
  limit?: number, offset?: number
}): Promise<unknown>
tools.shadcn.list_items_in_registries({
  registries?: string[], types?: string[], limit?: number, offset?: number
}): Promise<unknown>
tools.shadcn.view_items_in_registries({items: string[]}): Promise<unknown>
tools.shadcn.get_item_examples_from_registries({
  registries?: string[], query: string
}): Promise<unknown>
tools.shadcn.get_add_command_for_items({items: string[]}): Promise<unknown>
tools.shadcn.get_audit_checklist(): Promise<unknown>
```

These are **observed session schemas**, supported by [the official implementation][mcp-source]. `limit` defaults to 100; its description says 0 means unlimited. Prefer a small explicit limit for discovery.

**Actual read-only calls and outputs, 2026-09-29:**

| Call | Observed output | Consequence |
| --- | --- | --- |
| `get_project_registries()` | Only `@shadcn` | An official-only discovery baseline already exists in this session. |
| `search_items_in_registries({registries:["@shadcn"],query:"sidebar",types:["block"],limit:5})` | **17 matches**; first five `sidebar-02`, `sidebar-04`, `sidebar-05`, `sidebar-06`, `sidebar-08`; names, descriptions, `registry:block`, next offset 5 | Dynamic enumeration works; no need to maintain a static block list in `/design`. |
| `search_items_in_registries({registries:["@shadcn"],query:"combobox",types:["ui"],limit:5})` | One `combobox` item, `registry:ui` | Components and blocks can be queried separately. |
| Both searches above | Every displayed add command was **`[object Promise]`** | Do not copy commands from search text. |
| `get_add_command_for_items({items:["@shadcn/sidebar-08","@shadcn/combobox"]})` | `npx shadcn@latest add @shadcn/sidebar-08 @shadcn/combobox` | Explicit command tool works, but this runner reflects the service cwd, not Stack's pnpm project. |
| `view_items_in_registries({items:["@shadcn/sidebar-08","@shadcn/combobox"]})` | Sidebar: description, type, **6 files**. Combobox: type, **1 file**, dependencies `cn, @base-ui/react`. **No file contents or registryDependencies** | Contrary to its description, MCP view is only a summary. Use CLI `view` to inspect the full payload. |
| `get_item_examples_from_registries({registries:["@shadcn"],query:"button-demo"})` | Two full examples, `button-demo` and fuzzy extra `button-group-demo`, paths under **`registry/new-york-v4/examples/`**; group demo uses **`DropdownMenuTrigger asChild`** | Examples are real code but neither exact-match nor reliable project-base selection. |
| `search_items_in_registries({query:"sidebar",types:["block"],limit:2})` | “No registries are configured…or pass them explicitly.” | Omitting the registry does not search built-in `@shadcn`. |
| `search_items_in_registries({registries:["https://ui.shadcn.com/r/styles/base-nova/registry.json"],query:"sidebar",types:["block"],limit:2})` | 17 results; first two `sidebar-02`, `sidebar-04` | **Direct catalog URLs work in MCP** despite registry-name-only descriptions. |
| `view_items_in_registries({items:["https://ui.shadcn.com/r/styles/base-nova/button.json"]})` | Button metadata, 1 file, dependency `cn` | **Direct item URLs work in MCP**; output still omits code. |

Reproduction contracts and source explanations for this table: [MCP handler][mcp-source], [MCP formatters][mcp-utils], [official base-nova catalog](https://ui.shadcn.com/r/styles/base-nova/registry.json), [sidebar item](https://ui.shadcn.com/r/styles/base-nova/sidebar-08.json), [combobox item](https://ui.shadcn.com/r/styles/base-nova/combobox.json). These are session observations, not claims that every MCP release behaves identically.

- **The Promise defect has a source-level explanation:** `npxShadcn()` is async, but `formatSearchResultsWithPagination()` interpolates it without awaiting. The standalone add-command handler does await it. `formatRegistryItems()` explicitly renders only metadata/counts/direct dependencies, explaining the missing payload. [MCP utility source][mcp-utils]
- **Official code inspection works through CLI:** from Stack's `packages/ui`, `pnpm exec shadcn view @shadcn/sidebar-08 @shadcn/combobox` returned complete JSON including `files[].content`, `target`, `registryDependencies`, and docs links. Sidebar is a Base Nova block with an `app/dashboard/page.tsx` target and dependencies `sidebar`, `breadcrumb`, `separator`, `collapsible`, `dropdown-menu`, `avatar`. Its navigation uses Base UI `render={...}`. Combobox uses `@base-ui/react` and depends on `button` and `input-group`. Registry payloads still contain template imports and `IconPlaceholder`; **raw `view` output is not transformed install-ready application code**. [CLI view source][view-cli]; [sidebar JSON](https://ui.shadcn.com/r/styles/base-nova/sidebar-08.json); [combobox JSON](https://ui.shadcn.com/r/styles/base-nova/combobox.json)
- **Current CLI help is ahead of its general docs:** local 4.21.0 `search --help` supports optional registries, `--type/-t`, `--json`, GitHub sources, and URLs. The current `/docs/cli.md` search synopsis omits `--type`/`--json` and still shows required registries. Source and observed help agree. [Current search CLI source][search-cli]; [general CLI docs][cli-docs]
- **Roadmap boundary:** Registry Health docs explicitly say “experimental and not live yet”; scores are collected but do not affect visibility/ordering, and future ranking/filtering/UI are separate. Even its proposed score concerns availability/schema/installability, **not design quality, code quality, popularity, or accessibility**. Do not build `/design` selection around an assumed operational health-ranking API. [Registry Health](https://ui.shadcn.com/docs/registry/health.md)

### Inferences

- A thin router can ask MCP for 5–10 relevant official items, inspect 2–3 using project-local CLI plus component docs, and stop once there is a credible fit. MCP is a catalog interface, not an autonomous component evaluator.
- Treat “components,” “blocks,” and “examples” as separate useful discovery shapes. A block can introduce routes and several components; it should not be installed as if it were one harmless primitive.
- Prefer composable official primitives already present locally before a new whole block. The sidebar block above is a demonstration of why route targets and dependency closure belong in selection evidence.

### Gaps

- No candidate has been installed, built, rendered, profiled, or accessibility-tested in this investigation. “Official” is provenance, not an accessibility/performance certification of a composition.
- The live session MCP's exact npm package version remains unverified. Its discovered tools and outputs are recorded above; current-source explanations are pinned to a dated commit.
- No actual community gap was requested for this research, so no community candidate sweep was performed.

## 2. How do cwd, project configuration, namespaces, and dynamic registries interact?

### Takeaway

**Make `@shadcn` explicit on every official-first discovery call, and make the real application directory explicit for CLI work.** Namespaces, direct URLs, and GitHub addresses are current capabilities; server-side “dynamic search” is a different feature from discovering a new registry on demand.

### Cited Findings

- **The session MCP is intentionally project-independent:** installed role `mcp.json` invokes `/Users/arthack/.local/bin/agentstart mcp shadcn`. AgentStart runs `npx --prefix / --yes shadcn@latest mcp` with its fixed resource directory as cwd. The installed resource `components.json` has `style: "radix-nova"`, `rsc:false`, and `registries:{}`. Thus a session changing directories or targeting Stack does not retarget this MCP. [Installed role entry](file:///Users/arthack/.local/share/agentstart/resources/roles/default/mcp.json); [launcher lines 77–85](file:///Users/arthack/code/agentstart/scripts/agentstart); [fixed config](file:///Users/arthack/.local/share/agentstart/resources/shadcn/components.json)
- **MCP also discards project styling independently of that wrapper:** `getMcpConfig()` returns only `registries`; `getRegistriesConfig()` loads registry declarations, not style/base/aliases. The handler passes that reduced config into registry APIs, whose defaults choose a fallback style. Therefore even launching the server in Stack's UI directory does **not** prove examples/items are Base Nova. This explains the observed `new-york-v4` examples; direct style-specific URLs or the full project CLI are the useful workarounds. [MCP config helper][mcp-utils]; [registry API][registry-api]; [config defaults][registry-config]
- **`mcp --cwd` currently fails to retarget tool reads.** The flag exists, but command startup only calls `loadEnvFiles(options.cwd)`; tool handlers use `process.cwd()`. Direct read-only MCP probes of installed 4.21.0 confirmed this:
  - Process cwd `/Users/arthack/code/skills`, args `mcp -c /Users/arthack/code/stack/packages/ui`: `get_project_registries` printed an empty registry list; add-command tool used `npx`.
  - Process cwd `/Users/arthack/code/stack/packages/ui`, args `mcp`: registry list contained `@shadcn`; add-command tool used `pnpm dlx`.
  - Both probes only initialized MCP and called registry/command-text reads, then terminated the process. [MCP command source lines 90–106][mcp-cli]; [tool handlers][mcp-source]
- **No per-call cwd is in the exposed schemas.** The internal list parser happens to accept an unused `cwd`, but it is not an exposed or effective project-selection mechanism. Use actual process cwd for a project-bound server. `pnpm --dir /Users/arthack/code/stack/packages/ui exec node -p 'process.cwd()'` was observed to print precisely that directory. [MCP handler][mcp-source]; [Stack package manager declaration](file:///Users/arthack/code/stack/package.json)
- **Omitted registry lists exclude built-ins:** shared `resolveSearchRegistries()` filters `BUILTIN_REGISTRIES` out when given no explicit addresses. In Stack, `registries:{}` is legitimate: `info` includes implicit `@shadcn`, but bare `pnpm exec shadcn search --json` fails “No registries are configured.” Explicit `@shadcn` works. [Resolver][search-source]; [Stack config](file:///Users/arthack/code/stack/packages/ui/components.json)
- **Discovery need not initialize a project.** Actual call from the installed CLI, `pnpm exec shadcn search @shadcn -q sidebar -t block -l 2 --json -c /Users/arthack/code/skills`, succeeded without a `components.json` there: total 17, first two sidebar blocks, structured `addCommandArgument`. Search and view create in-memory fallback configurations; no `init` is required. No-project results use fallback style and still need compatibility re-resolution before installation. [Search CLI][search-cli]; [view CLI][view-cli]
- MCP descriptions claiming `components.json` is strictly required are stale relative to implementation: explicit built-in names/URLs can resolve through defaults, while `getRegistriesConfig()` supports `package.json` registries and merges `components.json` per key when present. Empty config listing is not a reliable initialized-project check. [Registry API, `getRegistriesConfig`][registry-api]; [MCP helper][mcp-utils]
- **Namespace config:** `@name/item` uses a registry URL template, commonly `https://host/r/{name}.json`; `{style}` is optional. Object config supports URL, headers, and params with environment-variable substitution. `@shadcn` is built in. This is a registry alias/configuration system, not a per-provider MCP requirement. [Namespaces][namespace-docs]
- **New namespace discovery differs between MCP and CLI:** CLI `search` and `view` call `ensureRegistriesInConfig` with **`writeFile:false`**; missing aliases can be resolved from package declarations and the official registry directory **in memory**. MCP search goes directly through configured registry mappings/defaults and has no equivalent directory-discovery step. For an unknown community source, pass a verified direct catalog URL or use CLI discovery rather than silently editing `components.json`. [Search CLI][search-cli]; [view CLI][view-cli]; [registry discovery source][registry-discovery]; [MCP handler][mcp-source]
- **Documentation conflict to preserve:** the namespace page says registries are never auto-added, while the directory page says `add` or `search` automatically adds them to `components.json`. Current source is more specific: `search`/`view` discovery is non-persistent (`writeFile:false`); the shared helper can persist directory-discovered mappings for callers permitting writes. Do not describe `search` as a config mutation on the inspected version. [Namespace docs][namespace-docs]; [directory docs](https://ui.shadcn.com/docs/registry/registry-index.md); [discovery helper][registry-discovery]
- **Direct catalog versus item URL:** search/list needs a catalog matching `registry.json`; view/add needs an item payload. A provider homepage is neither. MCP accepted both kinds in the appropriate tools during this research. Search result item-address construction rewrites a catalog URL's `registry` segment; verify the resulting exact item URL before installing unusual custom endpoint shapes. [Registry API][registry-api]; [item-address builder][search-source]
- **GitHub registry addresses are implemented, not roadmap:** `owner/repo` for search/list, `owner/repo/item` for view/add, optional `#branch`, `#tag`, or full SHA. Repository root must contain a valid `registry.json`; arbitrary repositories do not become installable merely because they contain React code. GitHub Enterprise hostnames are not supported by this address form. Dependencies do not inherit the parent's pinned ref. Official docs describe public and credential-backed private GitHub support. [GitHub registries](https://ui.shadcn.com/docs/registry/github.md); [search implementation][search-source]
- **Dynamic search means optional server-side catalog filtering:** requests forward `q`, comma-separated `type`, `limit`, `offset`; a returned `pagination` object opts into server ranking/filtering. Static catalogs continue working with local fuzzy matching. Multi-registry search over-fetches and merges; a server cap can limit reachable later pages. This does not turn MCP into a search engine across every community registry. [Dynamic search docs](https://ui.shadcn.com/docs/registry/dynamic-search.md); [search implementation][search-source]

### Inferences

**Minimal registry strategy**

1. Keep a single official MCP connection. Leave Stack's `registries:{}` alone; `@shadcn` already resolves. Always pass `registries:["@shadcn"]` for official discovery.
2. If the current MCP cannot produce project-base examples, inspect through `pnpm exec shadcn ... -c <app>`; a known style-specific catalog/item URL is also a useful read-only MCP input. Do not assume `<repo root>` is `<app>`.
3. Name a concrete missing capability after inspecting official options, e.g. “large-data grid requires virtualization and column pinning beyond the selected official composition.” Then find one or two relevant community sources from the current official directory or a known repository; inspect their catalog dynamically.
4. Use direct catalog/item URLs or GitHub addresses during exploration, avoiding a growing permanently configured catalog. Add a stable namespace only when a selected source needs recurring use, headers/auth, or an alias. That configuration belongs to implementation, not catalog discovery.
5. Keep provenance at item granularity: namespace or exact item URL/address, repository/ref when relevant, observed date, required base/style, dependencies and targets. Do not pin only the parent GitHub item and claim all transitive dependencies are pinned.

**Exact useful CLI commands** — below use Stack's already-installed, observed **4.21.0** and do not install anything. This deliberately avoided `pnpm dlx` downloading packages during the read-only assignment. For a future authorized invocation that explicitly wants current upstream, the official runner form is `pnpm dlx shadcn@latest <command>`; record/recheck version and help because capabilities can drift. [Local package](file:///Users/arthack/code/stack/packages/ui/package.json); [CLI docs][cli-docs]

```bash
# From /Users/arthack/code/stack/packages/ui:
pnpm exec shadcn --version
pnpm exec shadcn info --json
pnpm exec shadcn search @shadcn -q sidebar -t block -l 5 --json
pnpm exec shadcn search @shadcn -q combobox -t ui -l 5 --json
pnpm exec shadcn view @shadcn/sidebar-08 @shadcn/combobox
pnpm exec shadcn docs button sidebar --json

# From any directory, reliably select the app and installed executable:
pnpm --dir /Users/arthack/code/stack/packages/ui exec shadcn info --json
pnpm --dir /Users/arthack/code/stack/packages/ui exec shadcn search @shadcn -q sidebar -t block -l 5 --json

# Read-only URL/address forms, after identifying a named gap and real source:
pnpm exec shadcn search https://provider.example/r/registry.json -q REQUIRED_CAPABILITY -t block --json
pnpm exec shadcn view https://provider.example/r/selected-item.json
pnpm exec shadcn search owner/repo -q REQUIRED_CAPABILITY --json
pnpm exec shadcn view 'owner/repo/selected-item#FULL_COMMIT_SHA'
```

The final four lines are **syntax examples with placeholders**, not tested providers. Official URL forms were actually exercised through MCP; no community providers were invented or installed.

### Gaps

- MCP source supports explicit built-in lookup without project config, but the local no-config MCP probe only exercised registry-list and command generation; the **CLI** no-config search was directly verified. Do not present the latter as a direct no-config MCP search test.
- Public GitHub registry addressing and dynamic server search were verified from current primary docs/source, not a separate live community registry request. Directory-wide namespace enumeration is not one of the seven exposed tools.
- Direct URLs without namespace mappings do not provide an arbitrary authentication-header argument in the MCP tool schema; private authenticated registries require the appropriate configuration/environment or supported GitHub credential path.

## 3. How should `/design` connect this to local Stack and choose components?

### Takeaway

**Stack already has the required Role skill/MCP machinery and a compatible shadcn application.** A `/design` router can hand off an explicit official registry and application path to the existing shadcn skill, keeping discovery, selection, and installation distinct. No new Stack Package API, registry mirror, or hardcoded community catalog is necessary for the first version.

### Cited Findings

- **Actual Stack UI context, read with `pnpm exec shadcn info --json`:** Next.js App Router **16.3.6**, React dependency **^19.3.0**, TypeScript, RSC true, Tailwind v4, **Base UI** with `style:"base-nova"`, Lucide icons, CSS `packages/ui/app/globals.css`, aliases `@/components/ui`, `@/lib/utils`, `@/hooks`, resolved cwd `/Users/arthack/code/stack/packages/ui`. `components.json` has no custom registries. Root package manager is **pnpm@12.5.1**. [UI package](file:///Users/arthack/code/stack/packages/ui/package.json); [components config](file:///Users/arthack/code/stack/packages/ui/components.json); [root package](file:///Users/arthack/code/stack/package.json)
- **Installed primitives observed by `info`:** alert-dialog, alert, badge, button, command, dialog, dropdown-menu, field, input-group, input, kbd, label, native-select, popover, scroll-area, separator, sonner, spinner, switch, textarea, toggle-group, toggle, tooltip. Sidebar and combobox are not in that observed list; do not assume they are importable because they exist upstream. [Local component directory](file:///Users/arthack/code/stack/packages/ui/components/ui)
- **CLI docs resolution respects this project:** `pnpm exec shadcn docs button sidebar --json` returned `base:"base"` and `/docs/components/base/button`, `/docs/components/base/sidebar`, plus Base example URLs. The fetched official Base button docs use `render` for DropdownMenuTrigger, in contrast to the MCP fallback demo's `asChild`. [Base button docs](https://ui.shadcn.com/docs/components/base/button.md); [general CLI docs][cli-docs]
- Stack Role external MCP records support **stdio** `{type,command,args,env?,envVars?}` and **HTTP** `{type,url,bearerTokenEnvVar?,httpHeaders?,envHttpHeaders?}`. The strict stdio schema has **no cwd field and no project-path interpolation field**. Enabled external MCP records materialize into private launch config; the official shadcn server is stdio. [Role schema](file:///Users/arthack/code/stack/packages/roles/src/resources.ts); [materialization](file:///Users/arthack/code/stack/packages/roles/src/bundle.ts); [official server transport][mcp-cli]
- Roles contain enabled skills including supporting files, MCP definitions, instruction fragments and trusted projects. Native invocation is `stack roles inject [default|role-name] -- <claude|codex|opencode> [native args...]`; it captures a private snapshot and excludes ambient capability config. This is implemented in the local repo, not a proposed router feature. [ADR 0123](file:///Users/arthack/code/stack/docs/adr/0123-role-injection-for-native-clis.md); [injection implementation](file:///Users/arthack/code/stack/packages/roles/src/inject.ts)
- **Worker defaults changed today:** ADR 0124 supersedes ADR 0122's capability-only rule. Manager/Bot and Worker defaults are separate; explicit Worker `roleId` remains supported; Workers now receive selected Role instruction fragments (ACP once on initial task, Claude via system append). Roles are immutable per launched snapshot; changes affect later launches. Do not repeat the superseded claim that Workers never get Role instructions. [ADR 0124](file:///Users/arthack/code/stack/docs/adr/0124-manager-and-worker-launch-defaults.md); [ADR 0122, selection/snapshot contract](file:///Users/arthack/code/stack/docs/adr/0122-worker-role-selection-without-instructions.md)
- Stack exposes read-only `role_launch_preview({roleId,cwds:[absolutePath],context?})`, including enabled skills/MCPs, launch issues, config, and trusted-project matching. The current `cwds` input is **for trust matching**, not an MCP cwd override. Prefer metadata-filtered preview output; full launch/editor snapshots can contain MCP credentials. [Role API](file:///Users/arthack/code/stack/packages/roles/api.ts)
- **Live Stack Role inventory could not be inspected:** a supported socket client read of `roles_snapshot` failed `connect ENOENT /Users/arthack/.local/state/stack/sockets/roles.sock`. Thus source-level support is confirmed, but no claim is made that the running/default Stack Role already contains shadcn. Session AgentStart MCP availability is separate evidence. [Socket client invocation path](file:///Users/arthack/code/stack/packages/roles/cli.ts); [Role schema](file:///Users/arthack/code/stack/packages/roles/src/resources.ts)
- **Repository constraints matter for applying blocks:** Stack's UI is the central Canvas application; guidance says use the existing space architecture, add UI primitives from `packages/ui`, and run UI typecheck for affected UI/API work. It forbids unsolicited new surfaces/dependencies and warns that an in-place production build replaces a live `.next`; use authorized dev/separate-checkout verification. A block's `app/dashboard/page.tsx` target must not silently become a new Stack surface. [Stack AGENTS](file:///Users/arthack/code/stack/AGENTS.md); [sidebar payload](https://ui.shadcn.com/r/styles/base-nova/sidebar-08.json)
- The loaded shadcn skill requires explicit registry selection when adding a component/block and says to ask if unspecified. It also requires checking local installed components, fetching docs, reviewing transformed additions, and preserving user-approved overwrite boundaries. [Installed shadcn skill](file:///Users/arthack/.local/share/agentstart/resources/roles/default/skills/shadcn/SKILL.md)

### Inferences

**Proposed minimal Stack wiring — not executed**

1. Put the `/design` router and necessary implementation skills in the **chosen Role** through Stack's existing role resources when deployment is authorized. Include shadcn for shadcn work; put user-authorized official-first routing in the router's task brief/instructions. Treat this as a Role capability, not a new server lifecycle.
2. One compatible project-bound stdio definition for this particular Stack UI is:

   ```json
   {
     "type": "stdio",
     "command": "pnpm",
     "args": [
       "--dir", "/Users/arthack/code/stack/packages/ui",
       "exec", "shadcn", "mcp"
     ]
   }
   ```

   This uses an already-present dependency, and actual pnpm cwd behavior was checked. The Role resource additionally needs its normal name/description/enabled metadata. Resolve command availability in the launch environment. **Do not substitute `mcp -c <app>` for the process-cwd fix on the observed version.** This definition is specific to this app; it is not a reusable hardcoded path for all projects.
3. A shared multi-project Role may use a deliberately project-independent official-discovery MCP, as the existing AgentStart wrapper does, with **all project inspection/install through CLI `-c` or `pnpm --dir`**. If project-specific private registries must be visible to MCP, use a launch explicitly rooted in that project. Stack currently has no demonstrated dynamic per-call cwd templating; that would be a future capability, not required for v1.
4. Verify selected Role metadata and `role_launch_preview` once the Stack server is available, then start a new intended session. Existing Role snapshots will not hot-reload. A native launch example after configuration is `stack roles inject <chosen-role> -- codex`, run from the task's intended project directory. This is a future launch example, not a command run here.
5. Avoid `shadcn mcp init` as the Stack integration path: it writes harness config and installs dependencies, whereas Stack already owns private Role delivery. Use one official MCP, not one MCP per registry. Component registry namespaces are data supplied to that MCP/CLI.

**Resolving the explicit-registry skill rule**

The human has authorized an **official-first** policy. `/design` can concretely translate that authorization into the delegated brief:

> “Target `/Users/arthack/code/stack/packages/ui`. Discover candidates in **`@shadcn`** first, reusing installed primitives. Search community only for a named gap that official candidates cannot satisfy. Return a shortlist with provenance and compatibility notes. This stage is discovery/selection; execute installation only within the implementation scope of the user request.”

The downstream shadcn invocation is now given a registry; it is not being asked to invent a default. Do not weaken the skill to “always pick shadcn” for unrelated requests. For a chosen community candidate, delegation should likewise name its exact namespace/item or item URL. Discovery authorization does not by itself require installing it.

**Three stages and concrete outputs**

1. **Discovery (read-only):** identify the app/workspace and existing components; make explicit `@shadcn` searches for the behavior and for block/primitive shape; fetch appropriate docs/examples. Output a bounded candidate list and, if necessary, one named official gap plus a tightly scoped community search.
2. **Selection (read-only):** compare 2–3 candidates or an existing-primitives composition. Use full CLI payloads and dependency targets, not MCP metadata alone. Output recommendation, reasons, exact source identifiers, project-base fit, dependencies, file/route changes, and unresolved evidence. A successful search is not a successful selection.
3. **Install/adapt (implementation scope):** inspect a selected item's `add --dry-run`, `--diff`, and/or `--view` as appropriate; then install with the project's runner, review transformed files/imports/icons/semantics, adapt inside Stack's requested surface, and verify behavior. Do not overwrite local edits on the strength of a block demo. Use `pnpm --filter @stack/ui typecheck`; render/interaction checks should target the actual changed controls. No install or dry-run was executed during this research.

Future implementation examples, **not run**:

```bash
# From packages/ui, after a candidate is selected:
pnpm exec shadcn add @shadcn/combobox --dry-run
pnpm exec shadcn add @shadcn/combobox --view combobox.tsx
pnpm exec shadcn add @shadcn/combobox

# Stack UI check from repository root:
pnpm --filter @stack/ui typecheck
```

**Pragmatic shortlist rubric — a decision aid, not an upstream score**

Use `pass / needs adaptation / unknown / fails`, with evidence and one-sentence tradeoff per dimension. Reject incompatible candidates before aesthetic ranking; prefer the smallest adequate change.

| Dimension | What to inspect before selection |
| --- | --- |
| Behavior fit | Exact task and states: empty/loading/error/disabled; interactions; mobile behavior. Does the block solve the requirement or only resemble its screenshot? |
| Accessibility | Semantic controls, labels/names, keyboard paths, visible focus, modal focus/escape behavior, required titles, reduced motion, contrast. Existing Base/Radix primitives help, but verify the final composition. |
| Project compatibility | Base UI vs Radix vs Aria APIs; React/Next/RSC boundaries; Tailwind version/tokens; aliases; icons; CSS ownership; package versions; route/file targets; existing local components and edits. For Stack, Base UI `render` is material. |
| Performance | New direct/transitive packages; client JS and RSC boundaries; chart/editor/animation weight; list size and virtualization; image/font/network costs. Separate measured results from code-based expectations. |
| Maintenance/provenance | Official source first; actual repository/license, recent relevant maintenance and issue response, docs and reproducible item/ref. Registry-directory inclusion or stars alone do not prove maintained code. |
| Adaptation cost | Number of touched files, token fit, composition complexity, collision risk, dependencies already present, and how much of a block would be discarded. |

Compact shortlist record: `candidate`, `registry/item or URL`, `observedAt`, `requiredBase`, `docs`, `fit`, `a11yEvidence`, `performanceEvidence`, `maintenanceEvidence`, `dependencies`, `fileTargets`, `adaptations`, `recommendation`. Keep “unknown” visible instead of fabricating confidence numbers.

### Gaps

- Stack's default and Worker Role resources could not be verified live because the Roles socket was absent at the default state directory. A future setup must inspect the effective Role and launch preview, not infer deployment from source.
- The project-bound MCP definition is schema-compatible and its cwd mechanism was verified; it was **not** registered in Stack or exercised through a Stack-launched agent.
- Per-project automatic MCP rebinding, shadcn service version pinning policy, and hot tool-context changes are design choices for future work; current v1 can use explicit CLI context without implementing them.
- Registry-health-based ranking is explicitly future/experimental upstream. Accessibility, runtime performance, and maintenance judgments remain the selecting agent's evidence-based work.

[mcp-docs]: https://ui.shadcn.com/docs/mcp.md
[cli-docs]: https://ui.shadcn.com/docs/cli.md
[namespace-docs]: https://ui.shadcn.com/docs/registry/namespace.md
[mcp-source]: https://github.com/shadcn-ui/ui/blob/08ab84f7d1952cc1f36055aa8931213a86b01bbd/packages/shadcn/src/mcp/index.ts
[mcp-utils]: https://github.com/shadcn-ui/ui/blob/08ab84f7d1952cc1f36055aa8931213a86b01bbd/packages/shadcn/src/mcp/utils.ts
[mcp-cli]: https://github.com/shadcn-ui/ui/blob/08ab84f7d1952cc1f36055aa8931213a86b01bbd/packages/shadcn/src/commands/mcp.ts
[search-source]: https://github.com/shadcn-ui/ui/blob/08ab84f7d1952cc1f36055aa8931213a86b01bbd/packages/shadcn/src/registry/search.ts
[search-cli]: https://github.com/shadcn-ui/ui/blob/08ab84f7d1952cc1f36055aa8931213a86b01bbd/packages/shadcn/src/commands/search.ts
[view-cli]: https://github.com/shadcn-ui/ui/blob/08ab84f7d1952cc1f36055aa8931213a86b01bbd/packages/shadcn/src/commands/view.ts
[registry-api]: https://github.com/shadcn-ui/ui/blob/08ab84f7d1952cc1f36055aa8931213a86b01bbd/packages/shadcn/src/registry/api.ts
[registry-config]: https://github.com/shadcn-ui/ui/blob/08ab84f7d1952cc1f36055aa8931213a86b01bbd/packages/shadcn/src/registry/config.ts
[registry-discovery]: https://github.com/shadcn-ui/ui/blob/08ab84f7d1952cc1f36055aa8931213a86b01bbd/packages/shadcn/src/utils/registries.ts
