# Predictable experiments and exact adoption

Build enough infrastructure to answer the question. A local state switcher is
often sufficient; a remote controller is justified only by an actual device or
multi-controller need. Use real rendering components to reduce preview drift.

## Repeatable scenarios

Choose a bounded set relevant to the work: empty, sparse, dense, long labels,
active, blocked, failed, disconnected, recovered. Match scenarios across
variants and separate synthetic inputs from production data. Keep renderer
instances stable through ordinary tuning so sliders do not replay startup,
drop focus, or cancel held input.

Expose meaningful parameters with units/ranges and a baseline. Independent
choices stay independent: changing icons should not reset size, resetting
spacing should not change motion. Declare shared, layout-specific, and
session-only controls. Apply a grouped reset atomically. Show requested values
separately from effective fit limits when the viewport cannot accommodate them.

The preview interface adjusts declared presentation parameters and scenarios;
it need not execute arbitrary code, commands, or filesystem paths. Production
input and lifecycle ownership remain intact.

## State of the design itself

| State | Promise |
| --- | --- |
| Live | What the target actually acknowledged and shows |
| Working draft | Retained editable choices, if durability is promised |
| Checkpoint | The exact snapshot captured for review/export |
| Production defaults | The adopted baseline in the real product |
| Rehearsal | Fake activity, held input, debug holds, temporary connections |

Do not call an unsent edit live, a saved draft accepted, or rehearsal production.
Save the reviewed snapshot, not whatever exists when a delayed write finishes.
If edits continue, preserve them and make divergence from the checkpoint clear.
For remote controllers, reject stale edits and observe after reconnect rather
than blindly replaying uncertain mutations. Report target save and host export
separately if either can fail independently.

## Adoption

Capture reviewed choices including relevant inactive layouts, hidden-control
tuning, icons, sounds, and build-time assets. Exclude held fingers, fake activity,
debug timing holds, and credentials. Preserve asset provenance, author/license,
and required notices; a research screenshot is not automatically cleared art.

Translate the choice into real tokens, components, constants, and assets. Keep
a reproducible relationship to the reviewed artifact where complexity warrants
it. Remove rejected branches and unnecessary experiment controls. Check the
actual product with real state inputs and packaged assets after adoption.

Older profiles need explicit compatibility behavior. Rebuilds or reconnects
should not erase a promised durable draft. Keep reset-to-production distinct
from granular resets.

## Demonstration versus proof

Compose a demo around problem → meaningful action → payoff, at its actual
viewing size. Keep original captures separate from edits. Crops and annotations
can clarify; shortened timings, manufactured sounds, or interpolated frames
cannot substantiate runtime responsiveness. Review the final export and make
it understandable muted when sound is not essential. Record whether a capture
is a normal run, deterministic rehearsal, or held inspection state.
