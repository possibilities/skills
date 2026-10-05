---
name: design-visual
description: >-
  Shape interface hierarchy, composition, typography, spacing, color, icons,
  data presentation, and design systems. Use when a screen is busy, bland,
  inconsistent, hard to scan, or needs a coherent visual direction across
  web, mobile, desktop, CLI, or TUI. Preserve the actual stack and accepted style.
---

# Visual judgment

Begin with the person, job, real content, primary relationship/action, target,
and accepted constraints. Inspect the current composition and component/token
system. If invoked with a brief, use it; if alone, infer these from the task
and ask only about material uncertainty.

## Choose an organizing idea

Build around the working object or decision: stalled work and its recovery,
the document being edited, aligned alternatives, the live instrument and its
controls. A product title plus identical metric cards is not a default answer.

Ask whether changing the product name would make the proposal equally plausible
for an unrelated app. Find specificity in content and behavior, not novelty for
its own sake. An established design system can be exactly right. Concentrate
character in a few intentional proportions, typographic relationships, assets,
or expressive objects; make supporting controls cooperate.

## Fix relationships before details

Establish where the eye enters, what belongs together, and where it goes next.
Use position, scale, alignment, weight, and space before boundaries. True peers
deserve equivalent treatment; unequal content need not occupy equal cards.
Keep qualifiers beside the facts they explain.

Every visual device makes a claim: border = boundary, number = order/reference,
connector = relationship, badge = meaningful category/state. Remove devices
without a job. Keep secondary information readable while letting it recede.

Distinguish **too much material** from **too much competing emphasis**. For the
first, remove, combine, reorder, or disclose. For the second, reduce competition
while retaining a focal anchor. Shrinking all text or flattening everything to
gray solves neither. Squint/blur checks reveal hierarchy, not usability; follow
them with reading and interaction.

## Build a coherent vocabulary

Use a small set of type roles for headings, body, labels, values, and supporting
context. Match peers and align shared edges/baselines. Judge line length and
leading at the intended reading size. Rewrite, wrap, or recompose before
shrinking essential type. Give every gap one owner: internal group rhythm and
separation between groups are different responsibilities.

Define semantic color roles for surface, text, focus, selection, warning, and
error. Separate entity identity from operational state and add a non-color cue
for essential meaning. Check supported appearances independently. Gradients,
glow, and expressive artwork are useful when they explain material, depth, or
character; restraint is not a universal ban on personality.

Choose icons as an optical family: size, stroke/fill, baseline, active and
disabled states. Compare abstract symbols with familiar icons/labels on first
recognition. Functional controls need names and understandable meaning; launcher
identity can be more abstract. Keep production asset provenance and license.

Read [systems and data](references/systems-and-data.md) for token architecture,
multi-surface systems, charts/comparisons, and migration.

## Adapt, then verify

Preserve object identity, state, meaningful value, primary action, and recovery
at constrained sizes. Reflow, stack, abbreviate meaningfully, or disclose before
compressing. Reserve geometry for legitimate changing labels and counts. Test
long/localized strings, sparse/dense content, larger text, and shallow height.

Translate to the medium: mobile respects safe areas and touch; desktop respects
native controls and window bounds; web preserves semantic reading order and
zoom; CLI keeps script output stable while organizing human text; TUI uses
display-cell widths, readable glyphs, and discoverable actions. Shared semantic
roles do not require identical pixel geometry.

Inspect whole-screen composition and native-resolution details in the actual
renderer. A screenshot can support hierarchy/clipping findings; it cannot
prove input, focus, lifecycle, or performance. Use the available target tools
for the claims you need. If behavior is the blocker, load the installed
`design-interaction` by its actual identifier, preferring the same family;
otherwise continue from project guidance without restarting intake.

Deliver concrete composition/role decisions and the rationale tied to the job.
For implementation, adopt them in existing components/tokens and show target
evidence. For a review-only request, return corrections without editing. Prefer
one coherent improvement over a catalog of unrelated aesthetic suggestions.
