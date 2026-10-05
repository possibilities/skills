---
name: design-interaction
description: >-
  Design and repair interface behavior: action/state meaning, focus, gestures,
  cancellation, refresh continuity, recovery, motion, sound, and responsiveness.
  Use for stuck holds, wrong-item clicks, lost drafts or scroll position,
  misleading status, notification behavior, or dynamic interaction design on
  mobile, desktop, web, CLI, and TUI.
---

# Trustworthy interaction

Identify the intended task, actual platform/toolkit, state owner, and observed
failure or open decision. Preserve the brief and accepted composition. When
invoked alone, inspect available project evidence and infer routine context;
ask only about a decision that materially changes behavior.

## Name the facts and the actions

Use the person's vocabulary consistently across control, progress, result,
and recovery. Choose controls by meaning: persistent preference, momentary
action, navigation, reading details, and external execution are different.
Advertised affordances should work, be explicitly noninteractive, or explain
why unavailable; silent callbacks are not finished controls.

Distinguish facts that change the next action:

- preference versus effective state; permission versus activity;
- requested versus accepted versus completed;
- execution versus quality; generated versus saved versus reviewed;
- connected versus fresh data versus rendered/audible output.

Design empty, initial-loading, useful-but-stale, disconnected, failed, unknown,
and recovered states where applicable. Missing measurements are not zeroes.
Immediate local input feedback is not proof of remote completion.

## Model the complete interaction

For each consequential action specify **acquire → immediate feedback → commit
or cancel → release/recover**. Identify the data/gesture identity carried
through the sequence. Consider pointer departure, second pointer, focus loss,
backgrounding, disable/removal, repeated events, and late acknowledgements.
A canceled hold must not latch or reopen because an old acknowledgement arrives.

Keep hit geometry stable. Bind activation to the pressed item's identity so
an arrival between down/up cannot redirect it. Dragging preserves the grab
point under one coordinate/movement owner. Decoration yields to input; overlay
dismissal should not accidentally activate what was covered.

Preserve selection, disclosure, drafts, focus, and reading position during
refresh. Retain useful committed content rather than blanking every poll.
Follow streaming content only when the person has chosen to follow and offer
a clear return to latest. Initial loading and explicit blocking operations can
still warrant progress.

Recover at the failed boundary. Retry saving a successful generation rather
than rerunning it. Preserve completed stages. When an external action may have
occurred, inspect the result before treating retry as harmless.

Read [state, attention, motion, and sound](references/state-and-motion.md) when
writing a state contract or designing dynamic/expressive feedback.

## Respect medium and input

| Target | Decisive boundaries |
| --- | --- |
| Mobile | Back/navigation, keyboard/insets, gesture ownership, lifecycle, text scaling, assistive paths |
| Desktop | First-click/window focus, modifiers/IME, menus, placement, arrival identity, drag/resize |
| Web | Semantic controls, focus entry/return, history, keyboard, zoom, form recovery |
| CLI | Streams/exits, prompts/non-TTY, interruption, script compatibility, failure wording |
| TUI | Focused region/edit modes, modal key ownership, stable refresh/selection, resize, terminal restoration |

Equivalent outcomes need appropriate input paths, not identical gestures.
Preserve visible keyboard focus, text composition, and assistive navigation.
Keep primary action and emergency escape discoverable.

## Verify the failure boundary

Use actual platform observation when available, loading the relevant operating
skill by its advertised name. Check the reported sequence plus its meaningful
interruption/race, not only the happy path. Use controlled state tests for
deterministic transitions and actual input for platform claims. Screenshots
cannot prove cancellation, latency, or sound; AX presence cannot prove an
unclipped target. Record device/build, sequence, scenario, and limits.

Return a compact state/transition contract, corrected behavior when requested,
and observed evidence. Keep untested cases explicit. Do not turn a behavioral
repair into a visual redesign or restart intake through the design router.
