# Make design judgment travel across platforms

**Status: proposed architecture; research complete, implementation pending. Research snapshot: 2026-09-29.**

Build `/design` as a **decision workflow and medium-sensitive judgment router**, supported by five independently useful specialists. The family should turn the consolidated AgentWiki doctrine into concrete briefs, alternatives, state models, component choices, and actual-target evidence. Platform references supply mobile, desktop, CLI, TUI, and web mechanics; existing implementation and observation skills supply stack-specific expertise. Reuse starts inside the project, then reaches official shadcn components/blocks where appropriate, escalating to community sources only for a named gap. Official shadcn discovery and Shoogle’s HTTP MCP were exercised during research, but their outputs require source inspection and project-context checks. Maintenance records belong outside runtime skill bundles. This report proposes the architecture and an abbreviated entrypoint; it claims no skill-performance results or completed deployment.

## 1. Six skills give the doctrine operational boundaries

The primary authority is the three consolidated wiki guides retrieved in full through `agentwiki get`: `designing-interfaces-with-clarity-and-character`, `designing-interactions-that-feel-trustworthy-and-alive`, and `a-practical-design-exploration-and-critique-playbook`. Their practical contribution is judgment tied to task, state, medium, and evidence. Historical Signal Room/Fleet TUI documents are tombstoned predecessors; their palettes, shell prohibitions, and shortcuts should not return as universal rules. ([Corpus evidence](../research_notes/Design%20skill%20architecture/design-corpus.md))

| Proposed skill | Distinct job and useful direct-invocation output |
|---|---|
| `/design` | Own intake, proportional workflow, medium/stack routing, decisions, and completion. Deliver a coherent answer or implemented slice. |
| `/design-explore` | Resolve one consequential uncertainty using a baseline and one or two genuinely different alternatives; return tradeoffs and a recommendation. |
| `/design-visual` | Establish hierarchy, subject-specific character, typography/spacing roles, and reusable visual systems; return composition/token decisions and adoption rules. |
| `/design-interaction` | Model state meanings, input, continuity, cancellation, recovery, and purposeful motion; return a state/transition contract and verification scenarios. |
| `/design-components` | Find and select compatible reusable material; return an inspected shortlist, dependency/file implications, and implementation handoff. |
| `/design-critique` | Audit existing work or diagnose a repair; return prioritized evidence-linked findings, corrections, and recheck requirements. |

The corpus notes favor one skill plus references to minimize duplication. That is a sound restraint, but the requested **family** earns five leaves through different outputs and independently useful invocation boundaries. Split by substantial workflow knowledge, not by platform label: five near-identical platform skills would repeat intake while obscuring differences in interaction and evidence. Keep platform details in conditional references. Merge a leaf later if usage shows it adds only forwarding boilerplate.

Each leaf starts from available intent, constraints, and evidence; it does not invoke `/design` to restart intake. The current task retains one decision owner, and an in-context loaded-reference list prevents circular or duplicate loading. Proposed authoring budgets are 700–1,000 words for the root and 400–700 per leaf, with an ordinary initial route below roughly 2,500 words: root, one leaf, one target reference. These are design targets, not measured savings. Author shared doctrine once and package necessary excerpts locally so direct leaf invocation remains self-contained.

| Doctrine becomes a move | Required decision or artifact |
|---|---|
| Begin with the person’s job | Identify real material, primary action, and constraints before choosing layout. |
| Make hierarchy relational | Diagnose excess content separately from competing emphasis; propose ordering/grouping before decoration. |
| Give different facts different states | Define what “requested,” “saved,” or “complete” actually establishes; distinguish missing measurements from zero. |
| Preserve continuity | Specify what survives refresh: drafts, selection, focus, reading position, and action identity. |
| Compare honestly, adopt exactly | Hold content/state/size constant; record the reviewed choice and verify its adoption in the product. |

These moves derive respectively from the visual, interaction, and exploration guides; they replace vague directions such as “make it premium.” Expression remains welcome when it belongs to the subject and preserves truthful control feedback. ([Visual guide](file:///Users/arthack/wiki/designing-interfaces-with-clarity-and-character.md), [interaction guide](file:///Users/arthack/wiki/designing-interactions-that-feel-trustworthy-and-alive.md), [playbook](file:///Users/arthack/wiki/a-practical-design-exploration-and-critique-playbook.md))

## 2. Route by working mode, then verify the actual medium

Use five working modes: **explore, build, repair, audit, system**. They are task states, not additional skills. Inspect the request, repository instructions, actual stack, existing components/tokens, accepted decisions, and available evidence first. Research only a named gap, starting with Brain when outside knowledge is needed. Compare alternatives only when a consequential design choice remains; select a direction, implement when requested, then verify the target. A clipped-label repair needs a bounded correction and narrow-width check, not an ecosystem survey. Audit findings follow **observed issue → affected task → evidence/location → correction → recheck**. Repair adds reproduction and before/after evidence; build adds implementation and adoption status; system adds semantic roles, platform mappings, and migration guidance.

### Stage × medium routing matrix

For `/design` invocations, the root integrates; table entries identify the dominant specialist and substantive target work.

| Surface | Explore | Build | Repair | Audit | System |
|---|---|---|---|---|---|
| Mobile | Explore: navigation/reach alternatives | Interaction: back, keyboard, safe areas, lifecycle | Interaction: release/background/cancel boundaries | Critique: scaling, touch, assistive flow | Visual: semantic roles with iOS/Android adaptations |
| Desktop | Explore: workspace/window organization | Interaction: focus, menus, shortcuts, resize | Interaction: first-click, IME, identity races | Critique: real window and keyboard flow | Visual: window/control patterns and persistence |
| CLI | Explore: command vocabulary and output order | Interaction: streams, exits, help, recovery | Critique: pipe/machine-format compatibility | Critique: non-TTY, no-color, interruption | Visual: output roles plus stable command contracts |
| TUI | Explore: cell-native hierarchy/disclosure | Interaction: focus/modal ownership and refresh | Critique: narrow/shallow layouts, glyph widths | Critique: navigation, resize, terminal restoration | Visual: cell-density and semantic-state vocabulary |
| Web | Explore: content hierarchy and composition | Visual/components: existing stack and responsive states | Critique: bounded layout/flow correction | Critique: semantics, focus, zoom, forms | Visual: tokens, patterns, component-state contracts |

Mobile web keeps web semantics while adding touch, viewport/keyboard, orientation, and safe-area questions. Native mobile uses the actual iOS/Android/React Native/Flutter stack; “native” does not imply Native SDK. Desktop WebViews need both shell and web evidence. CLI guidance concerns commands, streams, machine output, and cancellation; it expressly differs from full-screen TUI craft. Official Apple, Android, and Windows guidance provides platform entrypoints, while quantitative rules should be checked against the concrete SDK/target. ([Apple Design](https://developer.apple.com/design/), [Android](https://developer.android.com/design/ui), [Windows](https://learn.microsoft.com/en-us/windows/apps/design/), [CLI Guidelines](https://clig.dev/))

Reuse `shadcn` for an established/selected shadcn project, `ai-elements` for that adopted chat component family, and `ai-sdk` only when implementation touches its behavior. Select one chat-scroll owner: existing shadcn `MessageScroller` and AI Elements conversation wrappers should not be layered automatically. Use React performance guidance for React work; web-design-guidelines for web audits. Invoke `native-sdk` only when project evidence establishes it. `desktop` supplies macOS observation; `terminal-control` supplies real PTY operation. A design **build mode** does not implicitly activate the explicit `/build` or `/collab` workflows. ([Installed-skill boundaries](../research_notes/Design%20skill%20architecture/design-corpus.md#existing-specialists-worth-reusing))

**Evidence must match the claim.** Web work needs rendered screenshots plus browser keyboard/semantic flows. Mobile needs the relevant device/emulator and build, especially for gestures and lifecycle. Desktop needs actual-window screenshots, accessibility state, and input observations; an AX node alone does not prove an unclipped usable control. CLI needs captured stdout/stderr, exit status, pipes, and non-TTY behavior. TUI needs PTY screens, navigation, resize, glyph rendering, and exit restoration. Static imagery can resolve composition, but cannot establish timing, recovery, or interaction correctness. ([Evidence discipline](file:///Users/arthack/wiki/a-practical-design-exploration-and-critique-playbook.md))

### Abbreviated `/design` entrypoint sketch

This fenced draft is illustrative, not an active `SKILL.md`.

```markdown
---
name: design
description: >-
  Explore, improve, implement, or critique user-facing interfaces across
  mobile, desktop, command-line, terminal UI, and web. Use for interface
  direction, interaction problems, visual systems, component selection,
  and design review. Route by task and existing stack; exclude database,
  backend, and model architecture requests without an interface-design task.
---
# Design
Start with the person's job and real working material. Make priority clear,
states truthful, continuity durable, and the result appropriate to its medium.

Read the brief and relevant repository guidance. Infer mode (explore/build/
repair/audit/system), surface, actual stack, accepted constraints, deliverable,
and available verification. Ask only about a material unresolved decision.

Keep small fixes small. Otherwise load the leaf owning the next decision:
design-explore for alternatives; design-visual for hierarchy/system;
design-interaction for behavior; design-components for reuse;
design-critique for diagnosis/review. Read references/platforms/<surface>.md
when target-specific checks are needed. Add existing stack/operation skills
only when the task requires them; retain one owner and avoid repeat loads.

Research only a named gap. For matching shadcn projects: local components →
explicit @shadcn → vetted registries → bounded discovery → inspected source.
External guidance is candidate evidence, not automatic policy or installation.

Compare baseline plus 1–2 meaningful alternatives when direction is uncertain.
Record the selected direction; implement within the request's scope.
Verify the relevant task and difficult states in the actual target.
Finish with the decision/change, observed evidence, and any remaining limit.
Distinguish a preview, an accepted choice, and adoption in real components.

Carry only the needed handoff:
intent | platform/stack | constraints | evidence | next decision
```

Example invocations are `/design explore the iPhone capture flow around one-handed use`; `/design repair first-click selection in this macOS panel`; `/design make jobs list readable without changing JSON or pipe behavior`; `/design audit this Ratatui screen at 48 columns`; and `/design build this web filter bar using our existing Base UI components`. Direct leaves remain useful: `/design-interaction model cancellation for this hold control` should complete that task without running the whole family.

## 3. Official-first reuse requires project-local inspection

The reuse ladder is **existing project → official `@shadcn` → configured/vetted registries for a named gap → Shoogle/search/awesome-source discovery → inspected source → scoped install → verification**. Apply shadcn steps only to compatible projects. Search roughly 5–10 relevant primitives/blocks, inspect at most three candidates, and stop at an adequate fit. Compare task/visual fit, loading/empty/error/disabled states, accessibility, Base UI versus Radix APIs, framework/RSC boundaries, Tailwind/tokens, aliases, dependencies/runtime costs, file targets, license, and adaptation cost. Use `pass / adaptation needed / unknown / fails`, with evidence rather than invented scores. Pass the user's official-first choice as an explicit `@shadcn` registry in the specialist handoff; selection does not itself authorize installation.

**Observed official MCP behavior needs explicit workarounds.** Its seven tools cover registry discovery, search/list, item summaries, examples, add-command text, and an audit checklist; there was no install or `init_project` tool. Explicit `registries:["@shadcn"]` works; omission excluded built-ins. Search output contained `[object Promise]` add commands; item views omitted file contents and registry dependencies; examples resolved to fallback `new-york-v4` code using Radix-style `asChild`. These are dated observations explained by inspected source, not timeless defects. The MCP’s reduced configuration omits project base/style, and observed `mcp --cwd` loaded environment files without retargeting handlers using `process.cwd()`. Thus neither generated shell strings nor example code establishes project compatibility. ([Observed probes](../research_notes/Design%20skill%20architecture/shadcn-stack.md), [pinned MCP source](https://github.com/shadcn-ui/ui/blob/08ab84f7d1952cc1f36055aa8931213a86b01bbd/packages/shadcn/src/mcp/index.ts), [formatters/config](https://github.com/shadcn-ui/ui/blob/08ab84f7d1952cc1f36055aa8931213a86b01bbd/packages/shadcn/src/mcp/utils.ts))

Use the project-installed CLI for full `view` payloads, version-matched docs, and future `add --dry-run`/diff inspection. Local CLI probes used **4.21.0**; the session MCP's exact npm version was unverified. Review transformed imports, icons, dependencies, and routes before adoption: raw registry payloads contain templates. Direct catalog URLs serve search; item URLs serve view/add. CLI discovery can resolve namespaces without persisting configuration on the inspected version; a provider does not need its own MCP. Dynamic registry search means server-side `q/type/limit/offset` filtering, not universal semantic discovery. ([Namespaces](https://ui.shadcn.com/docs/registry/namespace.md), [dynamic search](https://ui.shadcn.com/docs/registry/dynamic-search.md), [CLI evidence](../research_notes/Design%20skill%20architecture/shadcn-stack.md#2-how-do-cwd-project-configuration-namespaces-and-dynamic-registries-interact))

### Stack owns delivery; process cwd owns project execution

Stack’s inspected UI uses Base Nova/Base UI, Tailwind v4, Next App Router, and pnpm in `/Users/arthack/code/stack/packages/ui`. Its Role machinery owns enabled skills, supporting files, MCP definitions, and launch snapshots. The stdio schema has no `cwd` field; HTTP definitions are also supported. A schema-compatible future project-bound definition is below; `pnpm --dir` process-cwd behavior was verified, but this definition was **not registered or exercised through Stack**. ([Role schema](file:///Users/arthack/code/stack/packages/roles/src/resources.ts), [integration evidence](../research_notes/Design%20skill%20architecture/shadcn-stack.md#3-how-should-design-connect-this-to-local-stack-and-choose-components))

```json
{
  "type": "stdio",
  "command": "pnpm",
  "args": ["--dir", "/Users/arthack/code/stack/packages/ui", "exec", "shadcn", "mcp"]
}
```

A shared Role can instead retain project-independent official discovery and execute all project inspection/install with `pnpm --dir <actual-app> exec shadcn …`. Process cwd still does not fix MCP base-selection omissions. Inspect effective Role metadata and `role_launch_preview` before a new launch; its `cwds` supports trust matching, not MCP rebinding. The Roles socket was unavailable, so the live Role inventory is unverified. Avoid inventing Stack interpolation APIs or using harness-config-writing `shadcn mcp init` as Role delivery. When implementation is authorized, adapt into existing Stack surfaces and run its required UI typecheck and actual-target checks. ([Launch contract](file:///Users/arthack/code/stack/packages/roles/api.ts), [Stack guidance](file:///Users/arthack/code/stack/AGENTS.md))

## 4. Discovery services nominate candidates, not dependencies

**Shoogle’s verified endpoint is `https://mcp.shoogle.dev/mcp`**, a documented no-auth Streamable HTTP MCP. Initialization, tool listing, global search, and scoped search succeeded. Exact tools are `search_registry_items(query, offset?, limit?)` and `search_registry_items_scoped(query, registries, offset?, limit?)`. They search item **names**, not demonstrated semantic/layout similarity. Results preserve registry/item provenance but contain no source or license audit. Serialize bounded calls; inspect JSON-RPC/MCP errors even after HTTP 200. Concurrent calls hit a rate limit, and documented bare namespace examples returned `unknownRegistries`; use exact returned/configured names rather than guessing prefixes. One query plus one refinement/page and one delayed read retry is a proposed budget, not a vendor guarantee. ([Shoogle contract](https://shoogle.dev/mcp/shoogle-skills), [observed calls](../research_notes/Design%20skill%20architecture/shoogle-webmcp.md))

An optional Stack HTTP resource can use `{ "type": "http", "url": "https://mcp.shoogle.dev/mcp" }` plus normal Role metadata. Prefer the normal MCP host over a custom protocol wrapper. The documented `shadcn search @shoogle` route deserves a small compatibility spike; it was not executed. Shoogle advertises semantic/layout discovery on its website, but browser search and preview were not demonstrated. ([Connection docs](https://shoogle.dev/mcp/other-mcp-clients), [CLI docs](https://shoogle.dev/mcp/cli))

**WebMCP is a different, page-exposed tool interface.** Current Chrome documentation uses `document.modelContext`; capability detection should enumerate actual page tools and schemas, or use agent-browser’s WebMCP catalog. Shoogle runtime support remains unknown: static markers were absent, but both browser paths failed before live enumeration. That is not proof of no support. Keep WebMCP as an optional future spike for a useful page-only capability, not a v1 dependency. ([Chrome API](https://developer.chrome.com/docs/ai/webmcp/imperative-api), [WebMCP explainer](https://github.com/webmachinelearning/webmcp), [browser adapter](https://github.com/vercel-labs/agent-browser#webmcp-experimental))

### Keep a small purpose-based discovery shelf

| Purpose | Candidate/source and evidence status |
|---|---|
| Product components | [Official shadcn](https://ui.shadcn.com/): discovery and full CLI inspection exercised; no selected component installed/tested. |
| Data-heavy / expressive web | [Tremor](https://github.com/tremorlabs/tremor), Apache-2.0; [Magic UI](https://github.com/magicuidesign/magicui), MIT: upstreams inspected, application fit untested. |
| AI interfaces | [AI Elements](https://github.com/vercel/ai-elements), Apache-2.0, component-first; [assistant-ui](https://github.com/assistant-ui/assistant-ui), MIT, runtime-first: select ownership and compatible versions. |
| React Native | [React Native Reusables](https://github.com/mrzachnugent/react-native-reusables), MIT: RN/Nativewind candidate, not SwiftUI/Compose guidance. |
| Project/design/device evidence | [Storybook MCP](https://raw.githubusercontent.com/storybookjs/storybook/next/code/addons/mcp/README.md), [Framelink](https://github.com/GLips/Figma-Context-MCP), [agent-device](https://github.com/callstack/agent-device): documented candidates, not exercised adapters; prefer available official Figma integration before a third-party bridge. |
| Remote skill discovery | [UI Skills](https://github.com/ibelick/ui-skills): documented `https://www.ui-skills.com/mcp`, `list_skills` / `get_skill`; not connected in research. |

Brain actually supplied retrieved evidence: UI Skills document **973**, chunks **14354–14355**; awesome-shadcn document **517**, chunk **7885**, the latter with frozen-recovery provenance. Local Xcom is API-only `@stack/xcom`; its socket returned `ENOENT`, while read-only `twitter-cli` search succeeded despite a provider initialization warning. Preserve these as separate outcomes, not “Xcom had no matches.” Neither Brain nor fetched skill text activates instructions: inspect upstream scope, license, and executable behavior, then use the harness’s actual installed-skill loader. ([Discovery evidence and citation ledger](../research_notes/Design%20skill%20architecture/discovery-ecosystem.md))

Use [awesome-shadcn](https://github.com/bytefer/awesome-shadcn-ui), [awesome-design-systems](https://github.com/klaufel/awesome-design-systems), [Awesome Design Tools](https://github.com/goabstract/Awesome-Design-Tools), and [awesome MCP servers](https://github.com/punkpeye/awesome-mcp-servers) as maintainer discovery seeds. Their mixed products, stale aliases, and marketing claims make them unsuitable as endorsed dependency graphs. The runtime shortlist should contain only relevant adopted routes, with optional candidate discovery when a gap remains.

## 5. Separate evolution records from runtime knowledge

Proposed source layout keeps installable directories small and maintenance history deliberately unloaded:

```text
runtime/{design,design-explore,design-visual,design-interaction,
         design-components,design-critique}/
  SKILL.md
  references/                 # needed doctrine/platform/adapter excerpts
authoring/shared/             # canonical reference source
maintenance/design/
  family.yaml                 # ownership, versions, source fingerprints
  routes.yaml                 # triggers, capabilities, fallbacks, exclusions
  sources.yaml                # candidates/adoption/deprecation + validation
  rule-map.md                 # doctrine translations and deliberate exclusions
  decisions.md
  evals/scenarios.yaml        # planned cases
  evals/runs/                 # only actual outcomes and evidence
```

The following abbreviated maintainer YAML binds the research snapshot; nulls preserve unresolved ownership and unexecuted evaluation. Actual resource records should also distinguish upstream revision, installed version, and record version.

```yaml
schema_version: 1
family: design
version: 0.1.0-proposal
status: proposed
owner: null # decide before distribution
provenance:
  retrieved_at: 2026-09-29
  method: agentwiki-cli
  wiki:
    - slug: designing-interfaces-with-clarity-and-character
      sha256: 6c0fb842bd0d81cf63c3765b92f4d7000e38d81215d87e5bf7bac9b767df1180
    - slug: designing-interactions-that-feel-trustworthy-and-alive
      sha256: 60da2e46c91af204fe1bfffed8988d26366c405c2f0fe35cea877286a69b6728
    - slug: a-practical-design-exploration-and-critique-playbook
      sha256: 02c972a6b81d48c104cce2fb8bd1b17b2951504dc64f6601dbb7027802a2b124
routes:
  - id: shadcn-reuse
    trigger: matching-project-and-component-gap
    skill: design-components
    capabilities: [shadcn-search, project-local-cli]
    fallback: existing-components-and-source-docs
resources:
  - id: shoogle-http
    lifecycle: candidate # candidate -> adopted -> deprecated
    upstream: https://shoogle.dev/mcp/other-mcp-clients
    endpoint: https://mcp.shoogle.dev/mcp
    validation:
      status: locally-exercised
      date: 2026-09-29
      scope: [initialize, tools-list, global-name-search, scoped-name-search]
      limitations: [rate-limit-policy-unknown, namespace-example-mismatch]
    compatibility: {transport: streamable-http, project-integration: untested}
    license: {service_terms: unknown, item_license: inspect-at-source}
    runtime_eligible: false # candidate, not yet adopted
evaluations:
  scenarios: evals/scenarios.yaml
  outcomes: evals/runs/
  last_run: null
freshness:
  adopted_adapters: monthly
  seed_catalogs: quarterly
  triggers: [wiki-hash-change, failed-probe, major-release, license-change]
```

Record source/adapter scope and limitations per claim; keep compatibility and license at selected-item granularity. Promote candidates only after the intended scenario is observed; deprecate with reason/replacement. Recheck component fit at selection time and platform guidance at SDK/deployment-target changes. Repeated human corrections should become bounded doctrine changes backed by examples, not automatic global taste rewrites. ([Fingerprints and maintenance basis](../research_notes/Design%20skill%20architecture/design-corpus.md#primary-source-fingerprints))

### Measurable implementation phases

| Phase | Acceptance check |
|---|---|
| Curate doctrine | Map each operative rule to a consolidated section; record retired rules and five platform translations. |
| Author family | Six self-contained entrypoints; direct leaf use works; no route loops, competing chat owners, or mandatory research for small fixes. |
| Wire optional tools | Validate effective Role/launch metadata, CLI cwd/base, one official query, and optional serialized Shoogle query; retain offline fallback. |
| Evaluate scenarios | Compare baseline and family on non-React web, mobile cancellation, desktop first-click, CLI piping, narrow TUI, small repair, screenshot audit, and chat ownership; review actual evidence and scope/load behavior. Record outcomes separately from plans. |
| Install/distribute | Choose owner and managed source, verify six bundles plus references in a fresh intended session, and confirm maintenance files are excluded. |

Three material defaults need adoption: **six workflow skills with platform references; official MCP/CLI first with optional Shoogle HTTP; explicit source ownership before distribution**. Recommend retaining this repository as the authoring source only if AgentStart explicitly manages it; otherwise follow the existing AgentGuidance ownership route. Its current `~/code/agent*/skills/*` scan does not include `~/code/skills`, and whole-directory copying makes maintenance separation consequential. This is a concrete future deployment task, not a completed installation. ([Distribution evidence](../research_notes/Design%20skill%20architecture/design-corpus.md#distribution-and-ownership-evidence), [sync source](file:///Users/arthack/code/agentstart/scripts/sync-skills))

Research limitations are narrow but important: no family evaluations or component adoption ran; live Stack Role inventory and Shoogle browser/WebMCP behavior remain unverified; Apple HIG body extraction failed although its design hub was retrieved. Three paid agentsearch calls reported `cost_usd: null` and `cost_status: unavailable`; total cost is **unknown, not zero**. Tool-path failures establish unavailable observation, not missing product capabilities. ([Accounting and limitations](../research_notes/Design%20skill%20architecture/shoogle-webmcp.md#research-accounting-and-method-limitations))

## Conclusion

The valuable boundary is between a reusable decision and the evidence needed to trust it on a particular surface. This architecture makes that boundary explicit: doctrine shapes choices, specialists resolve concrete questions, and platform-specific observation establishes what actually works. Its next milestone is a small authored family evaluated on discriminating tasks—not a larger catalog of aesthetic instructions.
