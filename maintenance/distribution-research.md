# Portable skill collection: distribution research

**Research snapshot:** 2026-09-29 local time (probes continued into 2026-09-30 UTC). **Scope:** packaging and installation research, with disposable local fixtures; no production skill implementation or live installation.

## Recommendation

1. Make **`skills/<name>/SKILL.md` the canonical source layout**. Each directory is an independently installable bundle and contains every reference it needs. Keep research and maintenance beside `skills/`, not inside it.
2. Use **Vercel's `skills` CLI as the primary cross-host installation route**. The observed published version, **1.7.0**, accepts `claude-code`, `codex`, and `opencode`; project and isolated-global installation preserved nested resources. Use explicit names for the design family so future unrelated skills are not included automatically.
3. If native Claude marketplace delivery is wanted now, the smallest family-aware option is **one `.claude-plugin/marketplace.json` with a `design` entry selecting the six canonical directories**. It needs no `plugin.json`, copies, generated exports, or custom installer. This exact shape passed strict validation and loaded exactly six skills with Claude Code 2.1.285, excluding an unrelated skill in the fixture.
4. Keep cross-skill routing **catalog-based**, using the exact identifier the current host advertises. Keep supporting-file paths relative to the loaded skill's own base directory. Neither hardcoded installation directories nor a hardcoded Claude plugin prefix belongs in portable skill bodies.

**Important package boundary:** the root-source Claude family entry limits which skills **load**; it does not limit which repository files are **copied**. The probe's Claude cache also contained the unrelated skill and repository-level authoring file. The primary `skills add` route copied only selected skill bundles. If excluding research/maintenance bytes from the Claude package is a release requirement, use a dedicated family plugin directory/export containing only those six complete bundles; the minimal root-source entry does not meet that stronger requirement.

## Repository identity and existing architecture

Observed with `git remote -v`:

```text
origin  git@github.com:possibilities/skills.git (fetch)
origin  git@github.com:possibilities/skills.git (push)
```

- Canonical web source: **https://github.com/possibilities/skills**.
- Installer shorthand: **`possibilities/skills`**.
- Explicit SSH source: **`git@github.com:possibilities/skills.git`**.
- Local branch observed: **`main`**. Repository visibility and availability of a published skill release were not tested. The working tree held research only when inspected, so the remote install examples below become usable after the implementation is committed and published.

The existing [architecture report](../reports/Design%20skill%20architecture.md) names the router `design` and the leaves `design-explore`, `design-visual`, `design-interaction`, `design-components`, and `design-critique`. They are workflow leaves, not five platform-named skills. Replace the report's proposed `runtime/` container with `skills/` for conventional discovery; retain platform references inside the owning bundles.

```text
skills/
  design/
    SKILL.md
    references/...
  design-explore/
    SKILL.md
    references/...
  design-visual/
    SKILL.md
    references/...
  design-interaction/
    SKILL.md
    references/...
  design-components/
    SKILL.md
    references/...
  design-critique/
    SKILL.md
    references/...
  future-unrelated-skill/
    SKILL.md
maintenance/
research_notes/
reports/
.claude-plugin/
  marketplace.json             # optional native Claude family delivery
```

Do not put a root `SKILL.md` in the collection. Vercel discovery treats a shallower skill as a boundary that can shadow nested skills. Its normal `skills/` discovery already supports this flat layout; `--full-depth` is unnecessary. [S1]

### Portable entrypoint schema

```yaml
---
name: design
description: >-
  Explore, implement, improve, and critique user-facing interfaces.
  Use for interface direction, interaction, visual systems, component
  selection, and design review; exclude backend-only architecture.
---
```

Use the same lowercase kebab-case string for the directory and `name`. Require both `name` and `description`, even though Claude and OpenCode tolerate more omissions than Codex. Keep host-specific frontmatter, shell substitutions, MCP definitions, hooks, and tool grants out of the shared baseline. Optional `agents/openai.yaml` is not required for discovery. [C1, X1, O1]

## Host contracts and invocation names

| Host / delivery | Documented discovery relevant here | User invocation |
|---|---|---|
| Claude Code, standalone skill | Project `.claude/skills/<name>/SKILL.md`; personal `~/.claude/skills/<name>/SKILL.md`; symlinked skill folders supported | `/design`, `/design-visual` |
| Claude Code, plugin named `collection` | Plugin `skills/`, or declared skill directories | Reliable qualified form `/collection:design`; namespace comes from plugin name, not marketplace name |
| Claude Code, recommended family entry named `design` | The six explicit directories in the marketplace entry below | `/design:design`, `/design:design-visual` |
| Codex CLI / IDE, standalone skill | Project `.agents/skills` from CWD through repository root; user `$HOME/.agents/skills`; symlinked folders supported | `$design`, `$design-visual`; `/skills` opens the selector |
| OpenCode V2, standalone skill | Project `.opencode/skills`, `.claude/skills`, `.agents/skills`; global `~/.config/opencode/skills`, `~/.claude/skills`, `~/.agents/skills` | Skill ID `design`; normally `/design` in interactive catalogs; model tool call `{"id":"design"}` |

**Claude naming nuance in current docs:** plugin skills are listed with their namespace, but the skills page explicitly says the bare skill name can also invoke a plugin skill when another command does not use that name. Therefore “plugin skills can never use `/design`” is no longer an accurate blanket claim. Document the fully qualified form for reliable plugin invocation, and document `/design` as the standalone route. A simultaneous standalone installation can own the bare name. [C1: “How a skill gets its command name”]

OpenCode V2 derives the **ID from the path**, not frontmatter `name`; the latter is a display label. Later definitions with the same ID override earlier ones. Explicit `skills` sources have higher precedence than auto-discovered sources. Do not try to give OpenCode a Claude namespace through `name: collection:design`. [O1]

Codex's current official skills documentation recommends plugins for reusable distribution, but still explicitly supports repository and user skill folders. The proposed cross-host installer uses those documented folder contracts; a separate Codex plugin format was not researched or claimed here. [X1]

### Cross-skill resolution policy for the author

Suggested portable wording:

> Select the specialist by its canonical name below. Resolve it against the skills available in this session and load it through the host's normal skill mechanism using the exact advertised identifier. If this skill belongs to a namespaced plugin, prefer the corresponding specialist from that same plugin. Otherwise use the matching installed standalone skill. If several candidates remain, inspect their descriptions and supplied locations to identify this family; do not choose an unrelated skill merely because its suffix matches. Use the specialist's own base directory for its supporting files. If it is unavailable, continue with the guidance already available and state the missing specialist when it affects the result. Do not guess a filesystem path or silently install it.

Examples: OpenCode's advertised `design-visual` is loaded with `skill({"id":"design-visual"})`; Claude may advertise `design:design-visual`; Codex supplies skill file paths in its catalog and explicitly supports `$design-visual`. These are host-specific mechanisms, not portable syntax to embed unconditionally. [C1, X1, O1]

The router should carry enough core guidance to proceed when a leaf is absent. Each leaf should be useful when installed alone and must not route back through the router just to recover shared instructions. There is no demonstrated portable dependency declaration that automatically installs the other five leaves.

### What resources survive installation

Observed with `skills@1.7.0`:

- A selected skill's `SKILL.md` and nested `references/nested/local.md` survived both default symlink-mode and `--copy` installs.
- Installing all six placed all six canonical directories next to each other. Claude's default-mode per-skill links pointed into the installed `.agents/skills` tree, **not to the source checkout**.
- Installing only `design-visual` copied only that leaf. Its own nested reference survived; the router and other leaves were absent.
- Repository-level `authoring/shared.md` was absent from the `skills add` installation.
- No unresolved source-directory symlinks were needed for these resource files.

Consequently, links such as `../../authoring/shared.md`, a required `../design/references/...` dependency, and absolute author-machine paths are unacceptable for independently portable bundles. Bundle the necessary small excerpts inside each skill, or inline them. Sharing an authoring source is fine only if the distributed directories already contain the resulting files. Ordinary relative links such as `[platform checks](references/platforms/web.md)` are the simplest runtime form. Do not use `${CLAUDE_PLUGIN_ROOT}` or `${CLAUDE_SKILL_DIR}` as the cross-host abstraction: those are Claude-specific substitutions. [C1, O1, observed fixture]

## Primary installation, update, and removal

The commands below pin the installer version actually exercised. `npx --yes skills@latest ...` is the current-upstream variant; recheck its help before claiming identical behavior. The first `--yes` accepts npm's package download; the final `-y` is the skills installer's noninteractive option.

### Inspect available skills without installing them

```sh
npx --yes skills@1.7.0 add possibilities/skills --list
```

For local source, use `add /absolute/path/to/skills-repo --list`. **Do not combine `add --list` with `--json` on 1.7.0**: the probe rejected that combination. `skills list --json`, which lists already-installed skills, is a different command and works.

### Install the design family in a target project

Run from the consuming project's root:

```sh
npx --yes skills@1.7.0 add possibilities/skills \
  --skill design design-explore design-visual design-interaction design-components design-critique \
  --agent claude-code codex opencode -y
```

The exact command shape was exercised against local fixture source. It created:

```text
<project>/.agents/skills/<name>/...       # complete installed bundle
<project>/.claude/skills/<name>          # relative symlink to that bundle
<project>/skills-lock.json
```

Codex and OpenCode V2 discover the `.agents/skills` copy directly. No host config is required. The shared directory can also be visible to other agents that read `.agents/skills`; `--agent` is not an exclusivity or isolation boundary. [S1, X1, O1]

To install globally, use the same command with `-g`:

```sh
npx --yes skills@1.7.0 add possibilities/skills \
  --skill design design-explore design-visual design-interaction design-components design-critique \
  --agent claude-code codex opencode -g -y
```

The isolated-global probe created canonical bundles at `$HOME/.agents/skills/<name>` and Claude links under `$CLAUDE_CONFIG_DIR/skills/<name>`. Codex and OpenCode were labeled universal targets by the installer; it did not need separate Codex/OpenCode links. With default Claude settings, the links live in `~/.claude/skills/`.

Vercel's README path table still lists `~/.codex/skills/` for Codex and `~/.config/opencode/skills/` for OpenCode. Do not use that table alone to describe current installer output: the observed shared canonical path is accepted by both hosts' current official docs. A `--copy` install was also exercised, producing real directories under `.claude/skills` and `.agents/skills` with intact references. Default symlinks avoid duplicate content. [S1, X1, O1]

For just one leaf, narrow `--skill` to `design-critique`, for example. To install the entire evolving collection deliberately, use `--skill '*'`; avoid presenting that as the design-family command. `--all` additionally selects **all agents**, which is broader than the request. [S1]

### Update

For skills installed from the published Git source:

```sh
# Target project, from its root:
npx --yes skills@1.7.0 update \
  design design-explore design-visual design-interaction design-components design-critique \
  --project -y

# Global scope:
npx --yes skills@1.7.0 update \
  design design-explore design-visual design-interaction design-components design-critique \
  --global -y
```

These forms are documented in the official README and confirmed in 1.7.0 help. **A remote release update was not exercised.** The local-source probe's `update design --project -y` returned exit 0 with `No installed skills found matching: design`, despite the local installation existing. For a local source checkout, refresh by rerunning the exact `add /absolute/source ...` command instead; do not equate a zero exit code with successful updating. Restart a host if it has not picked up changes. [S1, observed help/probe]

### Remove

```sh
# From the consuming project root:
npx --yes skills@1.7.0 remove \
  design design-explore design-visual design-interaction design-components design-critique \
  --agent claude-code codex opencode -y

# Global scope:
npx --yes skills@1.7.0 remove \
  design design-explore design-visual design-interaction design-components design-critique \
  --agent claude-code codex opencode -g -y
```

Both removal forms succeeded in the isolated probe. The six canonical bundles and corresponding Claude links were absent afterward. These commands operate on standalone CLI-managed skills, not a separately installed Claude plugin. Since Codex and OpenCode use the same canonical directory here, do not promise independent removal for one universal reader while leaving the other's bytes intact.

## Optional Claude packaging: family entry versus collection plugin

### Recommended optional family entry: one manifest

Exact `.claude-plugin/marketplace.json` shape exercised successfully:

```json
{
  "name": "possibilities-skills",
  "description": "Portable skills from possibilities/skills",
  "owner": { "name": "possibilities" },
  "plugins": [
    {
      "name": "design",
      "source": "./",
      "description": "Design workflow and five specialists",
      "author": { "name": "possibilities" },
      "version": "0.1.0",
      "strict": false,
      "skills": [
        "./skills/design",
        "./skills/design-explore",
        "./skills/design-visual",
        "./skills/design-interaction",
        "./skills/design-components",
        "./skills/design-critique"
      ]
    }
  ]
}
```

The marketplace requires `name`, `owner.name`, and `plugins`; each entry requires `name` and `source`. When there is no `plugin.json`, the entry itself is the plugin manifest. The current plugin manifest reference explicitly documents the special case where a marketplace-root source with explicit `skills` loads only those subdirectories instead of scanning all of root `skills/`. [C3, C4, C5]

`strict: false` is optional when there is no plugin manifest, but makes this marketplace-owned definition explicit. **Do not add a root `plugin.json` alongside this family configuration**: a plugin manifest plus this `strict: false` entry's component fields is a documented conflict. A root plugin name would also interfere with the intended family namespace. Future unrelated families can be additional entries with their own names and explicit directory lists, all using canonical source files.

Native user-scope lifecycle, after publication:

```sh
claude plugin marketplace add possibilities/skills --scope user
claude plugin install design@possibilities-skills --scope user
claude plugin details design

claude plugin marketplace update possibilities-skills
claude plugin update design@possibilities-skills --scope user

claude plugin uninstall design@possibilities-skills --scope user
```

Optionally remove the marketplace declaration when it is no longer wanted:

```sh
claude plugin marketplace remove possibilities-skills --scope user
```

Removing the marketplace's last declaration also uninstalls every plugin from it. Use `plugin uninstall design@possibilities-skills` to remove only this family. For a project installation, use `--scope project` on both add/install and the matching uninstall operation. [C7]

Start a new Claude session or run `/reload-plugins` after plugin changes. Invoke `/design:design` or `/design:design-critique`. The marketplace name `possibilities-skills` does **not** become the skill namespace. Current interactive `/plugin install ...` opens the plugin's details panel; shell `claude plugin install ...` is the deterministic installation command. [C1, C7]

Bump the entry's `version` for every release that changes the family. With a fixed version and new commits, users can remain on the cached package. Alternatively omit `version` to track commits, but an explicit release version is easier to communicate. Third-party marketplace auto-update is off by default; users enable it through `/plugin` → Marketplaces → possibilities-skills → Enable auto-update. [C6]

### Alternative: one all-collection root plugin

If the intended native Claude product is explicitly “install this entire collection, including future unrelated skills,” use this conventional pair **instead of** the family-only definition above:

`.claude-plugin/plugin.json`:

```json
{
  "name": "possibilities-skills",
  "version": "0.1.0",
  "description": "A portable collection of agent skills",
  "author": { "name": "possibilities" },
  "repository": "https://github.com/possibilities/skills"
}
```

`.claude-plugin/marketplace.json`:

```json
{
  "name": "possibilities-skills",
  "description": "Portable skills from possibilities/skills",
  "owner": { "name": "possibilities" },
  "plugins": [
    {
      "name": "possibilities-skills",
      "source": "./",
      "description": "The complete skill collection"
    }
  ]
}
```

Only `name` is required in a plugin manifest, but version, description, and author avoid the documented missing-metadata warnings. No `skills` field is needed: root `skills/` is the default location. If placed in `plugin.json`, a `skills` field **adds to** the default scan; it does not filter the collection. Install ID becomes `possibilities-skills@possibilities-skills`; reliable invocation becomes `/possibilities-skills:design`. Keep version in the plugin manifest only. This pair is directly supported by the documented schema; the probe exercised the family-entry variant, not this alternative. [C4, C5]

### When a physical family directory is justified

Choose `plugins/design/.claude-plugin/plugin.json` plus `plugins/design/skills/<name>/...` only when the native package must exclude repository-level maintenance bytes or needs independent non-skill components. Keep the six complete directories inside that plugin root. A manifest path such as `../../skills/design` is invalid: component paths must stay inside the plugin root. [C4]

Claude documents marketplace-internal symlinks as a sharing mechanism: targets elsewhere in the same marketplace are dereferenced when copied into the cache. This can avoid duplicated authoring files, but local-directory/command-source behavior and validation of symlinks differ, and Windows requires symlink support. That path was not exercised here; adding six symlinks or an export step solely to save two tiny JSON files would be needless complexity for the initial portable collection. [C6]

## OpenCode V2 optional checkout source

No OpenCode config is needed for the primary installer. For an existing authoring checkout, V2 also supports this exact shape in a project or global `opencode.json(c)`:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "skills": ["/absolute/path/to/skills-repo/skills"]
}
```

`skills` is an **array**, not a guessed V1 `skills.paths` object. Relative entries resolve from the active working directory, not the config file; absolute paths are clearer for a shared checkout. Config arrays from discovered files combine. Update this delivery by updating the checkout; uninstall it by removing the one configured source entry. This is a documented optional authoring path, not a config change made by this research. [O1, O2]

Do not put the GitHub repository URL directly in `skills`: HTTP entries mean an OpenCode catalog with `index.json`, not a Git clone. No catalog, npm plugin, or OpenCode-specific distribution service is needed for this repository. V2's catalog root-`SKILL.md` ID quirk is another reason to keep the ordinary directory installation. [O1]

## Dry validation and isolated install verification

Run the following only after the actual bundles exist. It uses native tooling and disposable directories; there is no custom validation framework to maintain. These commands validate packaging, not design-workflow quality.

### Source discovery and manifest checks

```sh
# From this repository's root:
npx --yes skills@1.7.0 add . --list
claude plugin validate . --strict --json
claude plugin validate ./skills --strict --json
```

The root command validates a marketplace first when both manifest files exist. For the alternative root-plugin pair, also validate the plugin file explicitly:

```sh
claude plugin validate ./.claude-plugin/plugin.json --strict --json
```

**Observed validator limitation:** both fixture validation commands exited 0, but `validate ./skills --json` returned `contents: []`. The marketplace result likewise had no per-skill results, which is documented for marketplace validation. Treat these as manifest/schema checks, not proof that all six skill bodies or resource links were validated. Count the names from `skills add --list`, inspect the files, and compare installed bundles.

### Disposable lifecycle probe

This recipe assumes a POSIX shell and an installed `claude`, Node/npm, and Python is not required. Capture the source and executable paths before changing `HOME`. On this machine the approved scratch parent is used explicitly:

```sh
REPO="$PWD"
CLAUDE_BIN="$(command -v claude)"
T="$(mktemp -d /private/var/folders/9g/l0rgs8rs2_9__kqn0smr9tnh0000gp/T/opencode/skills-check.XXXXXX)"
mkdir -p "$T/home" "$T/config" "$T/data" "$T/state" "$T/cache" \
  "$T/claude" "$T/codex" "$T/npm-cache" "$T/tmp" "$T/project"

(
  export HOME="$T/home"
  export XDG_CONFIG_HOME="$T/config" XDG_DATA_HOME="$T/data"
  export XDG_STATE_HOME="$T/state" XDG_CACHE_HOME="$T/cache"
  export CLAUDE_CONFIG_DIR="$T/claude" CODEX_HOME="$T/codex"
  export npm_config_cache="$T/npm-cache" TMPDIR="$T/tmp"
  export DISABLE_TELEMETRY=1 CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC=1
  cd "$T/project" || exit 1

  npx --yes skills@1.7.0 add "$REPO" \
    --skill design design-explore design-visual design-interaction design-components design-critique \
    --agent claude-code codex opencode -y --json

  for skill in design design-explore design-visual design-interaction design-components design-critique
  do
    diff -r "$REPO/skills/$skill" ".agents/skills/$skill" || exit 1
    test -f ".claude/skills/$skill/SKILL.md" || exit 1
  done

  # For the recommended optional family marketplace:
  "$CLAUDE_BIN" plugin validate "$REPO" --strict --json
  "$CLAUDE_BIN" plugin marketplace add "$REPO" --scope user
  "$CLAUDE_BIN" plugin install design@possibilities-skills --scope user
  "$CLAUDE_BIN" plugin details design
  "$CLAUDE_BIN" plugin uninstall design@possibilities-skills --scope user
  "$CLAUDE_BIN" plugin marketplace remove possibilities-skills --scope user

  npx --yes skills@1.7.0 remove \
    design design-explore design-visual design-interaction design-components design-critique \
    --agent claude-code codex opencode -y
)
```

Use an appropriate `mktemp` parent on other machines. The `diff` checks assume ordinary self-contained resource files, as recommended. A run with `--copy`, a run selecting only one leaf, and the same lifecycle with `-g` under this temporary home exercise the other important boundaries. Keep actual outcome separate from proposed commands in release notes.

For the **alternative root plugin**, a session-only no-install inventory command is:

```sh
claude --plugin-dir /absolute/path/to/skills-repo plugin details possibilities-skills
```

Run that under the same isolated environment for a dry packaging check. `--plugin-dir` does not process marketplace family-selection entries; the recommended marketplace-only design family therefore needs the disposable marketplace add/install loop above. [C7]

## Evidence and limits

### Actual probes

Versions observed: **Claude Code 2.1.285**, **Codex CLI 0.159.1**, **OpenCode v2.0.16**, **skills 1.7.0**. Only version/help inspection was performed against Codex/OpenCode executables; no model session or background service was started.

Probe root:

```text
/private/var/folders/9g/l0rgs8rs2_9__kqn0smr9tnh0000gp/T/opencode/skills-distribution.EWTVvV
```

All installing commands redirected `HOME`, XDG config/data/state/cache, `CLAUDE_CONFIG_DIR`, `CODEX_HOME`, npm cache, and temporary files into that scratch tree. Fixtures had six named design bundles, an unrelated seventh bundle, nested local references, and an outside-bundle authoring sentinel. There were no hooks, MCP servers, or executable skill scripts.

| Probe | Observed outcome |
|---|---|
| `skills add <fixture> --list` | Seven skills discovered; six design skills and one unrelated skill |
| `skills add <fixture> --skill <six> --agent claude-code codex opencode -y --json` | Six installed results, all three agent names; references intact; unrelated skill absent |
| Same command with `-g` in temporary home | Six canonical bundles in temporary `$HOME/.agents/skills`, Claude links in temporary config |
| One leaf with `--copy` | Only that leaf installed, nested resource intact in both copied destinations |
| `skills list --json` | Listed installed skills, but reported only Claude Code and Codex even when explicitly filtered for all three; do not use this display omission as evidence that OpenCode cannot read `.agents/skills` |
| `skills add --list --json` | Rejected; plain `--list` works |
| `skills update design --project -y` on local-source install | Exit 0 but no matching updatable skill; no update demonstrated |
| `claude plugin validate <fixture> --strict --json` | Success, no manifest warnings/errors |
| Marketplace add → install → details | Success; `Skills (6)` with the six exact design names; zero agents/hooks/MCP/LSP |
| Claude cache inspection | Whole root-source package present, including unrelated/authoring files; only six skills loaded |
| Standalone project/global removal | Success; canonical bundles and links gone |
| Claude uninstall + marketplace removal | Success inside scratch |

The `skills` installer files remain in isolated npm cache and the single-leaf copy fixture remains in scratch for inspection. No real user configuration, other repository, README, or implementation file was changed by this research. The report itself is the sole authored repository file.

### Boundaries of the conclusion

- The common installer is verified at the filesystem/package level. A fresh Codex/OpenCode session loading and following the actual design skills is a release acceptance step, not an outcome of this probe.
- Claude's plugin component inventory is verified, but no model was asked to route between leaves. Namespaced invocation behavior is sourced from current official documentation.
- Hosted Git installation, authentication, release update detection, and Windows behavior were not exercised. The local Git remote identifies the source, not public accessibility.
- Current upstream docs can exceed older installed versions. The versioned CLI observations above are the reproducible baseline.
- No portable package dependency resolver or external shared-reference transport was established; self-contained bundles and explicit family installation are the supported baseline.

## Sources and retrieval provenance

Brain was queried before web retrieval with `Claude Codex OpenCode skills plugin marketplace portable installation`. Its results were community repositories rather than current host contracts; they were treated as prior-reading leads, not packaging authorities. Example: **document_id 1056, chunk_id 15362, “Diagram Design,” https://github.com/cathrynlavery/diagram-design**. No Brain write or paid web search was used.

The OpenCode skill was loaded and only V2 documentation was used for V2 claims. No inference was made from the generic `https://opencode.ai/config.json` schema. Agentscrape retrieved the official Vercel CLI README. Its browser-backed documentation requests failed with `upstream_unavailable` / `Plugin 'stack' returned success=false`; direct `webfetch` then successfully retrieved the official documentation below. Known URLs were fetched directly.

- **[C1] Claude Code skills:** https://code.claude.com/docs/en/skills — discovery, standalone/plugin naming, symlinks, frontmatter, local resources, Claude-only substitutions.
- **[C2] Claude plugins overview:** https://code.claude.com/docs/en/plugins (current content: plugins overview) — plugin as a unit; native versus standalone delivery.
- **[C3] Create a marketplace:** https://code.claude.com/docs/en/plugin-marketplaces (current content: create a marketplace); canonical page https://code.claude.com/docs/en/plugins/create-marketplace — required fields, root-relative sources, local validation/install loop.
- **[C4] Plugin manifest reference:** https://code.claude.com/docs/en/plugins/manifest-reference — required plugin name, default `skills/`, additive manifest skill sources, root-source marketplace selection, containment, strict-mode conflicts.
- **[C5] Marketplace reference:** https://code.claude.com/docs/en/plugins/marketplace-reference — top-level/entry schemas, source types, no-manifest entries, names and version precedence.
- **[C6] Host and maintain a marketplace:** https://code.claude.com/docs/en/plugins/host-marketplace — version bumps, auto-update default, relative-path hosting, marketplace symlinks.
- **[C7] Plugin commands reference:** https://code.claude.com/docs/en/plugins/cli-reference — exact install/update/uninstall/marketplace/validate/details commands, scopes, session-only plugin loading, validation limitations.
- **[X1] OpenAI skills:** https://developers.openai.com/codex/skills (current content: “Build skills,” linked canonical https://developers.openai.com/codex/build-skills) — `name`/`description`, `$` invocation, `.agents/skills` discovery, symlinks, optional `agents/openai.yaml`, local skills versus plugin distribution.
- **[O1] OpenCode V2 skills:** https://opencode.ai/v2/docs/skills — directory resource base, all discovery paths, path-derived IDs, exact skill tool schema, V2 config source array, catalogs and precedence.
- **[O2] OpenCode V2 config:** https://opencode.ai/v2/docs/config — config files and `skills` array shape.
- **[S1] Vercel skills CLI official README:** https://github.com/vercel-labs/skills — multi-agent support, source forms, explicit skill selection, add/update/remove, copying/symlinking, discovery and manifest support. Read through Agentscrape; returned README artifact SHA-256 **`ec12d27cafb4d6153770a319f6d88a6936729a48e6aceba8a7d6a0574573bdf7`**.
- **Local CLI evidence:** installed `claude plugin --help`, `claude plugin validate --help`, `codex --help`, `opencode --help`, `opencode debug --help`; downloaded-in-scratch `skills@1.7.0 --help` and the lifecycle commands recorded above. Local observations qualify README defaults where they differed.
