# Shoogle and WebMCP for the /design skill family

Research date: **2026-09-29**. Labels below distinguish **vendor/spec documentation**, **observed behavior**, and **inference/recommendation**. This was read-only research: no authentication, installation, skill deployment, or changes to other repositories.

## 1. Which Shoogle, what does it search, and what agent contracts exist?

### Takeaway

The relevant product is **Shoogle at https://shoogle.dev/**. Its **own hosted MCP is real and returned useful results in live unauthenticated calls**; this is a viable optional keyword-discovery adapter. Its name-based MCP/CLI search and its website's advertised semantic/layout discovery must be treated as distinct capabilities.

### Cited Findings

#### Identity and coverage

- **Observed:** The homepage calls itself “Your shadcn UI components & blocks search engine.” It links to `/search`, `/directory`, and its own `/mcp` documentation. The docs show an **Alpha** label. Use **Shoogle** / `shoogle.dev`, not an inferred alternate spelling or a similarly named search product. [Homepage](https://shoogle.dev/); [MCP overview](https://shoogle.dev/mcp)
- **Local context checked before live search:** Agentbrain `context("Shoogle shoogle shadcn WebMCP")` found document **23**, chunk **303**, title “Search for shadcn blocks online.”, source `https://shoogle.dev/`. The stored excerpt was only “Search shadcn blocks on the web,” so it established identity but supplied no current integration contract. Relation provenance: legacy-recovery collection, frozen recovery generation source; no linked relations. [Saved source, checked live](https://shoogle.dev/)
- **Vendor statement + observed page:** The directory says its community registries are “pulled from the shadcn/ui directory” and links to shadcn's registry-index contribution instructions. It displayed **402 registries**, with categories and pagination. This is a directory count at observation time, **not a verified count of fully indexed/searchable registries or all components**. [Shoogle directory](https://shoogle.dev/directory); [upstream registry index](https://ui.shadcn.com/docs/registry/registry-index)
- **Vendor statement:** Shoogle stores shadcn registry items to make them searchable and installable directly from the registry server. The MCP overview's animated counters extracted as `0` plus digit sequences; those are unusable evidence for a component count. [MCP overview](https://shoogle.dev/mcp)
- **Observed provenance returned by search:** Items include an original registry namespace, registry homepage, item name/type, optional description, and namespaced install argument. Example: `@cult-ui/feature-carousel`, homepage `https://www.cult-ui.com/` with Shoogle UTM parameters, `registry:ui`, and a carousel description. Results are discovery pointers, not a source-code/license attestation. [Live MCP endpoint](https://mcp.shoogle.dev/mcp); [documented result description](https://shoogle.dev/mcp/shoogle-skills)

#### Official Shoogle MCP: public contract and live verification

- **Vendor documentation:** `https://mcp.shoogle.dev/mcp` is the published **Streamable HTTP, no-auth** endpoint. This is an official **Shoogle** integration, not evidence that shadcn maintains or endorses Shoogle. It is separate from the official shadcn MCP. [Shoogle connection docs](https://shoogle.dev/mcp/other-mcp-clients); [official shadcn MCP](https://ui.shadcn.com/docs/mcp)
- **Observed:** An unauthenticated JSON-RPC `initialize` POST returned HTTP 200, server name `shoogle-mcp-server`, version `1.0.0`, tools capability, and protocol version `2024-11-05` (the request offered `2025-03-26`). No `mcp-session-id` header was returned. A following `tools/list` POST succeeded. This demonstrates an operational service, though not every client's transport/version compatibility. [Live endpoint](https://mcp.shoogle.dev/mcp)
- **Observed:** `tools/list` returned **exactly two tools**, despite the setup page's wording “and the rest.” Both are discovery tools; neither installs source. The `inputSchema` defines numbers for offsets/limits but does not encode all bounds stated in descriptions. [Live endpoint](https://mcp.shoogle.dev/mcp); [setup wording](https://shoogle.dev/mcp/other-mcp-clients)

| Tool | Actual advertised inputs | Advertised behavior |
| --- | --- | --- |
| `search_registry_items` | required `query: string`; optional `offset: number`, `limit: number` | Search item **names** across indexed registries; default offset 0, default/max limit 100 |
| `search_registry_items_scoped` | required `query: string`, `registries: string[]` with at least one element; optional offset/limit | Same name search restricted to namespaces; reports `unknownRegistries` |

Source for both rows: the live `tools/list` response from [Shoogle MCP](https://mcp.shoogle.dev/mcp), corroborated by [Shoogle skill docs](https://shoogle.dev/mcp/shoogle-skills).

- **Vendor description, not independent backend inspection:** The live tool description explicitly says “using the **Convex full-text index on item names**.” This supports keyword/name search, not an assertion of semantic embedding search, visual similarity, or arbitrary natural-language retrieval through MCP. [Live tool catalog](https://mcp.shoogle.dev/mcp)
- **Observed successful global search:** `search_registry_items({"query":"carousel","offset":0,"limit":3})` returned three items: `@shadcncraft/use-carousel`, `@cult-ui/feature-carousel`, and `@cult-ui/loading-carousel`. Pagination reported `total: 100`, `hasMore: true`, `limit: 3`, `offset: 0`; a separate `totalResults` also reported 100. The payload timestamp was `2026-09-29T22:49:23.770Z`. Treat 100 as the server-reported query total, not a proven exhaustive census. [Live endpoint](https://mcp.shoogle.dev/mcp)
- **Observed successful scoped search:** `search_registry_items_scoped({"query":"carousel","registries":["@cult-ui"],"offset":0,"limit":2})` returned the two Cult UI carousels, reported total 8 and `hasMore: true`, with `unknownRegistries: []`. Timestamp: `2026-09-29T22:49:37.235Z`. [Live endpoint](https://mcp.shoogle.dev/mcp)
- **Observed documentation/behavior caveat:** The tool description gives bare namespace examples `shadcn` and `magicui`, but a call using exactly those strings returned zero items and `unknownRegistries: ["shadcn","magicui"]`. The successful `@cult-ui` call used a namespace copied from an actual result. This does **not** prove whether `@shadcn` or `@magicui` is covered, nor prove prefixing alone explains the difference. Prefer exact returned/configured namespace strings. [Live endpoint](https://mcp.shoogle.dev/mcp)
- **Observed operational caveat:** Two simultaneous search calls caused one to return HTTP 200 with JSON-RPC error `-32603`, message `Internal error`, data `Rate limit exceeded. Try again in 3s.` The other completed. A later sequential retry of the rate-limited read succeeded. HTTP success is therefore insufficient: inspect the JSON-RPC error and MCP result content. Rate limits exist, but their full policy was not established. [Live endpoint](https://mcp.shoogle.dev/mcp)
- **Observed response shape:** Tool data arrived as JSON serialized inside `result.content[0].text`, not a typed `structuredContent` object. Fields observed were `query`, `pagination`, `items`, `totalResults`, `timestamp`, plus `registries` and `unknownRegistries` for scoped calls. Each item had `name`, `type`, `registry`, `homepage`, `addCommandArgument`, and sometimes `description`. [Live endpoint](https://mcp.shoogle.dev/mcp)

Minimal request used for the successful read, to the **documented** endpoint above:

```json
{
  "jsonrpc": "2.0",
  "id": 5,
  "method": "tools/call",
  "params": {
    "name": "search_registry_items",
    "arguments": { "query": "carousel", "offset": 0, "limit": 3 }
  }
}
```

Headers used: `Content-Type: application/json` and `Accept: application/json, text/event-stream`. A normal MCP host should negotiate and manage the protocol rather than copying this research probe into a production HTTP wrapper. [Shoogle transport docs](https://shoogle.dev/mcp/other-mcp-clients); [observed endpoint](https://mcp.shoogle.dev/mcp)

#### CLI, search URLs, website, and skills

- **Vendor-documented CLI:** `npx shadcn@latest search @shoogle -q carousel`. Published query parameters are **required `q`**, optional comma-separated `type`, `limit`, and `offset`. Shoogle specifically says omitting `q` returns no results. This command was **not executed**, because installing/running a fetched CLI was outside this research's constraints. [Shoogle CLI docs](https://shoogle.dev/mcp/cli)
- **Official shadcn contract:** Dynamic search forwards `q`, `type`, `limit`, `offset` to the configured registry catalog URL. A `pagination` object marks a server-filtered response; otherwise the CLI filters a static catalog locally. Search results need not contain source files or dependencies. Notably shadcn's generic specification says no query should return paginated items, whereas Shoogle documents no-query/no-results. [Dynamic search documentation](https://ui.shadcn.com/docs/registry/dynamic-search)
- **Observed website routes:** The homepage links to `/search`, `/search?tab=explore`, and `/search?tab=bookmarks`. The search page has Search/Fresh/Explore/Registries/Bookmarks navigation and a preview area. Its HTML contains a text combobox with placeholder “Search shadcn blocks (e.g. chart, carousel)” and a form marked `data-search-form="true"`. [Homepage](https://shoogle.dev/); [search page](https://shoogle.dev/search)
- **Observed implementation detail, not stable public API:** The search page's linked main bundle validates URL state including `tab`, `q`, `preview`, `kw`, `score`, and `freshMode`. This supports that `q` exists as website URL state, but the precise submit/navigation/result behavior was not exercised. Do not promote bundle internals into a supported REST or semantic-search contract. [Observed linked bundle](https://shoogle.dev/assets/index-DwI_RgwO.js)
- **Vendor distinction:** Shoogle's skill docs describe MCP tools as name/keyword search, then explicitly say “For semantic or layout-based block discovery, use shoogle.dev/search instead.” The site advertises richer browser discovery than the MCP. No ranking/semantic quality evaluation was performed. [Shoogle skill docs](https://shoogle.dev/mcp/shoogle-skills)
- **Vendor skill exists:** Shoogle publishes instructions for a skill that teaches assistants to use its MCP and `shadcn add`. The skill depends on the MCP being configured. No skill was downloaded or installed. [Skill documentation](https://shoogle.dev/mcp/shoogle-skills)

### Inferences

- Use Shoogle as **cross-registry discovery**, preserving the original namespace and item identifier. Inspect the source registry before selection; a directory listing and install argument do not establish compatibility, license, maintenance, or quality. The evidence for this separation is the returned metadata-only result shape. [MCP results](https://mcp.shoogle.dev/mcp); [shadcn search schema](https://ui.shadcn.com/docs/registry/dynamic-search)
- A generic shadcn registry-search adapter may eventually cover `@shoogle` without a new MCP connection. The hosted Shoogle MCP is more thoroughly verified in this run; the CLI route needs a bounded compatibility spike in an already provisioned environment. [Shoogle CLI docs](https://shoogle.dev/mcp/cli)

### Gaps

- Exact indexed item count, proportion of the 402 directory registries actually searchable, crawl cadence, deleted-item handling, ranking/deduplication, license coverage, freshness guarantees, and SLA are unknown. No source-inspection or corpus audit was done.
- No separately documented Shoogle REST API, canonical raw registry catalog URL, or stable semantic-search API was established. **Do not invent `/api/search` or a registry URL.** Resolve any future CLI catalog URL from the actual configured/published namespace mapping.
- No independent third-party Shoogle MCP was needed or validated. The product's own documentation and live endpoint resolve the central “does a real MCP exist?” question. Alternate product spellings were not established as aliases.
- Browser search submission, result-card accessibility, preview fidelity, authentication requirements for bookmarks, and screenshot-based selection remain unverified because both available browser routes were unavailable; details follow below.

## 2. Does Shoogle expose WebMCP, and what do browsers/tools support now?

### Takeaway

**Shoogle WebMCP support is unverified.** Its operational HTTP MCP is not WebMCP. WebMCP is a genuine, evolving browser API with current Chrome/Edge experiments and explicit `agent_browser` tooling; it should be an opportunistic, capability-detected path, not a dependency for v1 component discovery.

### Cited Findings

#### What WebMCP is and current status

- **Specification:** WebMCP lets a page register structured tools backed by JavaScript or annotated HTML forms; the browser mediates discovery and invocation in the page context. It complements backend MCP rather than replacing it. DOM clicking, accessibility snapshots, browser automation exposed through an MCP server, and an HTTP MCP endpoint are not themselves proof of WebMCP. [WebMCP explainer](https://github.com/webmachinelearning/webmcp); [Chrome overview](https://developer.chrome.com/docs/ai/webmcp)
- **Fresh primary-source API detail:** Chrome's imperative API docs, updated **September 21, 2026**, use **`document.modelContext`**, including `registerTool`, `getTools`, `executeTool`, and the `toolchange` event. The live spec agrees. A detection plan based only on older `navigator.modelContext` examples would be stale. [Chrome imperative API](https://developer.chrome.com/docs/ai/webmcp/imperative-api); [current explainer](https://github.com/webmachinelearning/webmcp)
- **Chrome documentation:** WebMCP entered an origin trial in **Chrome 149**; local development can enable `chrome://flags/#enable-webmcp-testing`. The overview still calls it proposed/experimental and says visiting a site is necessary to discover its tools. This research did not enable flags or enroll any origin. [Origin-trial announcement, June 9](https://developer.chrome.com/blog/ai-webmcp-origin-trial); [current overview](https://developer.chrome.com/docs/ai/webmcp)
- **Project-maintained implementation status:** The current table says Chrome 149 and **Edge 150** have origin trials, Brave Leo has experimental support, and ChatGPT Desktop supports WebMCP. Firefox and Safari entries link standards-position/implementation discussions rather than asserting shipped support. Meta Ray-Ban support is listed as coming soon. These are **maintainer-reported statuses**, not browsers demonstrated in this run; do not extrapolate ChatGPT Desktop support to this session's built-in browser. [Implementation status](https://github.com/webmachinelearning/webmcp/blob/main/implementation-status.md)
- **Scope/permissions:** Chrome documents origin isolation and the `tools` Permissions Policy. Same-origin tools are returned by default; cross-origin discovery additionally needs explicit `fromOrigins` and the provider's `exposedTo`, with cross-origin frame registration gated by `allow="tools"`. Tool absence can therefore reflect browser version/flags, frame or permission scope, or page state, not just lack of site implementation. [Chrome overview](https://developer.chrome.com/docs/ai/webmcp); [imperative API](https://developer.chrome.com/docs/ai/webmcp/imperative-api)

#### Available host capabilities and how to detect real tools

- **Live primary documentation + installed tool-schema inspection:** Agent-browser documents WebMCP enabled by default for its managed Chrome, proactive `data.webmcp` discovery summaries, and `webmcp list/invoke/result/cancel`. The current harness exposes `agent_browser_webmcp_list` with `session`, optional `tool`, and optional `frameId`; the open tool exposes `webmcp`. This confirms an adapter surface exists, not that this run successfully reached a browser. [Agent-browser README, WebMCP section](https://github.com/vercel-labs/agent-browser#webmcp-experimental)
- **Documented agent-browser detection sequence:** After navigating to the intended site/session, inspect any `data.webmcp` update. Use `agent-browser webmcp list --json` to recover the actual catalog, or fetch a selected tool with `webmcp list <tool> --frame <frame-id> --json` before invocation. Summary omission means **no update**, not “zero tools”; `ready` with `tools: []` clears an old catalog, and `unavailable` invalidates it. Refresh schemas after catalog changes. [Agent-browser README](https://github.com/vercel-labs/agent-browser#webmcp-experimental)
- **Documented in-page detection route:** In a browser with the current API, feature-detect `document.modelContext?.getTools`, then await `document.modelContext.getTools()` and return serializable fields such as names, origins, schemas, and annotations. Do not serialize `window`, invoke tools as a probe, or register injected tools to make a negative result look positive. Merely finding `modelContext` confirms a platform surface, **not a page's registered search tool**. [Chrome imperative API](https://developer.chrome.com/docs/ai/webmcp/imperative-api)
- **Local tool inventory observation:** The built-in `browser` catalog has page evaluation and frames tools, but no dedicated tool named for WebMCP was found. A connected, supporting browser could potentially enumerate via read-only evaluation; its actual API version and access were not established. This inventory result is narrower than a claim that the built-in browser does or does not support WebMCP. [Relevant browser API being probed](https://developer.chrome.com/docs/ai/webmcp/imperative-api)

Suggested **read-only detection snippet**, not executed here:

```js
const context = document.modelContext;
if (typeof context?.getTools !== "function") {
  return { status: "unavailable" };
}
const tools = await context.getTools();
return {
  status: "ready",
  tools: tools.map(({ name, description, origin, inputSchema, annotations }) => ({
    name, description, origin, inputSchema, annotations
  }))
};
```

This matches the September 21 Chrome documentation. On a different implementation, use its documented inspector/catalog surface rather than guessing obsolete testing APIs. [Source](https://developer.chrome.com/docs/ai/webmcp/imperative-api)

#### Shoogle-specific evidence and browser blockers

- **Observed bounded static check:** The fetched `/search` HTML contained no `webmcp`, `modelContext`, `toolname`, or `tooldescription` strings; its form lacked WebMCP declarative annotations. The single main JavaScript bundle linked by that page, 606,872 characters, likewise had no matches for those markers. This is **limited negative static evidence only**: lazy-loaded modules, frames, runtime conditions, and different page states were not examined. [Search HTML](https://shoogle.dev/search); [observed main bundle](https://shoogle.dev/assets/index-DwI_RgwO.js)
- **Session observation:** `agent_browser_open` for `https://shoogle.dev/` in isolated session `shoogle-research` failed with `Plugin 'stack' returned success=false`. Agentscrape's browser extraction failed with the same upstream error. `agentscrape doctor` reported dependencies available, so availability checks did not resolve the launch problem. This is a local tool-path failure, **not a Shoogle rejection or negative WebMCP catalog**. [Target](https://shoogle.dev/); [expected agent-browser behavior](https://github.com/vercel-labs/agent-browser#webmcp-experimental)
- **Session observation:** The fallback built-in browser open of `https://shoogle.dev/search` failed with `[browser.disconnected] No desktop browser is connected to this session`. No browser retries, sign-in, browser installs, or configuration changes followed. Therefore there was no live DOM, tool-catalog, or UI-submission demonstration. [Target](https://shoogle.dev/search)

### Inferences

- Classify Shoogle as **HTTP MCP: verified; WebMCP: unknown**. A future browser check should navigate the actual search page, wait for meaningful page readiness, enumerate registered tools in the correct frame, and inspect any candidate's full schema. A successful generic browser search still would not establish WebMCP. [Protocol distinction](https://github.com/webmachinelearning/webmcp); [discovery API](https://developer.chrome.com/docs/ai/webmcp/imperative-api)
- For component discovery, WebMCP solves the specific gap where a useful site's stateful search/preview functionality is exposed only through its page tools. It does not improve the already verified Shoogle name-search MCP merely by adding another layer. [WebMCP motivation](https://github.com/webmachinelearning/webmcp); [Shoogle tools](https://shoogle.dev/mcp/shoogle-skills)

### Gaps

- Actual Shoogle runtime registration: unknown. There was neither a positive catalog nor a successfully observed empty catalog in a supporting browser.
- Built-in browser support/version/flags and agent-browser's operational status in this host: unknown beyond the catalog and failures above. No repairs were attempted.
- Cross-browser interoperability and specific client versions were not exercised. Current documentation includes evolving and future-version details, so feature detection should govern behavior rather than browser-brand assumptions.

## 3. Bounded operational route, v1 adapter, spikes, fallback, and research accounting

### Takeaway

Use **official shadcn first → configured/vetted registries → Shoogle or targeted discovery → source inspection → component selection**. Ship the read-only discovery policy around existing official shadcn tooling; an optional Shoogle HTTP MCP adapter is evidenced and narrow enough for v1. Keep browser semantic search and WebMCP behind explicit, bounded capability spikes.

### Cited Findings

- **Official baseline:** The shadcn MCP browses/searches compatible registries configured in the project's `components.json`; the standard shadcn registry requires no extra configuration. It also supports installation, so discovery policy must select the appropriate read operations. [Official MCP](https://ui.shadcn.com/docs/mcp)
- **Existing adapter format:** Official registry search works with static catalogs or documented dynamic search/pagination. Source files and dependencies are not required in search results, which is why a later item/source inspection remains necessary. [Dynamic search](https://ui.shadcn.com/docs/registry/dynamic-search)
- **Specific discovery gap solved by Shoogle:** Its hosted MCP searches indexed community item names beyond the project's configured list and returns original registry/item references. It does not return code, dependency analysis, or visual previews in the observed results. [Shoogle tool docs](https://shoogle.dev/mcp/shoogle-skills); [live endpoint](https://mcp.shoogle.dev/mcp)

### Inferences

#### Recommended bounded runtime policy

1. **Establish project context and reuse opportunities.** Identify the project's actual component base, styling setup, existing components, aliases, and configured registry identities. Search the **official shadcn** source for the required primitives or block shape first. This ordering is a discovery recommendation, not implicit permission to install from an unspecified registry. [Official MCP/configuration](https://ui.shadcn.com/docs/mcp)
2. **Search configured/vetted registries.** Prefer already-approved namespaces appropriate to the requested surface. Use existing shadcn search/view facilities rather than introducing one provider-specific adapter per registry. [Registry compatibility](https://ui.shadcn.com/docs/mcp); [search behavior](https://ui.shadcn.com/docs/registry/dynamic-search)
3. **Escalate once for missing coverage.** Use Shoogle keyword/name search, initially `limit: 10`, `offset: 0`; allow at most one refinement or additional page. Serialize Shoogle calls. If its server asks for a delay, allow one bounded delayed retry of the read, then return a degraded result/fallback. These numeric budgets are **recommended policy**, not vendor limits. Preserve an `unknownRegistries` distinction from a successful no-match result. [Observed tool/rate behavior](https://mcp.shoogle.dev/mcp)
4. **Inspect at most three candidates at their source.** Retain discovery service, registry namespace, item name, source/docs/demo URL, retrieval time, primitive/framework compatibility, dependencies, license, and any unavailable metadata. Inspect actual item/source and a preview when visual fit matters; avoid equating a search hit with source review. [Metadata-only search contract](https://ui.shadcn.com/docs/registry/dynamic-search)
5. **Select with provenance.** Return the best supported candidate or composition and a brief fit rationale. Installation belongs to the separately authorized implementation step using the exact reviewed registry/item. Never execute a returned shell command merely because it was supplied in tool output. [Returned install-argument contract](https://shoogle.dev/mcp/shoogle-skills)

#### Adapter readiness

| Adapter | Recommendation | Evidence / remaining check |
| --- | --- | --- |
| Existing official shadcn MCP/CLI read operations | **v1 foundation** | Official supported registry contract; use provisioned tooling. [Docs](https://ui.shadcn.com/docs/mcp) |
| Shoogle hosted HTTP MCP | **Viable optional v1 discovery adapter** | Initialize, tool listing, global search, and scoped search demonstrated; use normal MCP host, small limits, serialized calls, error/result parsing, original provenance. [Endpoint](https://mcp.shoogle.dev/mcp) |
| `shadcn search @shoogle` through existing registry adapter | **Small compatibility spike** | Official Shoogle docs exist; verify namespace resolution, installed CLI version, query requirement, pagination, original item identity, and read-only behavior without installing another tool. [Docs](https://shoogle.dev/mcp/cli) |
| Shoogle website semantic/layout search | **Browser-usability spike** | Vendor advertises it, but no interactive search/preview demonstrated. Verify one query, one returned source, and bounded extraction; record observed URL state rather than reverse-engineering a production endpoint. [Docs](https://shoogle.dev/mcp/shoogle-skills) |
| Generic WebMCP page-tool discovery | **Optional future capability path** | Agent-browser surface exists and current API is documented; need an operational host, real site tools, and useful schemas. Shoogle support remains unknown. [Agent-browser](https://github.com/vercel-labs/agent-browser#webmcp-experimental); [Chrome API](https://developer.chrome.com/docs/ai/webmcp/imperative-api) |

- **Future fallback chain:** If a known useful page offers a real read-only WebMCP search tool, inspect and use it. If no relevant tool exists or support is unavailable, use ordinary browser search/preview when connected; otherwise targeted source discovery and readable registry docs. All paths converge on the same provenance-aware candidate/source inspection. This is a fallback policy, not a proposal to inject synthetic WebMCP tools or build speculative integrations. [WebMCP's explicit automation fallback](https://github.com/webmachinelearning/webmcp#existing-web-actuation-techniques)
- **Only gap-solving alternatives:** The official shadcn registry directory helps identify providers outside Shoogle's verified coverage; targeted web search helps locate a specific missing capability; a browser helps assess visual/layout fit. An additional third-party Shoogle MCP wrapper offers no demonstrated advantage over its own endpoint. [Shoogle upstream directory provenance](https://shoogle.dev/directory); [official registry directory](https://ui.shadcn.com/docs/registry/registry-index)

### Gaps

#### Research accounting and method limitations

- Three paid `agentsearch.find` calls were issued: `"Shoogle" shadcn MCP API`, `WebMCP Chrome status navigator modelContext`, and `WebMCP Chrome early preview 2026`, five hits each. The first two completed according to the ledger, but their tool results were lost from the combined call when an independent scrape failed; no claims rely on those unseen hits. The third returned usable primary-source links.
- **All three have `cost_usd: null`, `cost_status: "unavailable"`. Total paid cost is unknown, not zero.** This is an accounting limitation. Each reservation was $0.005, but reservations are not measured charges and must not be reported as cost. Evidence: [local cost ledger](file:///Users/arthack/.local/state/agentsearch/search/ledger.jsonl), entries at `2026-09-29T22:11:42.779Z`, `22:11:42.786Z`, and `22:19:33.086Z`; response IDs `da71259e-8ae3-4b62-bdfa-ebe1b7f4244e`, `3a30bc08-59d3-49db-a316-df3d81a682e1`, `3a27fcc4-d76d-498a-8dbf-0063a226a585`.
- Known primary URLs were retrieved directly after Agentscrape's browser path failed. MCP verification used read-only initialization/discovery/search requests to the exact endpoint published by Shoogle. No undocumented endpoint was guessed. Static HTML/bundle inspection was limited to the search page and its linked main bundle; this cannot settle runtime WebMCP support.
- This research supports selecting an adapter and defining a small follow-up spike. It does not establish production reliability, full corpus coverage, semantic quality, or completed installation/integration.
