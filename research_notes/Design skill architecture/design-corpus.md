# Design corpus and architecture for a cross-platform /design family

Research date: 2026-09-29. Scope: local, read-only investigation and architecture recommendations. AgentWiki discovery and retrieval used the **agentwiki CLI**, as requested. Agentbrain was searched before considering external research; no external research was necessary or performed. Recommendations below are proposals, not approved product requirements or deployed skills.

## 1. What substantive doctrine should /design enforce, and which sources are authoritative?

### Takeaway

The primary doctrine already exists in three deliberately consolidated, medium-aware guides. `/design` should turn their judgment into a small execution discipline: frame the person's job, choose a subject-specific organizing idea, preserve interaction truth and continuity, compare proportionately, and verify the actual target. It should not reinstall a historical house aesthetic or make a web component library the definition of design. [Visual guide, introduction and “Sources and editorial scope”][visual]; [Interaction guide, introduction][interaction]; [Playbook, introduction and “Reusable briefs for future skills”][process]

### Cited Findings

#### Primary documents read in full

All three were retrieved completely with `agentwiki get <slug> --json`. Each is tagged `consolidated-design`, created September 27, 2026. Their source paths and supporting sections are:

| Exact slug / source path | Role and decisive sections |
|---|---|
| `designing-interfaces-with-clarity-and-character` — `/Users/arthack/wiki/designing-interfaces-with-clarity-and-character.md` | Visual judgment, not a house palette: **Begin with the person's job**; **Choose a direction that belongs to the subject**; **Establish hierarchy through relationships**; **Diagnose quantity separately from intensity**; **Make typography and spacing do real work**; **Use a coherent visual vocabulary**; **Choose icons and assets as families**; **Make comparisons visually honest**; **Adapt the composition before compressing it**; **A short design review**; **Sources and editorial scope**. [Source][visual] |
| `designing-interactions-that-feel-trustworthy-and-alive` — `/Users/arthack/wiki/designing-interactions-that-feel-trustworthy-and-alive.md` | Behavioral truth: **Make actions and consequences legible**; **Give different facts different states**; **Refresh without stealing continuity**; **Design the entire gesture**; **Respect attention, placement, and recovery**; **Use motion to explain or express**; **Choreograph changes rather than tweening everything**; **Budget sensory events and design silence**; **Treat responsiveness as part of the design**; **Interaction review prompts**; **Sources and editorial scope**. [Source][interaction] |
| `a-practical-design-exploration-and-critique-playbook` — `/Users/arthack/wiki/a-practical-design-exploration-and-critique-playbook.md` | Working method: **Frame one consequential question**; **Use references to answer questions**; **Compare a few genuinely different alternatives**; **Prototype in the real renderer**; **Make the experiment predictable**; **Run short feedback loops**; **Critique from the largest relationship to the smallest detail**; **Verify the difficult states**; **Capture and adopt exactly the reviewed choice**; **Demonstrate the result without distorting it**; **Reusable briefs for future skills**; **Sources and editorial scope**. [Source][process] |

#### Doctrine with a practical consequence

1. **Start with person, job, material, priority, and constraint.** The useful content or working object should lead. A dashboard introducing twelve totals before the blocked work introduces the database rather than the person's problem. Consequence: a design brief must identify the primary job and the real material that demonstrates it before selecting components. [Visual, “Begin with the person's job”][visual]
2. **Character comes from belonging to the subject.** Ask whether changing the product name would make the proposal equally plausible for an unrelated product. Compare compositions and behaviors, not accent colors. Familiar systems are allowed; arbitrary novelty is not required. Consequence: require one defensible organizing idea, not a prescribed font, gradient ban, palette, or layout shell. [Visual, “Choose a direction that belongs to the subject”][visual]
3. **Hierarchy is relational.** Position, scale, weight, alignment, and spacing come before containment; peers deserve equivalent treatment, unequal things need not be equal cards. Borders, badges, numbering, rails, and connectors all make semantic claims. Consequence: critique grouping and priorities before local corner, shadow, or margin polish. [Visual, “Establish hierarchy through relationships”][visual]; [Process, “Critique from the largest relationship to the smallest detail”][process]
4. **Busy and loud are different defects.** Too much content calls for removal, ordering, combination, or disclosure. Too much competition calls for reduced weight and emphasis while preserving an anchor. Shrinking all text or making everything gray fixes neither. [Visual, “Diagnose quantity separately from intensity”][visual]
5. **Use coherent roles, not attractive fragments.** Semantic color, typography roles, one owner for each gap, consistent icon families, and aligned numeric comparisons form a system. Essential state needs a non-color cue; identity color and runtime state are different facts. [Visual, “Make typography and spacing do real work,” “Use a coherent visual vocabulary,” “Choose icons and assets as families”][visual]
6. **A status must name a fact the product can establish.** Requested/accepted/completed, generated/saved/reviewed, connected/flowing/perceived, and execution/quality are distinct. Missing measurements are not zeroes; an admission acknowledgement is not completion. Consequence: include a small state/meaning model for dynamic work, not just a happy-path screenshot. [Interaction, “Give different facts different states”][interaction]
7. **Preserve continuity and bind actions to identity.** Refresh should preserve useful committed content, drafts, selection, focus, disclosure, reading position, and user-chosen follow mode. Incoming content must not change the target between press and release. Consequence: background-update and identity-race checks matter more than decorative loading. [Interaction, “Refresh without stealing continuity”][interaction]
8. **Design the entire gesture and failed boundary.** Acquisition, immediate feedback, commit, cancellation, and release must be defined. Backgrounding, focus loss, removal, second pointers, and late acknowledgements must not leave holds latched. Save retry should preserve a successful generation rather than rerun it. [Interaction, “Design the entire gesture,” “Respect attention, placement, and recovery”][interaction]
9. **Expression is welcome, but it has a job.** Start with a coherent still composition; concentrate motion or sound rather than making every region animate. Control truth changes immediately, independently of decorative transitions. Reduced motion must leave a finished design and current information. [Interaction, “Use motion to explain or express,” “Choreograph changes rather than tweening everything”][interaction]
10. **Adapt composition to the medium.** Terminal glyphs are not square pixels; native controls carry platform expectations; touch involves fingers and occlusion. Reflow and disclosure precede shrinking. Safe content bounds differ from backgrounds; physical orientation can affect insets. Consequence: share semantic intent across platforms, not mandatory geometry or interaction mechanics. [Visual, “Choose icons and assets as families,” “Adapt the composition before compressing it”][visual]
11. **Use the smallest experiment that can answer the question.** Baseline plus one or two meaningful alternatives, matched content/state/size/readiness, and controlled synthetic state are preferred. A static comparison may establish hierarchy; gesture behavior needs an interactive target. Add studio infrastructure only when the experiment warrants it. [Process, “Compare a few genuinely different alternatives,” “Prototype in the real renderer”][process]
12. **Evidence has limits.** Source review establishes intended rules, screenshots establish visible composition, recordings show observed timing and gestures, and target-device tests establish behavior on that device/build. Neither a schema nor an accessibility-tree node proves an unclipped usable control. [Process, “Verify the difficult states,” evidence table][process]
13. **The reviewed snapshot and the shipped result are different steps.** Distinguish live, draft, checkpoint, production defaults, and rehearsal conditions. Save exactly the reviewed snapshot; adopt it into real components/tokens/assets and then check the actual product. Preserve relevant asset source and license information. [Process, “Make the experiment predictable,” “Capture and adopt exactly the reviewed choice”][process]

#### Consolidated guidance versus historical and product-specific material

- **The old TUI documents are tombstoned, not mysteriously missing.** CLI `get` returned `document_not_found`; reading their retained source files revealed `deleted: 2026-09-27...` and an explicit replacement reason naming the consolidated three. Their house palettes, shell rules, and historical implementation instructions were intentionally retired. Both full historical files were read to establish exactly what must not be promoted back into universal doctrine. [Signal Room frontmatter][signal]; [Fleet TUI frontmatter][tui]
- **Signal Room supplied terminal craft, not a universal shell.** Useful historical sections include **Type and language**, **Spatial system**, **Responsive behavior**, **Accessibility and terminal behavior**, and **Provenance and governance**. They discuss cell widths, comfortable versus compact density, readable semantic state, ANSI-free snapshots, terminal restoration, real-renderer Unicode/ASCII behavior, and changes justified by real evidence. Its teal rail, exact hex values, dark-only canvas, uppercase roles, no-header/no-footer rule, and unadvertised Ctrl+K are historical house choices. [Signal Room §§ “Canonical tokens” through “Provenance and governance”][signal]
- **Fleet TUI's specific shortcuts and pointer conventions are historical.** It prescribed Ctrl+K, mouse-wheel changes to values, first-letter matching, an entirely chromeless surface, and a particular Signal Room/OpenTUI anatomy. These are useful examples of explicit interaction contracts, not requirements for every terminal application. Its own general lesson was to sharpen judgment without importing Vercel branding or web components. [Fleet TUI, introduction, “Shell,” “Command palette,” “Interaction,” “Testing”][tui]
- **The consolidation corrected over-generalization.** The visual guide expressly excludes historical palettes, shell prohibitions, and exact shortcuts. The interaction guide says suitable input paths need equivalent outcomes, not identical gestures, and does not prohibit all progress feedback. It says discoverability must be earned rather than assuming a team-known shortcut is discoverable. [Visual, “Sources and editorial scope”][visual]; [Interaction, “Make actions and consequences legible,” “Refresh without stealing continuity,” “Design the entire gesture”][interaction]
- **The historical local design resource is a shelf, not current global taste law.** `/Users/arthack/resources/design-with-ai/README.md` was read in full. It indexes 53 documents and advertises a dark, monospaced, subtractive house style plus a taste-improvement pipeline. That README makes stronger aesthetic commitments than the newer consolidated guides, which explicitly allow quiet utilities, expressive instruments, and editorial websites to look different. Only the README was read; its underlying 53 documents were not re-researched. [Resource README][resource]; [Visual, introduction][visual]
- **AgentVoice's terminal signal field is a strong example of specific design.** Its **Honest derived signals** separates two amplitude envelopes, onset, dominance, contact, persistence, and declared idle time from unmeasured pitch, spectrum, phonemes, or sentiment. **Implementation rules** are cell-native and its **Built artifact** uses the real renderer under synthetic scenarios. The named contact-fault artwork, amber/blue strands, 24–30 fps suggestion, one-large-renderable implementation, and old Signal Room relationship are product-specific/historical. No current shipped status or running gallery was independently verified. [Signal-field research, full document][field]
- **Sound findings show how doctrine should evolve from corrected evidence.** **§2 The ensemble claim, stress-tested** replaces a binary events-versus-bed rule with a budgeted hybrid. **§5 Voice-agent coexistence** documents corrections to assumed transport, semantics, and acoustic behavior. Reusable lessons are event budgets, truthful signals, designed silence, and listening in actual use; the specific graph, loudness suggestions, fmx transport proposals, and old backend claims remain contextual. [Sonification findings, §§2, 3, 5, 7][sound]; [Interaction, “Budget sensory events and design silence” and editorial scope][interaction]
- **Saved Vercel web guidance is available, but has scope and freshness limits.** Agentbrain `document_id:495` was read completely: source URI `https://vercel.com/design/guidelines`, saved metadata updated `2026-07-20`, content hash `71605e2eeef1ccb86301504d56b6231c9234fde618ada96234dd080cc3fcc935`. Search hits included chunks `7624` and `7625`; retrieval used the whole document. Its **Vercel-specific** section explicitly labels brand choices non-universal. It is different from `https://vercel.com/design.md`, the branded report guidance discussed in the consolidated visual guide. The saved web text also contains tension between a viewport maximum-scale suggestion and “Never disable browser zoom,” illustrating why archived material is not unquestionable current authority. [Saved source URI][websource]; [Visual, “Sources and editorial scope”][visual]

### Inferences

#### Proposed compact doctrine in the router

Carry approximately these seven obligations in the entrypoint; put elaboration behind references:

1. Establish the person's job, target medium, real material, and accepted constraints.
2. Make the primary relationship/action unmistakable; explain why the direction belongs to the subject.
3. Tell the truth about state and consequences; preserve continuity and recovery.
4. Adapt to the actual medium, input paths, and accessibility needs.
5. Compare meaningful alternatives only when a consequential choice remains.
6. Make the smallest coherent change or experiment that resolves the question.
7. Inspect actual-target evidence and report its limits; distinguish preview, accepted choice, and adoption.

These are a proposed distillation of the three guides, not a verbatim new mandate. Their value is directing decisions; they should not become a mandatory seven-heading report for a one-button fix.

#### Source precedence for design decisions

Within the governing instruction hierarchy, use the user's current task and valid project-specific contracts to define scope; use the consolidated three for general judgment; use current target/platform contracts and existing project conventions for mechanics; use case studies as examples; use superseded source files only for provenance or an explicitly requested historical language. If project precedent still requires a retired house design, describe the conflict and preserve intentional product constraints rather than silently deleting them.

Do not perform a fresh full-vault search or reread the three complete guides on every `/design` invocation. The skill should be authored from them into small self-contained working references. Research/update requests can reopen the sources; ordinary design should consume the distilled knowledge.

### Gaps

- The three guides contain substantial cross-platform judgment but are not a comprehensive Android, iOS, Windows, Linux, or command-line interaction standard. Platform conventions and quantitative accessibility requirements need current target-specific evidence when a concrete task depends on them.
- Historical source documents and research findings were read as authored evidence; their implementation and performance claims were not revalidated against product checkouts.
- The `design-with-ai` shelf may contain useful preference-learning techniques, but its constituent documents were not read. Its README's aesthetic and pipeline claims should not be presented as independently established current policy.

## 2. What is the smallest coherent family, routing matrix, and workflow output contract?

### Takeaway

Start with **one new `/design` entrypoint**, a concise shared doctrine, conditional mode/platform references, and existing specialists. Treat explore, critique, build, repair, and system as work modes rather than five automatically exposed skills. Route by **intent × medium × actual stack × evidence need**; operating tools and component libraries solve different parts of that decision. This is a proposed architecture grounded in the playbook's proportionality and the native-discovery policy. [Process, “Reusable briefs for future skills”][process]; [Discovery policy, “Put each instruction where it belongs”][discovery]

### Cited Findings

#### Current local inventory, not the historical inventory

- The requested default-role directory contains **28 skill directories**. Its entries resolve into `/Users/arthack/.local/share/agentstart/resources/skills/<name>/`. The role manifest names the same 28 skills. The common managed list contains 29 because `chats` is excluded from the default role by `skills-exclude.json`. [Default-role manifest][rolemanifest]; [Managed list][managed]; [Role exclusion][exclude]
- Exact observed default-role names: `agentroles`, `ai-elements`, `ai-sdk`, `brain`, `build`, `collab`, `desktop`, `email`, `find-skills`, `fleet`, `hunk-review`, `maintain`, `native-sdk`, `notifications`, `notify`, `plannotator`, `plannotator-annotate`, `plannotator-last`, `plannotator-review`, `scrape`, `search`, `shadcn`, `terminal-control`, `test-audit`, `vercel-react-best-practices`, `web-design-guidelines`, `wiki`, `zen-open`. All 28 frontmatter records were inspected; specialist body reads are identified below. [Default-role manifest][rolemanifest]
- `internal-skill-inventory` is explicitly historical. It reports 36 skills in an August pack and notes that `frontend-design` was removed September 9. Its old browser/keys/sounds/Peekaboo descriptions are not current availability. Current sync code explicitly retires `board groom attention browser bus grokbot herdr hud keys sounds`. [Inventory, opening and “Complete inventory”][inventory]; [Sync script lines 64–74][sync]
- The current discovery decision rejects a second global skill advertisement list. Names/descriptions are the catalog; the body holds useful workflow knowledge; references hold specialized detail. A skill does not expand task authorization. CLI and MCP variants of the same workflow do not inherently need separate skills. [Discovery policy][discovery]; [Discovery review, “The advertisement decision,” “The skills themselves”][discoveryreview]

#### Existing specialists worth reusing

Paths in this table use the requested installed role path. They resolve to the shared resource tree; no installed files were edited.

| Skill and exact relative path beneath `/Users/arthack/.local/share/agentstart/resources/roles/default/skills/` | Actual boundary / useful route |
|---|---|
| `web-design-guidelines/SKILL.md` — full body read | Web UI code audit. Fetches `https://raw.githubusercontent.com/vercel-labs/web-interface-guidelines/main/command.md` before a review and emits terse `file:line` findings. Useful implementation/accessibility review, not a general native/TUI aesthetic authority. Its broad “review my UI” description needs platform discrimination in `/design`. [Source][webskill] |
| `shadcn/SKILL.md` — full body read | Existing or explicitly selected shadcn stack. Inspect project context, installed components, base, aliases, framework, tokens, and package manager; use component-specific docs and references. Has `user-invocable: false`, not `disable-model-invocation: true`. [Source, “Current Project Context,” “Key Fields,” “Workflow”][shadcn] |
| `ai-elements/SKILL.md` — full body read | AI chat component library on shadcn/React; describes Next.js and AI SDK prerequisites. Conditional component reference directory. Useful for an adopted AI Elements UI, not a reason to choose that stack for every AI interface. [Source, “Prerequisites,” “Available Components”][elements] |
| `ai-sdk/SKILL.md` — frontmatter only | Generation/streaming/tool/RAG behavior when implementation actually touches AI SDK. An interface about AI does not by itself require this implementation dependency. [Source frontmatter][aisdk] |
| `vercel-react-best-practices/SKILL.md` — full body read | React/Next.js performance implementation or review; 70 rules across eight categories, individual rule files available. Its bundled full `AGENTS.md` is a compiled reference, not a reason to load all rules for a static composition question. [Source, “When to Apply,” “How to Use”][react] |
| `native-sdk/SKILL.md` — full body read | Discovery stub for an actual Native SDK project. Calls `native skills get core`; default implementation requires `native-ui` + `ts-core`; `ts-services`, `automation`, `zig`, and `core --full` are conditional. Mobile embedding is explicitly experimental. Generic “native app” is not evidence of this SDK. [Source, “Start here,” “Quick orientation”][native] |
| `desktop/SKILL.md` — full body read | Agentdesk/Codex Computer Use for **native macOS** observation and operation. Observe → act once → observe; prefer purpose-built application APIs when suitable. This is verification/interaction capability, not a native design-system or cross-platform desktop implementation skill. [Source, “Enter the Computer Use session,” “Deliver evidence”][desktop] |
| `terminal-control/SKILL.md` — full body read | Real PTY visible state, input, resize, screenshots, recordings. MCP covers existing sessions; current creation is via CLI `termctrl start`. Visible screen differs from retained logs; cleanup preserves others' sessions. OpenTUI host is conditional, not a universal terminal framework. [Source, “Discover and choose a session,” “Observe, interact, verify,” “Evidence and cleanup”][terminal] |
| `plannotator`, `plannotator-annotate`, `plannotator-last`, `plannotator-review` — frontmatter only | Existing optional review surfaces. The main skill defers to specific operations; the three operation skills are explicit-only. Do not make opening a review app the default for every design question. [Main source][plannotator]; [Annotate source][annotate] |
| `hunk-review/SKILL.md` — frontmatter only | Live Hunk/code-diff review when the user has or requests that workflow. Not the default visual critique mechanism. [Source][hunk] |
| `build/SKILL.md`, `collab/SKILL.md` — frontmatter only | Both currently declare `disable-model-invocation: true`. A design mode named **build** does not authorize implicitly invoking the `/build` workflow. Preserve the session's already-selected execution contract. [Build][buildskill]; [Collab][collabskill] |

#### Two concrete overlap hazards

1. **Chat component ownership:** current shadcn prescribes `MessageScroller`, `Message`, and `Bubble`, while AI Elements supplies its own conversation/message family. Blindly loading both as generic “AI chat” experts can produce competing scroll and message ownership. Inspect the project and select its actual owner; load further component references only for missing, compatible needs. [shadcn, “Chat & Messaging”][shadcn]; [AI Elements, example and component references][elements]
2. **Generic composition recipes versus subject-specific judgment:** shadcn's examples say dashboard = sidebar + card + chart + table. The consolidated visual guide says unequal material need not occupy identical cards and the work should belong to its subject. These can coexist if the recipe is treated as library composition guidance after the design is chosen, rather than as an automatic page template. [shadcn, “Principles”][shadcn]; [Visual, “Choose a direction that belongs to the subject,” “Establish hierarchy through relationships”][visual]

### Inferences

#### Proposed minimal package shape

This is a logical architecture, not files to create in this planning pass:

```text
design/
  SKILL.md                         # small intake, doctrine, routing, finish condition
  references/
    visual-judgment.md              # from clarity-and-character; question-driven
    interaction-truth.md            # from trustworthy-and-alive
    exploration.md                  # matched alternatives, controlled previews, decisions
    critique-and-repair.md          # evidence, severity, systemic fixes, recheck
    system-and-adoption.md          # roles, patterns, accepted snapshots, migration
    platforms/
      web.md
      mobile.md
      desktop.md
      cli.md
      tui.md
```

Keep provenance/evaluation maintenance records outside this runtime directory if the installer copies whole directories. The exact file split should be adjusted to prevent tiny one-paragraph fragments or repeated rules. A mode normally needs **one relevant mode reference and one target reference**; dynamic/expressive work may also need the interaction reference. The core can carry enough visual judgment for small tasks without loading another document.

Reasons for one new skill initially:

- The modes share the same brief, truth model, critique ordering, medium translation, and evidence boundary. Splitting now repeats these and increases catalog competition.
- Platform differences are meaningful but mostly reference/check-selection differences; implementation specialists already have their own entrypoints.
- Five modes × five platforms should not become 25 skills or a mandatory traversal graph.
- A dedicated new leaf is justified later when it owns a distinct repeatedly used workflow, has substantial reusable knowledge, or needs an independent invocation boundary. `/design` should not be reduced to a forwarding table with no design judgment of its own.

#### Proposed intake and routing algorithm

1. Read the user's request and available project evidence. Determine **mode**, **surface(s)**, **existing stack/design language**, **primary job**, **accepted axes**, **deliverable**, and **verification access**. Read applicable repository instructions before code exploration.
2. Infer routine facts from the project. Ask only for a material unresolved decision; avoid a compulsory questionnaire about platform, audience, palette, and fonts when the brief/tree already settles them.
3. State a compact working brief if useful: “For [person/context], improve [job] by resolving [question], preserve [accepted decisions], judge on [actual target/evidence].”
4. Load the mode and platform references that answer the identified question. Add an implementation specialist only after stack/task evidence warrants it. Add an operation/verification specialist only when using that capability.
5. Carry one conceptual route ledger in working context: selected mode/target; already-loaded skills; selected references; why the next load is needed. It need not be a file or verbose user-facing log.
6. Keep `/design` as the integrator. Specialists return implementation/evidence to the chosen work mode; they do not restart intake or route back through `/design`. If no specialist exists, continue using the relevant target reference and project docs, name a concrete gap, and avoid automatic skill installation.
7. Finish in the mode's output contract with observed evidence and any unresolved choice. Stop when the user's question or requested change is resolved, not when every possible checklist has been exhausted.

This prevents routing loops by establishing one decision owner and a directed flow: **design intake → selected knowledge → selected implementation/observation → same design task completion**. Avoid runtime recursion between generic workflow skills.

#### Proposed cross-platform routing matrix

| Target | Design questions and medium-specific checks | Conditional implementation routes | Verification and evidence |
|---|---|---|---|
| **Web** | Content hierarchy, semantic controls, links/history, forms, responsive composition, keyboard/focus, browser zoom, loading/error states, screen-reader semantics | Existing framework first. `shadcn` only for shadcn context/explicit choice; `ai-elements` for chosen AI Elements composites; `ai-sdk` for actual AI SDK behavior; `vercel-react-best-practices` for React/Next implementation/review. `web-design-guidelines` for web code audit | Available browser tool and its actual skill/runbook; DOM/accessibility plus screenshots and interaction. Check representative sizes and keyboard task. A fetched code-audit checklist cannot replace rendered judgment |
| **Mobile web** | Web semantics plus touch/occlusion, viewport/keyboard changes, safe areas, physical orientation, zoom and long text | Web stack routes; do not infer a native app from phone dimensions | Browser/device emulation for bounded claims; real device when keyboard, safe-area, gesture, performance, or orientation behavior is decisive |
| **Native mobile** | Platform navigation/back, touch reach/occlusion, text scaling, keyboard, lifecycle/backgrounding, cancellation, system insets, permission versus activity, platform assistive behavior | Existing Android/iOS/React Native/Flutter/etc. project and current platform docs. No matching general mobile implementation skill observed. Do not route to Native SDK merely because the target is native | Project/device/emulator tooling actually available. State exact device/build and coverage; do not substitute a desktop browser mock for mobile gesture proof |
| **Native desktop** | Window/content geometry, first-click and focus behavior, shortcuts and modifiers, IME/text composition, menus, drag/resize, scroll momentum, persistence and attention | Existing toolkit. `native-sdk` only when the tree or request establishes Native SDK; use its conditional subskills. Do not infer React or Zig from “desktop” | Native SDK `automation` for SDK app verification; `desktop`/Agentdesk for macOS real-window observation when needed. Windows/Linux require their available native route, not an assertion that Agentdesk covers them |
| **Hybrid/WebView desktop** | Native window/input/lifecycle contract plus web surface semantics. Identify which owner controls each behavior | Existing shell toolkit + relevant web implementation specialist; SDK only when used | Verify both web content and actual native shell for first-click, IME, focus, window sizing, packaged assets, and scroll behavior |
| **CLI** | Command/argument vocabulary, help discoverability, human-readable ordering, success/failure/recovery messages, stdout/stderr meaning, exit behavior, piping, machine formats, non-TTY use, no-color readability | Existing command contract/parser; no observed general CLI-design skill. A prose/output design problem need not load a TUI or browser specialist | Noninteractive invocations and captured output/exit behavior via shell; PTY only for interactive prompts/progress. Preserve script-facing contracts. A screenshot does not prove pipe compatibility |
| **TUI** | Cell dimensions, Unicode/grapheme width and fallback, keyboard focus and modal ownership, discoverability, state semantics, stable refresh, resize/shallow height, scrolling, interrupt and terminal restoration | Existing framework (OpenTUI/Textual/Ratatui/etc.) and project conventions. Read the TUI reference; do not choose OpenTUI, Signal Room, or an unadvertised Ctrl+K by default | `terminal-control` in a real PTY, current visible screen and input, narrow/wide/shallow dimensions, real glyph rendering, keyboard-only flow, supported pointer behavior, exit restoration; plain/no-color snapshot if promised |

The CLI row adds proposed engineering coverage beyond the primary guides; it should be validated against each command's real contract. It is intentionally distinct from full-screen TUI behavior. Platform terms identify user-facing surfaces, not JavaScript framework choices.

#### Output contracts for the five modes

| Mode | Triggering intent | Minimum useful output | Proportionate evidence / completion boundary |
|---|---|---|---|
| **Explore** | A consequential direction or behavior remains unresolved | One question; preserved axes; baseline plus 1–2 genuinely different alternatives; representative scenarios; perceptible tradeoffs; recommendation or honest Tie/Neither/Uncertain | Comparable previews at sufficient fidelity; actual target for consequential behavior. Record which choice was accepted and why. Do not build a remote studio for a static hierarchy choice |
| **Critique** | Assess an existing interface, screenshot, flow, or implementation | Short prioritized findings: **observed issue → affected task/person → evidence/location → correction → verification needed**. Separate defect from preference and uncertainty | Task → composition → interaction → type/rhythm → expression → adaptation → finish. With screenshots only, state what cannot be established. Critique alone does not authorize code changes |
| **Build** | Implement a new interface or an accepted direction | Brief/design commitments, state and interaction model appropriate to scope, implemented coherent slice, actual-target proof, adoption status | Reuse current stack and components. Check representative non-happy paths and task completion. “Preview works” and “shipping product uses it” are separate facts. Do not silently invoke the explicit `/build` workflow |
| **Repair** | Specific friction/defect with accepted design to preserve | Reproduction, likely systemic cause, bounded correction, before/after evidence, regression-sensitive behavior preserved | One failure-boundary check plus relevant constrained states. Avoid an unrelated redesign or a ceremonial alternatives exercise |
| **System** | Establish/consolidate a reusable language across surfaces/components | Inventory of existing patterns; semantic token roles; component/state/input contracts; platform mappings; representative examples; migration/adoption rule and ownership | Validate at least distinct representative contexts before declaring universality. Semantic consistency can coexist with different platform geometry and controls. A giant component catalog is not the default deliverable |

Cross-platform work should produce a shared semantic brief plus per-platform render/input/evidence mappings. For example, “preserve current selection during refresh” can be shared; browser Back behavior, native window activation, and terminal modal keyboard ownership remain separate mechanisms.

#### Controls against generic glossy work and needless loading

- Require an organizing idea tied to real content, not “premium,” “modern,” or “beautiful” as the only rationale.
- Treat existing design-system components as useful material, not a substitute for information architecture. Reuse a quiet form where it suits the task; do not force novelty.
- Preserve approved composition during repairs. A request to fix a cramped label should not trigger typography replacement, new theme, new library, and hero artwork.
- Permit deliberate gradients, glow, sound, and expressiveness where they explain or characterize the working object. Evaluate their function rather than encoding aesthetic bans.
- Keep discovery and dependencies separate: knowing a skill exists does not mean its body is needed. Loading a component skill does not authorize installing its library.
- Do not copy whole upstream skills into the new family. Refer to existing owners, and distill only local cross-platform judgment that those owners do not provide.
- Browser choice is capability-discovered. The installed role has no `browser` skill even though current `desktop` text refers to one; the wider harness may offer another browser integration. Do not hard-code a nonexistent skill ID or silently resurrect the retired browser owner.

### Gaps

- No installed general-purpose Android/iOS design, CLI design, TUI design-system, or universal desktop design skill was found in the 28-entry default role. This is an inventory observation, not proof that no such skill exists elsewhere.
- Browser tools available to a particular harness may differ from role-distributed skill files. The architecture must tolerate capability availability independently of names in the historical inventory.
- The proposed family size is an architecture recommendation, not an evaluated optimum. Split only when usage/evidence shows a distinct leaf earns its metadata and maintenance cost.
- The current shadcn/AI Elements overlap warrants an explicit project-owner selection rule; integration compatibility was not tested in an application.

## 3. What provenance, evolution, distribution decisions, and evaluation cases should accompany the family?

### Takeaway

Keep provenance and evaluation as authoring infrastructure, separate from ordinary runtime context. Record the rule-to-source mapping, deliberate exclusions, source revisions, and concrete failure cases that justify future change. Installation ownership is unresolved: the existing AgentStart scan discovers `~/code/agent*/skills/*`, so the new `~/code/skills` repository does not automatically participate. [Sync script lines 45–66, 113–159][sync]; [Discovery policy, “Adding or changing a skill”][discovery]

### Cited Findings

#### Distribution and ownership evidence

- AgentStart's `AGENTS.md` and `CONTEXT.md` were read. They assign toolchain convergence to AgentStart, general reusable doctrine to AgentGuidance, and self-contained tool skills to their owners. The sync path is unattended-safe and runs every six hours; skill directories are copied whole. This was a read-only investigation, so no sync/install command was run. [AgentStart guidance, “Fix-forward installation,” “Skills”][startagents]; [Context, “The sync path,” “Participant”][startcontext]; [Sync lines 147–170][sync]
- `tool-advertisement-policy` says to author a skill with its owning tool or in AgentGuidance for reusable general doctrine/ownerless third-party workflows, preserving one installer path and invocation-policy owner. A new standalone skills repository therefore needs an explicit source/distribution decision; it should not be “installed” by hand-editing generated role resources. [Discovery, “Adding or changing a skill”][discovery]
- The portable invocation policy is `disable-model-invocation` in frontmatter; AgentStart derives Codex's inverse representation. Description discoverability and explicit-only workflow policy are separate decisions. [Context, “Model invocation policy”][startcontext]; [Discovery policy][discovery]
- Current local third-party origins are recorded in `/Users/arthack/.local/share/agentstart/resources/skills-state/skills/.skill-lock.json`. Relevant entries last updated September 28 include `shadcn/ui` (`skills/shadcn/SKILL.md`), `vercel/ai-elements`, `vercel/ai`, `vercel-labs/native`, `vercel-labs/agent-skills`, and `anomalyco/terminal-control`; Plannotator is pinned to `v0.27.9`. The lock's folder hashes describe installed source folders, not necessarily Git commit IDs. [Skill lock][lock]
- Installed Terminal Control has an AgentStart-owned body marker referring to `config/terminal-control/skill-body.md`, so the upstream lock alone is insufficient to reconstruct the exact installed instructions. Native SDK is itself a discovery stub that delegates to version-matched CLI content. Provenance must distinguish upstream source, local adaptation, and runtime-discovered reference. [Terminal entrypoint][terminal]; [Native entrypoint][native]
- The document-placement policy routes by reader and lifetime. Repository instructions and reusable doctrine belong to their maintained owners; wiki is curated human-findable authored knowledge, not live inventory/session state. Therefore routine design runs need not publish new wiki pages or duplicate the corpus. [Placement, “The routing table,” “The wiki is the operator's library,” “Memory routes by audience”][placement]
- The skill-creator instructions were loaded for this architecture work. Their **Progressive Disclosure**, **Improving the skill**, and **Description Optimization** sections support conditional references, generalization from feedback rather than overfitting, realistic trigger/near-miss cases, and qualitative judgment where assertions would be artificial. No skill draft, evaluation execution, or installation occurred. [Skill Creator source][creator]

#### Exact additional authored documents read completely

Besides the three primary sources listed in §1, the following eight wiki documents were read completely:

| Exact slug | Exact source path | Important use |
|---|---|---|
| `arthack-tui-design-language-signal-room` | `/Users/arthack/wiki/arthack-tui-design-language-signal-room.md` | Tombstoned historical design language; terminal craft versus excluded house rules. [Source][signal] |
| `fleet-tui-design` | `/Users/arthack/wiki/fleet-tui-design.md` | Tombstoned shell/input contract; historical shortcut and framework scope. [Source][tui] |
| `internal-skill-inventory` | `/Users/arthack/wiki/internal-skill-inventory.md` | Historical inventory, frontend-design removal, old projection claims. [Source][inventory] |
| `core-guidance-and-skill-discovery-review-september-2026` | `/Users/arthack/wiki/core-guidance-and-skill-discovery-review-september-2026.md` | Native discovery, duplication, selective grooming, preserving authorization. [Source][discoveryreview] |
| `tool-advertisement-policy` | `/Users/arthack/wiki/tool-advertisement-policy.md` | Current catalog/body/reference/owner boundaries. [Source][discovery] |
| `document-placement-policy` | `/Users/arthack/wiki/document-placement-policy.md` | Reader/lifetime/owner of authored design knowledge and instructions. [Source][placement] |
| `agentvoice-reactive-terminal-signal-field-research` | `/Users/arthack/wiki/agentvoice-reactive-terminal-signal-field-research.md` | Honest signal mapping, glyph craft, controlled real-renderer case study. [Source][field] |
| `agent-swarm-sonification-findings` | `/Users/arthack/wiki/agent-swarm-sonification-findings.md` | Evidence-driven correction, sensory budgets, limitations of demonstrations. [Source][sound] |

Other design documents were discovered by search but not read in full: `agentvoice-android-the-voice-filament`, `agentvoice-live-and-design-mode-integration-plan`, `agentvoice-provisional-studio-defaults`, `agentlab-slice-1-historical-example-workbench`, `agentlab-slice-1-show-what-happened`, and the demo-production guides named in the primary playbook. They are candidate case studies, not additional evidence claimed by this report. [Primary guides' “Sources and editorial scope”][process]; [Visual editorial scope][visual]; [Interaction editorial scope][interaction]

#### Primary-source fingerprints

SHA-256 of complete local Markdown bytes, including frontmatter, read September 29. These bind this research snapshot; future edits should be intentionally compared rather than assumed equivalent. [Source files][visual] [and][interaction] [playbook][process]

```text
designing-interfaces-with-clarity-and-character.md
6c0fb842bd0d81cf63c3765b92f4d7000e38d81215d87e5bf7bac9b767df1180

designing-interactions-that-feel-trustworthy-and-alive.md
60da2e46c91af204fe1bfffed8988d26366c405c2f0fe35cea877286a69b6728

a-practical-design-exploration-and-critique-playbook.md
02c972a6b81d48c104cce2fb8bd1b17b2951504dc64f6601dbb7027802a2b124
```

### Inferences

#### Proposed non-runtime maintenance records

Keep these in the owning repository's authoring/research area, outside the installable `design/` tree where practical:

- **Source ledger:** source slug/path/URL; observed date; exact hash or version; status (consolidated, current contract, historical/tombstoned, product example, external saved snapshot); sections used; intended scope.
- **Rule map:** distilled rule → source section → target reference → exclusions/translation. Example: “preserve committed view on refresh” maps to the interaction guide, while “never show REFRESHING anywhere” is explicitly rejected as an old local overreach.
- **Routing decisions:** each skill's trigger, excluded near-misses, capability fallback, overlap owner, source path, invocation policy, and last-observed availability. Keep this focused on design routes rather than recreating a global skill catalog.
- **Change log:** observed design failure or user correction, generalized lesson, examples where it applies/does not, proposed scope, evidence, and approval/adoption status. One project preference must not silently become universal doctrine.
- **Evaluation case set and human rubric:** realistic tasks, source fixtures, expected route/output, evidence requirements, and known failure patterns. Record baseline/with-skill differences when evaluation is actually run, not invented scores.

Do not require these records to load on ordinary design tasks. A compact provenance pointer is sufficient; maintainers can open the ledger deliberately.

#### Evolution triggers

Revise only when a concrete condition warrants it:

1. The human repeats a correction across independent contexts; distinguish a local preference from a general defect before promotion.
2. An evaluation reveals wrong-medium routing, a route loop, redundant loads, stack invention, or inappropriate authorization expansion.
3. A specialist changes APIs, component ownership, invocation policy, or availability (especially chat ownership, Native SDK subskills, and browser operation routes).
4. A primary guide is revised/superseded, or an example is discovered to contradict current source evidence.
5. Actual target use reveals accessibility, cancellation, state-truth, continuity, or responsiveness failures not caught by current guidance.
6. Repeated mode-specific work grows substantial enough to earn a separately discoverable skill. Measure usefulness and load burden, not the number of skills produced.

The default response is a bounded rule/reference adjustment plus relevant cases, not an automatic global redesign, nightly self-rewrite, or forced adoption of newly fetched taste guidance.

#### Proposed evaluation cases (planning only)

These are proposed scenarios, not executed tests or measured results. Evaluate route correctness, final usefulness, scope preservation, medium-specific craft, evidence honesty, and load economy. Use qualitative review for design quality; reserve deterministic checks for concrete routing and artifact facts.

| Case / realistic prompt | Expected route and substantive success | Failure to expose |
|---|---|---|
| **Ambiguous improvement, existing web app:** “This incident queue feels busy. Make the important work easier to find; keep our components.” | Infer repair/critique from code/task; distinguish quantity from competing emphasis; improve blocked-work priority; preserve stack and accepted components | Generic hero/cards/gradient reskin; ask a long style questionnaire; replace component library |
| **Small accepted-axis repair:** “The composition is right. Fix these clipped labels at narrow widths.” | Repair + target reference; preserve composition; reflow, wrap, or meaningful disclosure; verify long labels at constrained size | Force multiple redesign alternatives; change typography/theme wholesale |
| **Static screenshot critique:** “Critique this onboarding screen, don't edit yet.” | Critique, ranked task/composition findings, screenshot evidence limits, proposed corrections | Claims keyboard/screen-reader/gesture behavior was verified; unrequested implementation |
| **Native Android hold control:** “Fix push-to-talk sticking when I switch apps.” | Native mobile repair + gesture/lifecycle state model; verify background/focus loss, release, cancellation, late acknowledgements on actual available target | React/shadcn migration; mobile browser mock used as proof; visual-only fix |
| **Native macOS attention panel:** “The notification looks fine but the first click sometimes opens a different item.” | Interaction truth/identity binding + macOS actual-window inspection; reproduce arrival between down/up; preserve focus | Treat as styling defect; accept API success as rendered/input proof |
| **CLI output contract:** “Make `jobs list` readable for people without breaking scripts.” | CLI reference; inspect existing contracts; human output hierarchy, piping/no-color, machine format and exit compatibility | Full-screen TUI or browser implementation; decorative ANSI in machine output; undocumented breaking flags |
| **TUI resize:** “This Ratatui dashboard breaks at 48 columns and hides the recovery action.” | TUI reference + terminal-control when operating; preserve framework; define compression priorities; verify keyboard, narrow and shallow layouts, real glyphs | Assume OpenTUI; impose Signal Room palette, no headers, or Ctrl+K; copy CSS media queries conceptually |
| **Native SDK context:** “Add a settings panel to this app.json / .native / core.ts project.” | Native SDK stub → core + native-ui + ts-core; services/automation only when needed; actual platform proof | Infer Zig from toolkit implementation; load every CLI subskill or rewrite as web UI |
| **Non-React web:** “Improve this server-rendered Django form and audit accessibility.” | Web reference + web-design-guidelines for code audit, existing template stack, browser interaction evidence | Load React performance, AI Elements, or initialize Next/shadcn without evidence |
| **AI chat overlap:** “Improve streaming follow in this existing shadcn MessageScroller chat.” | Inspect actual owner, use shadcn chat guidance; preserve reading position and opt-in follow; load AI SDK only for affected streaming implementation | Add a second AI Elements conversation wrapper/scroll owner merely because it is AI chat |
| **Honest expressive instrument:** “Make the two amplitude meters more expressive, but we only expose volume envelopes.” | Explore + interaction/TUI or native target reference; explicit derivations and declared idle motion; matched scenarios | Claim sentiment, thought, pitch, spectrum, or progress from unmeasured signals; ban all expression |
| **Small versus large exploration:** “Compare compact and persistent details for this editor.” | Baseline + 1–2 structural alternatives at sufficient fidelity; common content and state, tradeoffs | Twelve color variants; build a remote control studio before knowing it is needed |
| **Cross-platform system:** “Give the same job-monitoring concept a phone, desktop and terminal surface.” | Shared state/meaning vocabulary with per-target geometry/input contracts and evidence plan | Shrink desktop screenshot for phone; copy card/hover mechanics into terminal; shared aesthetic overrides usability |
| **Failed save after successful generation:** “Retry saving should not run the expensive operation again.” | Repair at persistence boundary; preserve generated result and newer live edits; represent saved/reviewed separately | Retry whole operation; label acknowledgement “saved”; overwrite later draft |
| **Provenance trap:** “Use our old Fleet TUI design guide.” | Recognize tombstone; clarify whether historical house language is actually intended; use current project constraints and named scope | Treat missing CLI result as no knowledge; resurrect old mandates as current universal policy |
| **Unavailable specialist:** “Design an iOS settings flow here.” | Mobile design reference and existing project/platform evidence; identify verification/tool gap without blocking useful design work | Claim installed iOS skill; auto-install a pack; route to experimental Native SDK mobile |
| **Near-miss negatives:** “Design a database schema”; “Which model should our request router use?” | No interface-design routing merely because of “design”; handle underlying architecture task | Overbroad description recruits unrelated system architecture into visual workflow |
| **Explicit workflow boundary:** “Design and implement the new filter bar” in an ordinary session | Design build mode, normal authorization, appropriate specialists | Auto-invoke explicit-only `/build` or `/collab`; require unrelated approval ceremonies |

For a first bounded evaluation round, choose five discriminating cases: non-React web, native mobile cancellation, CLI piping, TUI narrow layout, and small accepted-axis repair. Add the AI-chat overlap and screenshot-evidence case next. This samples genuinely different failure modes rather than repeatedly scoring attractive landing pages.

#### Recommended decisions for the coordinator

1. Adopt the consolidated three as the general doctrine baseline; retain old TUI sources and the design-with-ai shelf as provenance/case material only.
2. Begin with a single `/design` skill plus lazy references and existing specialists; avoid new platform wrappers that only restate existing instructions.
3. Make current project/stack detection precede framework-specialist selection.
4. Define mode-specific completion and evidence boundaries before drafting skill prose.
5. Decide authoritative source ownership and AgentStart distribution explicitly in a later implementation brief. The present repo can hold planning/source work, but its name does not match the existing automatic scan.
6. Keep runtime self-contained and portable; use non-runtime source ledgers and evaluation cases for provenance/evolution rather than making every design request re-research the vault.

### Gaps

- No installer change, owner transfer, frontend-design revival, or source-placement exception has been approved by this research. A future implementation brief must resolve whether the new repository becomes an explicitly managed external source or the reusable doctrine is authored through the existing owner.
- No new `SKILL.md`, specialist references, tests, preview, or deployment was produced. The proposed cases are unexecuted; no claimed success rate or token saving exists.
- Native browser/desktop/mobile verification capabilities vary by harness and device. The skill cannot promise proof it cannot collect; evaluation needs representative real environments.
- Full historical Vercel-native and design-studio originals were not read; the current consolidated guides explicitly describe their editorial replacement and were read fully. The old TUI originals were read because terminal-specific retirement details materially affect routing.

[visual]: /Users/arthack/wiki/designing-interfaces-with-clarity-and-character.md
[interaction]: /Users/arthack/wiki/designing-interactions-that-feel-trustworthy-and-alive.md
[process]: /Users/arthack/wiki/a-practical-design-exploration-and-critique-playbook.md
[signal]: /Users/arthack/wiki/arthack-tui-design-language-signal-room.md
[tui]: /Users/arthack/wiki/fleet-tui-design.md
[inventory]: /Users/arthack/wiki/internal-skill-inventory.md
[discoveryreview]: /Users/arthack/wiki/core-guidance-and-skill-discovery-review-september-2026.md
[discovery]: /Users/arthack/wiki/tool-advertisement-policy.md
[placement]: /Users/arthack/wiki/document-placement-policy.md
[field]: /Users/arthack/wiki/agentvoice-reactive-terminal-signal-field-research.md
[sound]: /Users/arthack/wiki/agent-swarm-sonification-findings.md
[resource]: /Users/arthack/resources/design-with-ai/README.md
[websource]: https://vercel.com/design/guidelines
[rolemanifest]: /Users/arthack/.local/share/agentstart/resources/roles/default/.agentstart-role.json
[managed]: /Users/arthack/.local/share/agentstart/resources/managed-skills.txt
[exclude]: /Users/arthack/code/agentstart/roles/default/skills-exclude.json
[sync]: /Users/arthack/code/agentstart/scripts/sync-skills
[startagents]: /Users/arthack/code/agentstart/AGENTS.md
[startcontext]: /Users/arthack/code/agentstart/CONTEXT.md
[lock]: /Users/arthack/.local/share/agentstart/resources/skills-state/skills/.skill-lock.json
[webskill]: /Users/arthack/.local/share/agentstart/resources/roles/default/skills/web-design-guidelines/SKILL.md
[shadcn]: /Users/arthack/.local/share/agentstart/resources/roles/default/skills/shadcn/SKILL.md
[elements]: /Users/arthack/.local/share/agentstart/resources/roles/default/skills/ai-elements/SKILL.md
[aisdk]: /Users/arthack/.local/share/agentstart/resources/roles/default/skills/ai-sdk/SKILL.md
[react]: /Users/arthack/.local/share/agentstart/resources/roles/default/skills/vercel-react-best-practices/SKILL.md
[native]: /Users/arthack/.local/share/agentstart/resources/roles/default/skills/native-sdk/SKILL.md
[desktop]: /Users/arthack/.local/share/agentstart/resources/roles/default/skills/desktop/SKILL.md
[terminal]: /Users/arthack/.local/share/agentstart/resources/roles/default/skills/terminal-control/SKILL.md
[plannotator]: /Users/arthack/.local/share/agentstart/resources/roles/default/skills/plannotator/SKILL.md
[annotate]: /Users/arthack/.local/share/agentstart/resources/roles/default/skills/plannotator-annotate/SKILL.md
[hunk]: /Users/arthack/.local/share/agentstart/resources/roles/default/skills/hunk-review/SKILL.md
[buildskill]: /Users/arthack/.local/share/agentstart/resources/roles/default/skills/build/SKILL.md
[collabskill]: /Users/arthack/.local/share/agentstart/resources/roles/default/skills/collab/SKILL.md
[creator]: /Users/arthack/.claude/skills/synced/29fe6327-b074-4ebe-abdd-91081b59d6e2_3a79806f-7570-469c-ba5e-128c3e68050e/skill-creator/SKILL.md
