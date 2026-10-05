---
name: design-components
description: >-
  Discover and select reusable UI components, blocks, and patterns that fit the
  actual project. Use when finding a component, comparing libraries, composing
  an interface from existing parts, or searching shadcn registries. Starts with
  local components and official shadcn for compatible projects, then broadens
  to vetted registries, Shoogle, and primary sources for a specific gap.
---

# Components that fit the job

Start with the required behavior and actual application directory, not a
catalog screenshot. Inspect the framework, package manager, primitive base,
tokens, aliases, current components/local edits, and design commitments. If
invoked alone, infer these from the task/project; ask only about an unresolved
choice with meaningful consequences.

Define the need as **task + content + states + input + constraints**. “Filter a
large incident queue while preserving URL state” is more useful than “beautiful
dropdown.” Distinguish a primitive, composite, whole block, and application
runtime; their adoption cost differs.

## Search in order, with a stopping condition

1. **Existing project.** Reuse installed components and accepted patterns.
   Prefer a small composition over replacing the system for a nicer demo.
2. **Official library.** For an established/selected shadcn project, explicitly
   use registry `@shadcn`. Inspect primitives and blocks separately. For native,
   Vue, server templates, or terminal frameworks, use their actual toolkit's
   components first; do not add React to satisfy this route.
3. **Configured/vetted sources.** Expand only after naming what the official
   option lacks: virtualization, a specific interaction, or an appropriate
   composition. A visual mismatch may need adaptation, not another dependency.
4. **Bounded discovery.** Use Shoogle, current directory/search, saved knowledge,
   or a relevant awesome list to find one or two promising sources. Inspect
   their upstreams and exact items before selecting.
5. **Stop at a credible fit.** Usually 5–10 search results and at most three
   inspected candidates are enough. Compare with composing existing parts.
   Do not enumerate registries after the requirement is satisfied.

Read [shadcn discovery and execution](references/shadcn.md) for its MCP/CLI
workflow. Read [discovery sources](references/discovery.md) only when broadening
the search or finding a missing skill/tool. Use the available `shadcn` skill
for version-matched implementation guidance, resolved by its actual catalog
identifier. Pass the explicit registry and app path so it need not guess.

## Inspect before selecting

Use full source/payload and current component docs, not only metadata or an
example. Compare these dimensions with **fits / needs adaptation / unknown /
fails**, supported by evidence rather than a synthetic confidence score:

- **Task and visual fit:** relevant content, state completeness, mobile/desktop
  behavior, hierarchy, and how much of a block would be discarded.
- **Compatibility:** framework/version, Base UI versus Radix/Aria APIs,
  rendering/client boundaries, Tailwind/tokens, aliases, icons, CSS ownership,
  package manager, and existing local edits.
- **Accessibility:** names/roles, keyboard/focus, overlay behavior, labels,
  non-color state, reduced motion. Library provenance does not certify a composition.
- **Cost:** dependency closure, runtime/client weight, large-data behavior,
  file/route targets, and adaptation complexity. Label unmeasured performance.
- **Provenance:** exact item/repository/ref, current docs, maintenance evidence,
  code/asset license and attribution. Popularity or directory inclusion is a lead.

Return a compact shortlist with source, key gain/cost, required changes, unknowns,
and a recommendation. For one obvious existing fit, one candidate is enough.

## Adopt within the requested work

A request to find or compare components ends with selection; a build/add request
normally includes the scoped installation and adaptation it needs. Preserve
project policy and local modifications. Inspect dry-run/diff and dependency/file
targets, then use the project's package runner and correct application cwd.
Review generated imports, tokens, icons, accessibility, and route placement.
Do not install an entire example page where only one control is needed.

Choose one owner for complex behavior. A chat scroller, editor runtime, or data
grid is not interchangeable decoration. Preserve existing ownership and avoid
stacking a second conversation/scroll manager merely because both libraries
advertise AI chat.

Run the relevant project checks and actual-target task, including material
loading/empty/error/input/constrained states. Report what was discovered,
selected, installed, adapted, and verified accurately. The result should solve
the requirement in this app; catalog search success is only the first step.
