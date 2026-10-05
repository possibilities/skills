# CLI: clarity for people and stable contracts for scripts

A CLI is a language and stream interface. Inspect existing commands, help,
output modes, parser contracts, and consumers before changing vocabulary or
formatting. Preserve established flags, JSON schemas, exit behavior, and piping
unless the request explicitly includes a compatibility change.

## Define what belongs where

- Human output should lead with the result or the next useful action. Use
  consistent nouns/verbs, concise labels, aligned comparisons, and meaningful
  units. Empty output, no results, partial success, and failure need distinct
  meanings.
- Follow the command's established stdout/stderr contract. Ordinarily data and
  requested machine output go to stdout, diagnostics/progress to stderr. Do not
  move an existing public stream contract as incidental visual cleanup.
- Keep JSON/JSONL or another machine mode parseable and stable: no banner,
  progress, color, or explanatory prose mixed in. A human-table improvement
  should not silently change default piped output.
- Make success/failure and recovery available through exit status and useful
  messages, not color alone. Differentiate retrying a failed write from repeating
  successful computation or an uncertain external effect.

## Compose for the destination

Use TTY detection to support the documented interactive behavior; redirected
output must not contain cursor animation or require a live prompt. Honor
existing no-color/plain-output conventions and inspect whether `NO_COLOR` is
already supported before documenting it. A narrow terminal may require a
vertical record or reduced human columns, while full machine data remains
available through its established mode.

Put examples and the normal next step in help where people look. Keep
subcommand/help relationships consistent. Prompt defaults should be visible,
and noninteractive execution should resolve through documented flags or fail
clearly instead of hanging. Show long-running progress only where useful;
interrupts should leave a truthful result and usable terminal.

Do not turn a readability request into a full-screen TUI. If the requested task
genuinely needs persistent navigation, use the TUI reference as a separate
surface with an explicit interface decision.

## Verify the public boundary

Run representative successful, empty, partial, and failed commands appropriate
to the change. Capture stdout, stderr, and exit status separately. Check the
existing machine mode with its parser, pipe/redirection behavior, narrow human
output, color-off output, and interruption when relevant. Use a real PTY for
prompts/progress; ordinary shell execution is enough for noninteractive cases.

Record the exact command and environment dimensions relevant to the claim. A
pretty terminal screenshot does not establish stream or script compatibility.
Avoid executing destructive examples merely to inspect their formatting; use
the project's existing dry-run/fixtures or a disposable target.

Reference: [Command Line Interface Guidelines](https://clig.dev/). Existing
public contracts remain the starting point even where a new CLI would choose
a different convention.
