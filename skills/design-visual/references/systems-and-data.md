# Systems, comparisons, and adoption

## A system expresses roles

Inventory existing tokens and representative screens before adding a second
system. Separate semantic roles (focus, selection, destructive action, surface,
subordinate text) from raw values. Define typography, spacing relationships,
shape/depth, icon family, and supported appearances only as far as the product
needs. Keep meaningful local exceptions explicit rather than hiding them in
one-off nudges.

A component contract includes purpose, anatomy, states, input behavior,
content limits, accessibility, and responsive behavior. A palette alone is not
a system. Distinguish primitive, composed pattern, and page-specific layout.
Promote a pattern after it works in genuinely different representative contexts,
not because two screenshots share rounded rectangles.

For multiple surfaces, map intent to local realization:

| Shared intent | Platform-specific expression |
| --- | --- |
| Current focus is unmistakable | Browser focus styling, native focus ring, terminal focused-region treatment |
| Secondary detail is available | Disclosure, inspector, detail view, command output mode |
| State is legible without color | Labels, shapes, glyphs, position, native accessibility state |
| Work survives refresh | Stable keys/identity, focus/selection/scroll handling appropriate to the toolkit |

Document ownership and adoption: canonical token/component source, how an
existing screen migrates, and the exceptions that stay local. Validate supported
themes and constraints. Avoid silently replacing user-modified components or
introducing a new dependency for a role the existing system can express.

## Honest data representation

Choose the representation from the question:

| Need | Starting representation |
| --- | --- |
| Exact lookup | Table/aligned text |
| Rank or magnitude | Position/length on a shared scale |
| Change over time | Ordered, comparable time values |
| Part of a whole | Proportions with a stated denominator |
| Threshold/exception | Distance from a visible boundary |
| Qualitative alternatives | Aligned semantic rows or contrasted sections |

Preserve units, periods, populations, baseline, and uncertainty. Unequal
populations make raw-count comparisons misleading. Missing data is not zero.
Length encodings need an honest common scale; a decorative bar cannot pretend
to measure something. Align label, plot, and value lanes so long labels do not
shorten individual tracks. Use consistent precision and tabular numerals where
appropriate. Direct labels and a text/table alternative improve inspection.

Give each claim one primary evidence home. Repeating a metric as a hero, three
cards, a chart, and a conclusion increases volume without understanding.

## Verify a system change

Pick representative examples that expose different demands: a dense data view,
a form/error state, a constrained viewport/window, or a terminal with long
labels. Inspect actual consumers after token/component migration. Record
remaining exceptions and whether old/new patterns coexist intentionally.

When a new visual role appears necessary, first ask which existing role fails
and in what context. That explanation is more durable than another raw color
or spacing value. Keep changes at the owning level so the same defect does not
need five local margin patches.
