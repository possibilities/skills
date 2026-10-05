---
name: design-explore
description: >-
  Explore interface directions through a focused baseline and meaningful
  alternatives. Use when choosing a layout, navigation model, visual direction,
  interaction, or prototype across mobile, desktop, CLI, TUI, and web, or when
  an interface feels wrong but the right correction is uncertain.
---

# Explore a design decision

Turn one consequential uncertainty into a comparison someone can judge. Use
the brief and evidence already available. If invoked alone, establish the
person, job, target/stack, accepted choices, question, and available evidence.
Infer routine facts from the project; ask only what changes the decision.

## Frame the experiment

Translate “make it nicer” into a question: can people find blocked work, does
navigation preserve context, is the relationship between a reading and its
controls apparent? Separate a defect from preference. A missed first press
needs repair whichever visual direction wins.

Preserve accepted axes. When the composition is right and spacing is wrong,
make the correction; do not manufacture three redesigns. For an open question,
start with the current baseline and one or two alternatives that change the
relevant structure or behavior. Name them perceptually: “work first,” “persistent
details,” “compact summary.” Color swaps alone are not structural alternatives.

Use references to answer this question. Inspect existing project knowledge
first; search outside only for the missing precedent or mechanism. For each
reference, say what transfers and what does not. A web animation can inspire
a native object without justifying a WebView implementation.

## Make comparison fair and useful

Hold representative content, state, size, text scale, primary task, and
interaction readiness constant. Include realistic names and lengths rather
than a polished empty demo. Explain a perceptible gain and a cost for each
direction. Tie, Neither, and Uncertain are valid outcomes.

Choose the smallest sufficient fidelity:

| Question | Useful evidence |
| --- | --- |
| Hierarchy, ordering, grouping | Comparable static compositions with real content |
| Navigation, gesture, focus, interruption | Interactive prototype in the actual renderer |
| Terminal density and glyph fit | Real cell rendering at target dimensions |
| Native input, lifecycle, safe areas | Target app/device or bounded emulator evidence |
| Latency, motion, sound | Observed task/timing or listening, with limits recorded |

Use existing components with controlled synthetic scenarios where practical.
Mark simulated state. A preview should not need live accounts, inference,
microphones, or external effects just to demonstrate an active state. Keep
adjustment controls outside the judged surface when possible. Read
[experiments and adoption](references/experiments.md) when building a tunable
prototype, saving a choice, or moving a reviewed direction into production.

## Run a short loop

1. Show the baseline at the intended scale and let the primary task guide review.
2. Identify the most consequential friction; make one interpretable change.
3. Compare under matched conditions, including the difficult state relevant to
   the question. Keep a failed variant's outcome separate from a successful one.
4. Recommend a direction with reasons and remaining uncertainty. Ask for taste
   decisions only where they matter; resolve routine implementation choices.
5. Record the reviewed choice and carry it into implementation if requested.
   Check the adopted product rather than equating a saved preview with delivery.

Adapt to the medium: mobile needs reach/back/lifecycle; desktop needs focus and
window behavior; CLI needs command/stream clarity; TUI needs cell geometry and
input ownership; web needs semantic order and responsive flows. Share the
intent, not identical geometry across them.

For an unresolved visual or behavioral mechanism, load the available
`design-visual` or `design-interaction` specialist by its advertised catalog
identifier, preferring this family in a namespaced installation. Pass the
question and constraints; do not restart the router or load all specialists.
If unavailable, continue using target docs and the evidence above.

Return the question, preserved constraints, compared directions, tradeoffs,
recommendation, and decisive evidence. Match output size to the decision; a
short comparison can be more useful than a mood board or elaborate studio.
