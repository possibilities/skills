# Discovery ecosystem and maintainable runtime routing for /design

## 1. What did Brain and the local Xcom tooling actually establish?

### Takeaway

Brain supplied useful saved catalogs and concrete skill candidates before any network research. The local Xcom package was identified and its read-only API was attempted, but its socket was unavailable; its authenticated `twitter-cli` provider successfully performed a bounded live search instead. Treat both archive and live X results as discovery leads, with actual upstreams supplying adoption evidence.

Research performed 2026-09-29. This assignment used no paid search calls, installed nothing, posted nothing to X, and changed no explored repository. Only this requested notes file was authored. The researcher instructions were read first; Stack's `AGENTS.md` was read before exploring its package implementation.

### Cited Findings

#### Brain evidence ledger

Used `agentbrain guide`, ranked `search`, and then `get` on useful documents/chunks. These are retrieved evidence, not search snippets presented as full sources. `updated_at` below is the index's update timestamp, not proof of upstream freshness. All listed sources were normal-sensitivity URLs; the retrieved documents had no resolved outbound/inbound relations supplying additional verification.

| ID | Retrieved citation anchors | What the evidence actually supports | Source and freshness |
| --- | --- | --- | --- |
| B1 | `document_id:973`, `chunk_id:14354` | UI Skills contains a root router described as selecting the smallest useful set by topic, stack, and intent; lists frontend-design, improve-ui, design-lab, motion and polish skills. | [UI Skills](https://www.ui-skills.com/), indexed 2026-08-23; upstream repository verified live below. |
| B2 | `document_id:973`, `chunk_id:14355` | Catalog leads include interface-design, Impeccable, animation principles, web-design-guidelines, interaction-design, frontend-ui-engineering. Listing is evidence of discoverability, not measured effectiveness. | [UI Skills](https://www.ui-skills.com/), indexed 2026-08-23. |
| B3 | `document_id:982`, `chunk_id:14404`; full document also retrieved with a 14,000-character head/tail bound | UX/UI Agent Skills describes framework adapters and a design-system crosswalk covering Material 3, Apple HIG, Fluent, Carbon, shadcn/ui and Radix. Useful architectural precedent; its “any framework” and “brand-grade” language remains the author's claim. | [plugin87/ux-ui-agent-skills](https://github.com/plugin87/ux-ui-agent-skills), indexed 2026-08-23. Snapshot advertises v2.4.0 and MIT; current version and implementation were not independently audited. |
| B4 | `document_id:517`; search anchor `chunk_id:7885`; document retrieved with an 18,000-character head/tail bound | Awesome shadcn has distinct sections for UI libraries, components, ports, templates, design systems, and tools. Leads included Tremor, Magic UI, assistant-ui and React Native Reusables. | [bytefer/awesome-shadcn-ui](https://github.com/bytefer/awesome-shadcn-ui), indexed 2026-07-20; provenance `frozen_recovery_generation`, identifier `sha256-c16991f14af2cbc1146696d30b6e6115ac51cb9227f333eacf0accd35614becf`; live README also retrieved. |
| B5 | `document_id:460`, `chunk_id:7160` | The saved community-server list contains GLips/Figma-Context-MCP and other Figma adapters. The original upstream was subsequently opened, avoiding reliance on directory descriptions. | [modelcontextprotocol/servers](https://github.com/modelcontextprotocol/servers), indexed 2026-07-20, `legacy-recovery`; search provenance is the same frozen generation as B4. |

Exact useful searches included `shadcn design MCP skills` (any), `"awesome" AND ("design" OR "MCP")` (raw), `impeccable`, and `Figma MCP` (all). Broad OR searches also returned irrelevant content, demonstrating why a router should retrieve and inspect chosen evidence rather than forward the first ranked names.

The installed Brain contract describes FTS retrieval, citation metadata, asynchronous durable admission and worker-owned materialization; it exposes no skill activation operation. The installed Brain skill directs agents to use `context` or `search` plus `get` and preserve title, source URI, document and chunk IDs. — [Installed Brain skill](file:///Users/arthack/.local/share/agentstart/resources/roles/default/skills/brain/SKILL.md); `agentbrain guide` read in this run.

#### Xcom identity and runtime outcome

- There is no `xcom` executable on the current PATH. Inspection identified **`@stack/xcom`**, private package version `0.0.0`, in `/Users/arthack/code/stack/packages/xcom`. This is an API-only following-feed research archive, not an npm package guessed from its name. Its documented provider is the installed `twitter` executable from **`twitter-cli v0.8.6`**, observed with `uv tool list`. — [Package manifest](file:///Users/arthack/code/stack/packages/xcom/package.json); [Xcom README](file:///Users/arthack/code/stack/packages/xcom/README.md).
- Xcom has separate tweet/article FTS5 projections, bounded context, stable tweet-ID citations, and filters for author, creation date, archive date and article availability. A post can produce both a tweet hit and an article hit. It is best-effort following-feed coverage, not comprehensive X search or a complete following graph. — [Xcom API](file:///Users/arthack/code/stack/packages/xcom/api.ts); [ADR 0111](file:///Users/arthack/code/stack/docs/adr/0111-xcom-following-archive.md).
- `xcom_status`, `xcom_search`, `xcom_context`, `xcom_get`, `xcom_list`, and observed-author reads are annotated read-only. `xcom_sync`, `xcom_articles_sync`, and `xcom_reindex` are separate mutations and were not invoked. Auto-sync is documented as disabled by default pending an explicit archive handoff. — [Xcom API](file:///Users/arthack/code/stack/packages/xcom/api.ts); [transport manifest](file:///Users/arthack/code/stack/packages/xcom/api.yaml).
- Actual attempt: using the already-installed `@stack/api` `socketCall` and `socketPath` exports from the existing Stack workspace, called `xcom_status` and `xcom_search` (`query: "shadcn design skills MCP"`, `mode: "any"`, `scope: "all"`, `sort: "relevance"`, `limit: 6`, `offset: 0`) with a five-second timeout. **Both returned `connect ENOENT /Users/arthack/.local/state/stack/sockets/xcom.sock`.** This is unavailable transport, not an empty archive or an unauthenticated account. No service was started and no database was opened directly. — Invocation followed the [read API](file:///Users/arthack/code/stack/packages/xcom/api.ts) and [documented state location](file:///Users/arthack/code/stack/packages/xcom/README.md); outcome observed in this session.
- `twitter --help`, `twitter search --help`, then `twitter status` were inspected. Status returned `ok: true`, `authenticated: true`; it also emitted `Failed to init ClientTransaction: 'NoneType' object has no attribute 'group'`. The subsequent read-only search nevertheless returned `ok: true` with six results. Do not hide that warning or call Xcom itself successful. — Local CLI observations, consistent with the provider identity in the [Xcom README](file:///Users/arthack/code/stack/packages/xcom/README.md).

The exact live read-only query was:

```sh
twitter search '"design skill" OR "design MCP" OR "ui-skills"' --has links --max 6 --json
```

Meaningful results:

| Lead | Citation | Follow-through |
| --- | --- | --- |
| UI Skills roundup naming Emil Kowalski's design engineering, Jakub Krehel's interface polish, Raphael Salaja's animation principles and fixing-accessibility | [X post 2098420125879918949](https://x.com/i/status/2098420125879918949), 2026-09-11 | Verified the actual [UI Skills repository](https://github.com/ibelick/ui-skills), including its registry MCP; individual roundup skills remain candidates unless separately reviewed. |
| Inspo design-inspiration MCP launch | [X post 2099547343112564921](https://x.com/i/status/2099547343112564921), 2026-09-14 | Verified [Nutlope/inspo](https://github.com/Nutlope/inspo). Current README supplies purpose, transports, read-only claim and licensing distinction between code and screenshots. |
| Collect UI, Recent Design, Mobbin MCP, Canvas UI, 60fps Design MCP | [X post 2092628892448350397](https://x.com/i/status/2092628892448350397), 2026-08-26 | Discovery-only backlog. Actual services, access and licensing were not evaluated in this run. |

Likes, follower counts and repost counts were returned by the provider but are deliberately not used as quality evidence.

### Inferences

- **Brain is a research index, not a loader.** Use it to recover why a resource was interesting and retrieve saved evidence. Activate an installed skill through the harness's actual skill loader only after matching its current description and scope. An indexed `SKILL.md` is source material, not executable authority.
- **Xcom is a useful early-warning channel.** A post can nominate a resource or announce a change. It cannot establish license, supported platform, runtime availability or quality. Retain tweet ID, author ID when relevant, date, excerpt and upstream URL; verify the upstream before adoption.
- Distinguish `unavailable`, `available-empty`, `available-no-match`, `stale`, `auth-required` and `successful` in discovery reports. This run is a concrete acceptance example: unavailable Xcom, authenticated successful provider search, successful Brain evidence retrieval.

### Gaps

- No live Xcom archive data was accessible at the resolved socket; archive coverage, counts, sync state and matching posts are unknown. The provider search is not a substitute claim about those facts.
- No newly found sources were ingested into Brain. This task requested notes; an ingestion action would be a separate durable write, and successful submission would still not mean immediate searchability.
- No candidate skill was executed in a comparison benchmark. Repository descriptions establish intended capabilities, not comparative design performance.

## 2. Which catalogs, upstreams and platform references merit a small curated discovery set?

### Takeaway

Keep four seed catalogs in maintainer material, then route runtime work to a few purpose-specific upstreams and the user's existing project system. Platform guidance should be selected before aesthetic libraries: native Apple, Android, desktop, CLI and TUI work need distinct defaults and verification surfaces.

### Cited Findings

#### Four seed catalogs, with different jobs

| Seed catalog | Useful purpose | Why it stays a seed, not a runtime authority |
| --- | --- | --- |
| [bytefer/awesome-shadcn-ui](https://github.com/bytefer/awesome-shadcn-ui) | Discover component libraries, focused widgets, native/framework ports and templates. | Its live README mixes free code, Pro products, affiliate links, templates and ports. It still links assistant-ui through an older owner (`Yonom`) and Tremor as `tremor-raw`; current upstreams differ. Every selected candidate needs canonical ownership and license verification. |
| [klaufel/awesome-design-systems](https://github.com/klaufel/awesome-design-systems) | Discover system governance, tokens, pattern libraries, a11y and component testing references. | The fetched README combines current additions with older Storybook addon names and dated articles. Category breadth is useful; inclusion does not establish current compatibility. |
| [goabstract/Awesome-Design-Tools](https://github.com/goabstract/Awesome-Design-Tools) | Discover tools by design activity: accessibility, animation, research, prototyping, handoff, assets and visual debugging. | The current text still contains historical LisaDziuba paths and old product descriptions. Use its taxonomy and leads, not its free/paid/platform badges as current guarantees. |
| [punkpeye/awesome-mcp-servers](https://github.com/punkpeye/awesome-mcp-servers) | Discover design-data, browser/device inspection, accessibility and agent tool adapters. | Very broad and includes advertisements and badges. Server listing is not a verification result. Promising entries opened directly: Framelink, Storybook MCP, and agent-device. |

All four READMEs were fetched live in this run. The content changes over time; a future maintained catalog should pin the exact commit or content hash. Do not copy their enormous lists into the design router.

#### Shortlist by purpose: component sources and registries

“Registry” here includes code registries/catalogs and platform component sources; they do not all implement the shadcn registry protocol. **No registry endpoint or namespace below should be guessed when it is not documented.** Recommendations are candidates for adoption, not changes to the user's dependencies.

| Purpose | Shortlist / official URL | Confirmed source and licensing | Fit and unresolved compatibility |
| --- | --- | --- | --- |
| Product UI | [shadcn/ui](https://ui.shadcn.com/) | Official repository [MIT license](https://github.com/shadcn-ui/ui/blob/main/LICENSE.md) fetched. Official MCP/registry mechanics are covered by the adjacent researcher. | Baseline only for the matching project stack. Inspect existing `components.json`, installed versions, tokens and primitive choice. Third-party registry entries do not inherit the shadcn repository's license. |
| Data-heavy dashboards | [Tremor](https://tremor.so/) | [Current upstream](https://github.com/tremorlabs/tremor) describes copy/paste React charts and dashboard components built on Tailwind and Radix; declares **Apache-2.0**. | React dashboard candidate. Verify chart dependencies, Tailwind generation, contrast, keyboard access and large-data behavior in the exact selected component. Do not assume the former `tremor-raw` link or a Pro product shares every current property. |
| Marketing / motion | [Magic UI](https://magicui.design/docs) | [Current upstream](https://github.com/magicuidesign/magicui) links documentation and declares **MIT**. Animated-component purpose is also documented by the [seed catalog](https://github.com/bytefer/awesome-shadcn-ui). | Pick specific effects for a brief; verify React/Tailwind/Motion versions and reduced-motion behavior. Magic UI Pro appears as a separate product in the catalog; its commercial terms were not inspected. |
| AI interfaces, component-first | [AI Elements](https://elements.ai-sdk.dev/) | [Vercel upstream](https://github.com/vercel/ai-elements) documents shadcn-based React conversation/message/reasoning components and registry URLs; [LICENSE](https://github.com/vercel/ai-elements/blob/main/LICENSE) is **Apache-2.0**, independently fetched. | README documents Next.js + AI SDK, initialized shadcn, Tailwind CSS variables. Inspect actual installed AI SDK/message API versions before using copied examples. Documented registry index: `https://elements.ai-sdk.dev/api/registry/registry.json`. |
| AI interfaces, runtime/interaction-first | [assistant-ui](https://www.assistant-ui.com/docs) | [Current upstream](https://github.com/assistant-ui/assistant-ui) documents streaming, attachments, auto-scroll, tool rendering, runtime adapters, and **MIT**; optional Assistant Cloud is a separate service. | Choose when its runtime abstractions solve the task. README currently offers Base UI default or Radix variants; verify chosen flavor and adapter. It links React Native and Ink packages, but feature parity and those packages' constraints were not checked. |
| Native / Expo React Native | [React Native Reusables](https://reactnativereusables.com/docs) | [Upstream](https://github.com/mrzachnugent/react-native-reusables) explicitly uses React Native + Nativewind and declares **MIT**. | Candidate only when React Native is the actual stack. Validate Nativewind/Expo/RN versions, native semantics, keyboard/safe-area behavior and platform differences. It is not a SwiftUI or Jetpack Compose library. |
| Native Apple and Android | [Apple Design](https://developer.apple.com/design/); [Android UI design](https://developer.android.com/design/ui) | Apple identifies HIG, official Figma/Sketch resources, SF Symbols and platform design videos. Android identifies adaptive phone/foldable/tablet design and desktop, Wear, TV and other device families. | Prefer official platform controls and native implementation docs. These are platform authorities, not interchangeable downloadable code registries. Asset/font/icon terms require their own checks; this run did not establish redistribution rights. |

#### Useful skills: a small, role-specific set

- **Existing web review/performance guidance:** [vercel-labs/agent-skills](https://github.com/vercel-labs/agent-skills) documents `web-design-guidelines`, React best practices, React Native guidance, composition and motion skills; declares MIT. Its discovery section says changes to main publish immutable releases containing a discovery index and a per-skill artifact. This is a particularly useful model for maintainable skill distribution. The harness already advertises web-design-guidelines and vercel-react-best-practices; prefer those current installed skills for their matching tasks rather than adding another copy.
- **Distinctive visual direction:** [Anthropic frontend-design SKILL.md](https://github.com/anthropics/skills/blob/main/skills/frontend-design/SKILL.md) was fetched directly. It ties visual choices to audience/subject, proposes a brief→plan→review→build→critique loop, stresses purposeful motion and concrete UI copy, and says the brief wins over generic aesthetic prohibitions. Its [per-skill license](https://github.com/anthropics/skills/blob/main/skills/frontend-design/LICENSE.txt) is Apache-2.0. It is guidance for a visual-design task, not a universal substitute for product interaction or platform conventions.
- **Focused polish/review workflow:** [Impeccable](https://github.com/pbakaus/impeccable) currently documents a single skill with subcommands including shape, audit, critique, polish, harden and animate, plus `PRODUCT.md`/`DESIGN.md` conventions. It is Apache-2.0. **Important maintenance detail:** the current README describes launchers, a binary engine downloaded on first use in some installs, and provider hooks. Treat its distribution as executable tooling requiring explicit adoption, not merely a block of prose. Its font/color prohibitions are an opinionated style source, not universal native/product design requirements.
- **Apple implementation depth:** [AvdLee/SwiftUI-Agent-Skill](https://github.com/AvdLee/SwiftUI-Agent-Skill) documents on-demand references for SwiftUI state, navigation, lists, accessibility, macOS windows and profiling; MIT. It also ships an executable `xctrace` helper and describes plugin-manifest migration. Pin the reference to the app's SDK/deployment target and inspect scripts before adopting. Its claims about the newest SDK were not independently validated against Apple release notes in this run.
- **Architecture precedent rather than default dependency:** [plugin87/ux-ui-agent-skills](https://github.com/plugin87/ux-ui-agent-skills), Brain B3, supplies router/adapters/crosswalk ideas. Its broad persona and large style library overlap the proposed family, so compare selective architectural ideas rather than layer a competing router wholesale.
- **Focused remote discovery:** [UI Skills upstream](https://github.com/ibelick/ui-skills) documents an MCP at `https://www.ui-skills.com/mcp` with **`list_skills` and `get_skill`**, as well as CLI browsing. Repository license is MIT. The licensing and provenance of each returned third-party skill still need verification. This MCP was documented, not connected or executed here.

#### Design/review MCP examples worth retaining

| Tool | Verified upstream capability | Routing recommendation and limitations |
| --- | --- | --- |
| [UI Skills](https://github.com/ibelick/ui-skills) | List and fetch skill content through its documented registry MCP. | Candidate runtime discovery adapter when available. Fetching guidance does not install or authorize it. Keep the chosen author/upstream identity. |
| [Framelink / Figma-Context-MCP](https://github.com/GLips/Figma-Context-MCP) | Uses Figma API data, simplifies layout/styling context, needs a Figma access token; MIT indicated in README. | Design-file context candidate. Compare against the available official Figma integration before adopting a third-party bridge. Its “one-shot accuracy” wording is marketing, not measured evidence in this run. |
| [Storybook MCP addon](https://github.com/storybookjs/storybook/tree/next/code/addons/mcp) | [Fetched upstream README](https://raw.githubusercontent.com/storybookjs/storybook/next/code/addons/mcp/README.md) documents `@storybook/addon-mcp`, default `/mcp` endpoint and configurable path. | Good route to the project's own components and stories. This source is the `next` branch: confirm availability and APIs in the installed Storybook release before use. Full tool behavior and license were not audited. |
| [agent-device](https://github.com/callstack/agent-device) | Current upstream reached through the `callstackincubator` alias documents CLI/MCP/Node API, accessibility snapshots, refs, screenshot evidence and iOS/Android plus additional targets; MIT. It explicitly emphasizes installed, version-matched help. | Candidate native review/verification adapter. Inspect current platform prerequisites and available device; don't infer an operational simulator from a catalog entry. No device was operated here. |
| [Inspo](https://github.com/Nutlope/inspo) | Upstream describes a read-only MCP for captured production-site references, extracted palettes/fonts/tokens, and reference components; hosted endpoint `https://inspomcp.dev/api/mcp`. MIT code; screenshots remain designers' work, with source credits/takedown process. | Inspiration/evidence candidate, especially marketing layout exploration. Never treat a screenshot's availability as a license to copy assets, or a generated extraction as an authoritative product design system. No MCP call was made here. |

The current agent-device upstream has a broader executable MCP than the older “discovery router” description in the awesome list. That concrete mismatch is another reason runtime discovery must inspect the live tool contract rather than preserve directory prose as its API. — [Seed entry](https://github.com/punkpeye/awesome-mcp-servers); [current upstream](https://github.com/callstack/agent-device).

#### Platform guidance: avoid a web-only /design router

- **Apple mobile and macOS:** the [Apple Design hub](https://developer.apple.com/design/) is the verified entry point to HIG, platform assets and videos. Follow the actual OS and SDK. The HIG body itself did not extract in this run; specific touch-target, type-size or Liquid Glass rules are therefore not asserted here.
- **Android:** [official UI guidance](https://developer.android.com/design/ui) explicitly separates mobile/adaptive layouts, desktop windowing/input, Wear, TV, widgets, cars and XR. Route by form factor, not just “Android.” The page links its own design kits and Now in Android sample.
- **Windows desktop:** [Microsoft's design hub](https://learn.microsoft.com/en-us/windows/apps/design/) grounds app design in Fluent, layout/navigation/input/typography/motion and ready-to-use resources. It supports a desktop-specific route rather than treating Electron or a narrow viewport as native Windows design.
- **CLI:** [Command Line Interface Guidelines](https://clig.dev/) discusses help, examples, stdout/stderr, machine-readable JSON, TTY detection, no-color and cancellation. It **explicitly excludes full-screen terminal programs**. Do not use it as complete TUI guidance.
- **TUI:** [Bubble Tea](https://github.com/charmbracelet/bubbletea) documents a Go/Elm-style model-update-view system, keyboard/mouse behavior, cell rendering and Bubbles components, with a v1→v2 migration guide; MIT. Treat it as a framework-specific reference, not a mandated replacement for an existing OpenTUI, Ink, Ratatui or Textual app. The installed harness's terminal-control skill is a relevant verification route for the project's actual TUI.
- **Web review:** [Vercel's skill collection](https://github.com/vercel-labs/agent-skills) explicitly covers keyboard focus, forms, reduced motion, theming, i18n, state and performance; [Storybook's own MCP](https://raw.githubusercontent.com/storybookjs/storybook/next/code/addons/mcp/README.md) provides a project-local integration candidate. Pair semantic/interaction inspection with rendered evidence, rather than treating a static visual catalog as review coverage.

### Inferences

- Adopt by **task fit and evidence**: a dashboard's operational density, sorting/selection, loading/error/empty states and keyboard navigation matter more than a library's marketing demo; a landing page may warrant a motion library that would distract from a daily-use administration screen.
- Keep several kinds of resources explicit: `guideline`, `skill`, `component-registry`, `component-library`, `reference-gallery`, `design-data-adapter`, `verification-tool`. “MCP” describes a transport/interface, not proof of design expertise.
- Use the project's current design tokens, components and stories as the first runtime discovery source. Remote catalogs should fill a specific missing capability, not trigger an unsolicited design-system replacement.
- Skills with aesthetic opinions need precedence rules: user brief → existing product/system constraints → platform conventions and accessibility requirements → optional style advice. Do not turn “avoid default fonts” into a ban on native system typography.

### Gaps

- No exact selected component was compiled against a real application. README compatibility is claimed support; peer dependencies and imported code must be checked at adoption time.
- Most license statements above came from primary README declarations; shadcn, AI Elements and Anthropic frontend-design also had license text fetched. These are not transitive-dependency or premium-asset license audits.
- Apple HIG and several generic pages initially failed Agentscrape with `upstream_unavailable`, evidence `Plugin 'stack' returned success=false`. `agentscrape doctor` passed and reported its browser/GitHub dependencies available; it did not resolve the live plugin failure. Direct read-only WebFetch recovered Android, Windows, CLI guidance and Apple's design hub. Apple HIG itself remained empty.
- Agentscrape refused the Storybook tree URL as an invalid URL; its exact public raw README was then fetched successfully. The `clig-dev/cli-guidelines` guessed repository path failed; the successfully fetched `clig.dev` page identifies the actual upstream as [cli-guidelines/cli-guidelines](https://github.com/cli-guidelines/cli-guidelines). Neither failed path is presented as verified evidence.
- Mobbin, 60fps and other X-only leads were not checked. The shortlist intentionally avoids claiming them as adopted or available.

## 3. How should /design discover resources at runtime without becoming a stale catalog?

### Takeaway

Make the router a small decision procedure with progressive loading. Keep mutable ecosystem inventories, review evidence and adoption history in maintainer data; runtime should resolve only the task-relevant adopted route against actual installed capabilities.

### Cited Findings

- UI Skills' saved root entry explicitly routes by **topic, stack and intent to the smallest useful set**, while the live upstream exposes a two-tool discovery surface. — [Brain B1: UI Skills](https://www.ui-skills.com/); [upstream MCP contract](https://github.com/ibelick/ui-skills).
- Vercel documents immutable release artifacts and a discovery index; SwiftUI Expert documents on-demand references and manifest/path migration. These support pinned, progressive skill loading rather than importing one giant mutable text corpus. — [Vercel agent skills](https://github.com/vercel-labs/agent-skills); [SwiftUI Expert](https://github.com/AvdLee/SwiftUI-Agent-Skill).
- Xcom's actual contract separates status/search/context from sync and index repair; its absence in this runtime did not prevent direct provider discovery. — [Xcom API](file:///Users/arthack/code/stack/packages/xcom/api.ts); observed socket outcome in section 1.
- Upstream providers can change executable behavior behind stable names: current Impeccable includes launchers/hooks, and current agent-device documents a direct command MCP where the list calls it a discovery router. — [Impeccable](https://github.com/pbakaus/impeccable); [agent-device](https://github.com/callstack/agent-device); [MCP seed catalog](https://github.com/punkpeye/awesome-mcp-servers).

### Inferences

#### Recommended runtime procedure

1. **Resolve the task and environment.** Determine design versus implementation versus review, the deliverable, audience/workflow, platform and form factors, repository stack, current design system and constraints. Ask only for material missing decisions.
2. **Inspect local authority.** Read relevant project guidance, package/deployment versions, token definitions, existing components and tests/stories. Discover only the available tools/skills matching the task. A skill being mentioned in Brain or a README does not establish that it is installed.
3. **Load a minimal route.** Shared design reasoning + one platform/stack reference + the relevant task workflow. Add motion/data-viz/a11y specialists only for a concrete facet. Avoid loading multiple competing high-level design personas.
4. **Fill a named evidence gap.** Search Brain and retrieve useful hits; if current discovery is needed, try an available read-only Xcom route or approved source catalog. Open the actual upstream, current documentation and selected implementation. Bound result count/context, and keep provenance.
5. **Report availability honestly.** Resolve `installed`, `connected`, `authenticated` and `usable-for-this-task` independently. On absence, continue with supported evidence/implementation routes and record the missing capability. No auto-install or service restart follows from failed discovery.
6. **Separate adoption/installation.** Runtime can recommend a candidate with evidence and compatibility questions. Installation, dependency edits, downloaded launchers, hook configuration and new MCP connections are explicit implementation/maintenance actions, not side effects of reading a catalog.
7. **Verify at the correct surface.** Browser plus semantic/keyboard evidence for web; actual native accessibility and rendered app/device evidence for mobile/desktop; help/streams/exits/pipes for CLI; PTY screens, navigation, resizing and cancellation for TUI. Preserve observed evidence and uncertainty.

#### Maintainer-only resource schema

This is a proposed information model, not a demand to create a runtime database. A checked-in YAML/JSON catalog plus a short generated routing summary is sufficient initially. Fields without evidence should be `unknown`/null, not inferred from popularity.

```yaml
schema_version: 1
id: stable-resource-id
name: Human-readable name
kind: skill # guideline|component-registry|component-library|gallery|mcp|verification-tool
purpose: [product-ui, data-heavy] # marketing-motion|ai-interface|native|cli|tui|review
ownership:
  upstream_owner: canonical organization or author
  maintainer: local role/person responsible for adoption
  upstream_url: canonical source URL
  historical_aliases: []
  ownership_last_checked: YYYY-MM-DD
lifecycle:
  adoption: candidate # adopted|retired
  upstream_status: active # archived|deprecated|unknown
  reason: specific capability and tradeoff
  decision_ref: null
  replacement_id: null
version:
  catalog_record_version: 1
  release: null
  commit: null
  content_digest: null
  installed_version: null
  validated_versions: []
provenance:
  discovered_via: brain # xcom|awesome-list|official-docs|project
  discovery_url: null
  brain_document_id: null
  brain_chunk_ids: []
  tweet_ids: []
  primary_sources: []
  retrieved_at: null
  last_verified_at: null
  source_updated_at: null # distinct from retrieval and index dates
  redirect_chain: []
evidence:
  level: catalog-lead # primary-docs|source-inspected|locally-exercised|scenario-validated
  claims: [] # each: statement, source, version, evidence, limitations
  scenarios_passed: []
  unresolved: []
fit:
  platforms: []
  form_factors: []
  frameworks: []
  framework_versions: []
  primitive_system: null
  styling_and_token_model: null
  required_dependencies: []
  deployment_targets: []
  exclusions: []
license:
  code_spdx: unknown
  license_url: null
  evidence_type: unknown # file|README|catalog
  asset_terms: unknown
  service_or_pro_terms: unknown
  transitive_review: unknown
runtime:
  eligible: false # normally true only for adopted entries
  trigger: precise task/environment match
  instruction_entrypoint: null
  reference_paths: []
  capability_probe: null # documented help/schema/status, never guessed names
  documented_endpoint: null
  read_operations: []
  mutating_operations: []
  auth_requirements: []
  fallback: null
maintenance:
  review_cadence: quarterly
  next_review_at: null
  triggers: [major-release, api-change, license-change, owner-change, failed-probe]
  acceptance_scenarios: []
  last_review_outcome: null
  retirement_condition: null
```

Important separations:

- **Record version / upstream version / installed version** are different facts.
- **Adoption state / upstream status / runtime availability** are different axes. An adopted resource may be unavailable today; an active, reachable tool may still be an unreviewed candidate.
- **Primary documentation / source inspection / executed scenario** are different evidence levels. A README says what the author intends; a successful scenario supports one tested behavior. Stars and generalized confidence numbers add no substitute evidence.
- **Discovery provenance / final authority** are different fields. Keep the X post or list that found the resource, while citing the canonical upstream for interface and licensing claims.
- **Maintainer inventory / runtime route** are different documents. Runtime gets triggers, fit, prerequisites, entrypoints and fallbacks; the broader evidence ledger stays out of default context.

#### Cadence and trigger recommendation

- Review adopted fast-moving skill/MCP integrations monthly, or immediately on a failed probe, major release, owner/URL change, license change, tool rename or new executable behavior.
- Review component registries at selection time against the project's locked versions; periodically check adopted registry health. Never bulk-update copied components merely because a catalog changed.
- Review platform guidance at SDK/OS major changes and when raising deployment targets. Store which version informed a decision.
- Review broad seed catalogs quarterly. Promote only candidates that close a concrete gap and pass an acceptance scenario; retire redundant or incompatible routes with a replacement/reason.
- Do not make every /design request perform an ecosystem refresh. Freshness checks should be bounded and tied to the task or a maintenance trigger.

#### Acceptance scenarios for the router family

These are proposed behavior checks for later evaluation, not implementation-mirroring unit tests:

1. **Existing SaaS settings UI:** finds the project's tokens/components first, loads matching product/web guidance, handles error/empty/disabled states, and verifies keyboard operation; does not introduce a new registry just for visual novelty.
2. **Dense dashboard:** identifies data density, filtering/sorting/selection, loading and chart accessibility needs before considering Tremor; records version fit and renders representative long/empty data.
3. **Marketing hero with motion:** chooses a coherent direction tied to the brief, uses a narrowly selected effect, checks small-screen layout and reduced motion, and distinguishes code license from photography/font rights.
4. **Streaming agent interface:** compares the actual need for AI Elements versus assistant-ui runtime behavior; validates tool-call, retry/cancel, long-content and scrolling states against the installed AI SDK, rather than blindly copying a README sample.
5. **SwiftUI iPhone/macOS:** routes to Apple guidance and the actual SDK, uses native controls/typography semantics, and requests native evidence; does not substitute React Native Reusables because “native” appears in its name.
6. **Android phone/tablet/desktop:** selects adaptive-layout and input guidance and verifies the relevant target; does not equate responsive web CSS with native Android adaptation.
7. **CLI versus TUI:** CLI route checks help/JSON/streams/exit status/pipes/no-color; full-screen TUI route additionally checks real PTY focus, resizing, navigation and cancellation. The router respects clig.dev's stated full-screen exclusion.
8. **Missing research transport:** Xcom socket absence is reported as unavailable; Brain citations and an available authorized discovery path remain useful. No sync, database creation or install happens silently.
9. **Catalog/upstream conflict:** old owner/path or differing API description is resolved through upstream metadata; the catalog record preserves the old alias and updates last verification, rather than treating both entries as unrelated tools.
10. **Unreviewed remote skill with scripts:** fetching it produces a candidate and executable-behavior note; it does not activate, install or override the current workflow automatically.
11. **Offline task:** already-adopted installed references continue to route without a network catalog fetch; unavailable freshness checks are stated precisely.
12. **Retired candidate:** an old Brain or X hit cannot revive a retired route without a new review and adoption decision.

### Gaps

- Ownership of the local /design family and adoption decisions remains a coordinator/user choice. The schema intentionally does not fabricate an owner or mark candidates adopted.
- The proposed cadence and scenarios are recommendations, not claims that any listed resource has passed them.
- Official shadcn MCP/Stack routing, Shoogle/WebMCP, and local wiki doctrine are adjacent researchers' scope and should be merged with these findings before finalizing the family architecture.
