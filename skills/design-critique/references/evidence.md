# Evidence and recheck

| Evidence | Supports | Does not establish alone |
| --- | --- | --- |
| Source/schema review | Intended structure, transformations, allowed states | Rendered usability or actual input |
| Deterministic/fake-state tests | State transitions and failure handling under those inputs | Device lifecycle, native focus, audible quality |
| Screenshot | Visible hierarchy, typography, clipping, state | Timing, keyboard, cancellation, recovery |
| Accessibility/DOM tree | Exposed names, roles, state, structure | Unclipped geometry, contrast, usable hit targets |
| Interaction recording | Observed task/transition sequence | Every other scenario or the cause of latency |
| Target-device/window/PTY run | That target/build's rendering and input | Universal behavior across environments |
| Listening/comprehension trial | Audible meaning and character in context | All acoustic environments or transport correctness |

Record the target/build, scenario, dimensions, relevant settings, and decisive
observation. Do not report a proposed check as performed or simulated activity
as a successful live effect. If only one viewport or input was checked, say so.

## Select revealing cases from the defect

- Content/fit: empty, one item, dense, long/localized labels, large text,
  minimum width, shallow height, orientation, supported themes.
- Input: keyboard-only, focus return, pointer/keyboard transition, assistive
  names/state, first click, IME, press/move/release/cancel, second pointer.
- Continuity: incoming item between down/up, refresh while editing/reading,
  stale content, reconnect, disappearing selection, live-follow opt-out.
- Dynamic feedback: rapid reversal, reduced motion, noisy/high-rate input,
  timer supersession, stale acknowledgement, first frame versus established view.
- Recovery: save while editing continues, failed persistence, interrupted
  command, reset scope, restart with a retained draft, legacy profile loading.
- Terminal: actual glyph cells, narrow/shallow screens, modal key ownership,
  streams/exits/non-TTY for CLI, cursor/mode restoration for TUI.

Choose the cases with a plausible failure path. A one-label fix does not need
a full lifecycle campaign; a stuck recording hold does need cancellation and
late-response evidence even if its screenshot is perfect.

## Recheck the correction

Hold representative conditions constant for before/after evidence. Check the
actual consumer after changing a shared token/component. Static/type checks
protect implementation contracts but complement, rather than replace, target
observation. Use existing meaningful checks; add a regression test when it
protects a real failure boundary rather than mirroring source or a screenshot.

If the target cannot be run, state what source inspection supports and the
specific observation still needed. Avoid saying “accessible,” “responsive,”
or “fixed everywhere” based on a single narrow kind of evidence.
