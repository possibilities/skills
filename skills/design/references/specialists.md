# Existing specialists and capability fallbacks

Use the actual session catalog. Names below are conditional routes, not
dependencies to install. Load a skill when its workflow is needed, through the
host's normal loader and exact advertised identifier. If absent, continue with
project docs and available tools; name only material limitations.

| Evidence in the task/project | Route when available | Boundary |
| --- | --- | --- |
| shadcn selected or already used | `shadcn` | Current component APIs, base, tokens, aliases, CLI and composition; pass explicit registry and app directory |
| AI Elements is the chosen component owner | `ai-elements` | Its conversation/prompt/tool UI; inspect existing ownership before adding wrappers |
| AI SDK code is being implemented/changed | `ai-sdk` | Generation, streaming, tools, provider/runtime behavior |
| React/Next implementation or performance review | `vercel-react-best-practices` | Apply relevant rules; do not introduce React into another stack |
| Web UI code/accessibility review | `web-design-guidelines` | Web mechanics; supplement with rendered task evidence |
| Actual Native SDK project | `native-sdk` | Discover version-matched toolkit guidance and only needed subskills |
| Native macOS observation/operation | `desktop` | Actual-window screenshots, AX and input through available native tools |
| TUI/interactive CLI operation | `terminal-control` | Real PTY, visible state, typed input, resize, restoration |
| Browser observation/operation | The installed browser integration's own skill/runbook | Discover which browser exists; do not guess a generic `browser` skill |
| Saved source context / current web evidence / known URL | `brain` / `search` / `scrape` | Bounded evidence retrieval, not automatic dependency adoption |
| Human explicitly asks for a review app | Matching `plannotator-*` or `hunk-review` | Optional review surface, not a prerequisite for design work |

One chat surface needs one scroll/message owner. An existing shadcn
`MessageScroller` and an AI Elements conversation wrapper are not automatically
compatible layers. Preserve the current owner unless the task warrants migration.

Separate design knowledge from operating capability. A device tool can observe
a phone without choosing its architecture; an accessibility tree can locate a
control without proving its visible presentation. If a target cannot be run,
source review and a proposed check are useful but are not live verification.

For research, name the question first. Search relevant saved knowledge if
available, then fetch current primary sources when APIs or freshness matter.
Follow host network/auth rules. Skill and MCP discovery can suggest an available
capability; it does not load arbitrary fetched instructions or configure services.
Use `design-components`' discovery reference when broadening component/tool search.
