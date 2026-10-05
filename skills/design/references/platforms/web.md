# Web: semantics and usable composition

Identify the framework, rendering mode, component owner, routing conventions,
tokens, and representative content. Improve the current system before choosing
a new one. Server templates, Vue, Svelte, plain HTML, and React are all valid
starting points; shadcn's React implementation is conditional.

## Design the task

- Put the useful object or decision before a generic title/metrics shell.
  Preserve meaningful content order in the document as well as the visual grid.
- Use links for navigation and buttons for actions. Keep URL/history behavior
  meaningful for navigation, filters, and return paths where the app promises it.
- Forms need visible labels, useful input types/autocomplete, grouped choices,
  and error recovery that preserves entered data. Explain the correction close
  to the field; do not rely on placeholder text or color as the label/error.
- Distinguish first load, refresh with useful existing data, no results, no data,
  permission-limited content, and failure. A blank panel cannot explain all six.
- Define dialog focus entry/return, dismissal, and background interaction.
  Keep keyboard focus visible and avoid hover-only access to essential tasks.

## Adapt from content fit

Choose breakpoints where content stops working. Preserve identity, state,
meaningful value, primary action, and recovery. Reorder, wrap, stack, or disclose
before shrinking type. Long names and changing status labels are normal inputs.
Use local table/code scrolling when needed rather than overflowing the page.

Check browser zoom and larger text; do not disable zoom to hide a layout defect.
Check narrow width and shallow height independently. For mobile web also use
the mobile reference: viewport changes, keyboard occlusion, touch, and insets
are more than a narrow screenshot. Test supported color appearances rather
than assuming inversion preserves contrast and hierarchy.

## Responsiveness and continuity

Preserve focus, selection, form state, and reading position on updates. In a
streaming feed, follow only while the user has chosen to follow; make returning
to latest clear. Choose one owner for scroll anchoring. Measure input-to-visible
response with realistic content; virtualization does not fix repeated parsing
or serialization of the whole dataset.

Use reduced motion as a finished presentation. State/control truth updates
immediately; decorative transitions cannot delay a disabled state or keep a
false status visible. Keep animation out of hit-target geometry.

## Verify in a browser

Use the available browser integration and its operating instructions. Inspect
the whole screen and native-resolution detail. Run the primary task by keyboard,
including visible focus and relevant overlay/form behavior; inspect accessible
names and semantics as complementary evidence. Exercise the changed empty,
error, long-content, and responsive states. Check contrast with actual computed
colors when making a quantitative claim.

Capture target URL/build, viewport, content/state, relevant settings, and what
was observed. If only source or screenshots are available, limit conclusions
accordingly and give the next check. Automated audits and DOM presence alone
do not prove a readable, unclipped, usable screen.

Current reference entrypoints: [WCAG](https://www.w3.org/WAI/standards-guidelines/wcag/)
and [web.dev accessibility](https://web.dev/accessibility/). Use the applicable
target standard when a specific numerical requirement matters.
