---
name: design-critique
description: >-
  Review or diagnose an existing interface with prioritized, evidence-linked
  design findings. Use for UX/design audits, screenshot critique, confusing or
  cramped screens, regressions, accessibility concerns, or bounded repairs on
  mobile, desktop, web, CLI, and TUI. Distinguishes visible evidence from behavior
  that still needs observation and preserves accepted design choices.
---

# Critique and repair

Identify the person's primary job, the actual platform/stack, accepted choices,
and the requested output: findings, proposed corrections, or implementation.
Use supplied evidence before collecting more. When invoked alone, infer routine
context from the project; a missing screenshot or target is a concrete evidence
gap, not a reason to invent what the interface looks like.

## Inspect from large relationships to detail

1. **Task:** Can someone understand and begin the main job? Is the useful
   content/action present before secondary metrics or setup?
2. **Composition:** Is the entry point and grouping clear? Does the organizing
   idea belong to this material? Are peers and unequal facts treated meaningfully?
3. **Interaction:** Do actions, state, feedback, continuity, and recovery tell
   the truth? What happens on interruption, refresh, and rapid reversal?
4. **Type and rhythm:** Can labels be read? Are units, precision, baselines,
   grouping, and gap ownership consistent?
5. **Expression:** Do color, imagery, motion, and sound support meaning or
   deliberate character? Are essential states available without color?
6. **Adaptation:** Does the task survive long content, larger text, constrained
   dimensions, alternate input, and accessibility settings?
7. **Finish:** Inspect clipping, optical alignment, first frames, asset edges,
   and transitions in the actual renderer.

Fix the largest consequential relationship first. Too much material calls for
ordering/disclosure; too much competing emphasis calls for hierarchy. Several
local margin bugs may share one grouping error. A target that jumps under the
pointer needs continuity, not an animation.

Inspect whole-screen composition and native-resolution detail separately. Use
the medium's mechanics: mobile lifecycle/back/touch; desktop focus/windows/IME;
web semantics/history/keyboard; CLI streams/exits/pipes; TUI cells, modes,
resize, and terminal restoration. Do not prescribe a web component kit or a
historical house palette merely because the interface lacks polish.

## Make findings actionable

Use this shape, shortened to the task:

> **Severity — observed issue.** Affected task/person; concrete location or
> evidence; why it matters; proposed correction; recheck needed.

Rank by impact on task completion, likelihood/reach, and recoverability:

- **Blocking:** prevents the primary task or can cause unintended action/loss.
- **Significant:** repeatedly obscures meaning, access, or recovery.
- **Polish:** perceptible finish issue with bounded task impact.

Separate observed defect, hypothesis needing a check, and preference. Aesthetic
preference can guide selection without becoming a universal mandate. Say when
there are no consequential findings; do not manufacture a quota of issues.

Use [evidence and recheck](references/evidence.md) when deciding what a source,
screenshot, recording, or live inspection establishes. Never infer verified
keyboard, assistive, timing, or gesture behavior from pixels alone.

## Repair within the accepted design

When implementation is requested, reproduce the important failure, find the
owning rule/component, make a bounded correction, and recheck both the failure
and nearby behavior. Preserve accepted composition and public contracts.
A clipped-label repair should not silently change theme, font, or framework.
For uncertain mechanism, load the available `design-interaction` or
`design-visual` skill by the actual catalog identifier, preferring this family;
carry the finding rather than restarting intake. No specialist is required for
a straightforward local correction.

Use existing stack guidance conditionally. Web code audits can use
`web-design-guidelines`; React performance rules apply only to React work.
Native and terminal work need their own observation tools. If those tools are
unavailable, still provide bounded findings and a specific next check.

Finish with the few highest-impact findings or completed corrections, decisive
evidence, and remaining limits. A screenshot-only review remains useful when it
is honest about its scope. A repair is complete when the observed experience
improves, not merely when source changes or static checks pass.
