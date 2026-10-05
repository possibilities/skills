# TUI: a real terminal surface

Inspect the actual framework and terminal contract: Ratatui, Textual, Bubble
Tea, OpenTUI, or another. Reuse its rendering/input lifecycle. A web layout is
not a terminal implementation plan, and no particular palette, shell geometry,
or command-palette shortcut is universal.

## Compose in cells

Begin with the working object, its state, primary action, and recovery. Define
what survives at minimum width and shallow height. Reflow, collapse secondary
columns, disclose detail, or use a focused view before making essential text
unreadable. Keep the next useful action discoverable even in a cramped state.

Measure display-cell width, not string length or UTF-8 byte length. CJK,
combining characters, emoji, and terminal/font differences can change geometry.
Use the framework's width/wrapping tools and inspect real rendering. Provide
ASCII or simpler-glyph fallbacks where the product promises broad terminal
support. Test glyph families on actual rows and controls, not square icons.

Use spacing, alignment, and restrained semantic emphasis. Give peers equal
roles and meaningful state a non-color cue. Dense output can still have a
clear entry point. Check the supported color depth/backgrounds and plain
representation instead of treating one dark screenshot as universal.

## Define input modes and continuity

Identify focused region, list selection, text-edit mode, modal ownership, and
global commands. Text input should not accidentally trigger global shortcuts.
Make essential navigation, help, exit, and recovery discoverable; preserve
existing shortcuts instead of imposing a new keymap for appearance.

Check keyboard-only operation. Support mouse behavior only where the app
actually promises it, without making it the sole path. Esc/back semantics
should unwind the right layer rather than discard unrelated work.

Background refresh should preserve selection by identity, scroll position,
expanded detail, and drafts. Keep useful committed content while fetching.
When the selected item disappears, choose a predictable successor and explain
the relevant change rather than acting on a different item silently.

Keep renderer lifetime stable through ordinary updates. Bound redraw work,
coalesce high-rate events, and avoid flicker. Terminal resize is an event to
handle, not a reason to lose editing state.

## Verify through a real PTY

Load `terminal-control` if available when operating the application, or use
the current harness's PTY capability. Inspect the current visible screen, not
only scrollback/logs. Exercise the main keyboard flow, narrow/wide/shallow
dimensions, long labels/glyphs, overlays, refresh, and the changed failure state.

Check normal exit and relevant interruption restore cursor visibility, terminal
modes, and shell usability. Capture terminal size, framework/build, scenario,
and input sequence with decisive screens or recordings. A string snapshot
cannot prove key delivery, glyph geometry, mouse modes, or terminal restoration.

Use current docs for the actual framework. Terminal craft is shared judgment;
framework-specific APIs and rendering assumptions are not interchangeable.
