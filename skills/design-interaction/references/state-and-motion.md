# State contracts, attention, and expressive feedback

## A compact contract

Use a table only when it makes behavior clearer:

| Current fact | Event and identity | Immediate feedback | Established next fact | Cancellation/recovery |
| --- | --- | --- | --- | --- |
| Idle | Press starts generation G | Press received | Request pending for G | Release/background invalidates G |
| Pending G | Accepted G | Active only if G still current | Operation active | Old G cannot reopen canceled work |
| Result generated | Save requested for snapshot S | Saving S | Saved only after durable acknowledgement | Retry S's write, preserve newer live edits |

These are examples, not a prescribed state library. Identify existing owners
before adding state machinery. Define authoritative events, stale-event
handling, side-effect ownership, and what must be released on all exits.

Useful scenario set: normal completion, rejection, interrupt, rapid reversal,
repeat, focus loss, background/removal, reconnect, stale response, failed save.
Select the cases that can fail in this interaction rather than applying every
case mechanically.

## Attention and placement

Separate durable work from transient arrival. Unread, unfinished, dismissed,
and responded are different facts. Group bursts intentionally, avoid focus
theft, and preserve the exact item someone activates. Counts should reveal
what they count. Timed dismissal respects active editing/menu/keyboard use;
cancel obsolete deadlines so they cannot dismiss a newer surface. Recovery
must remain reachable after feedback disappears.

Honor manual placement. Changing persistence or view mode should not reset
coordinates without reason. Compare content geometry, not just outer windows.
Do not disguise layout errors with animated movement.

## Motion

Start with a coherent still composition. Add motion to explain change,
preserve continuity, confirm input, or express the working object. Concentrate
it instead of pulsing every region. Keep labels/actions usable during entry.

Control truth updates immediately: disabled means disabled now; false status
words disappear now. Decorative completion cannot imply real task completion.
Choreograph state pairs rather than tweening every property; cancel obsolete
transitions on reversal. Keep the same renderer through ordinary updates.
Changing animation speed should preserve phase rather than jump to a new pose.

Use separate time scales for immediate feedback, short accents, and ambient
evolution. Hysteresis can calm noisy measurements but must not delay authoritative
control states. Reserve clearance for glow/drift/text; decorative transparency
does not guarantee visual occlusion. Inspect actual pixel intersections.

Reduced motion should disable relevant decorative translation, scale, and
brightness modulation while keeping current information and a finished scene.
It should not freeze an obsolete reading or leave a half-entered composition.

## Sound and high-rate events

Every event may update the model without every event producing a toast, sound,
or animation. Coalesce bursts into counts, summaries, or a bounded texture.
Design overflow and silence. Define normal, idle, unavailable, Off, and level
control instead of allowing activity volume to equal noise volume.

Use a related sound family and map cues to accepted events. Re-render, hydration,
reconnect, and asset readiness should not replay old cues. A normal release and
cancellation may deserve different feedback. In voice interfaces, test whether
cues feed into the microphone/speech detector; reacting after detection may be
too late. Audition with real controls over realistic durations. Playback success
alone does not establish comfort or comprehension.

## Responsiveness

Measure input-to-visible response, not only average frame rate. Typing can feel
bursty because conversion, serialization, or reconciliation blocks the input
thread. Bound hidden work and preserve unchanged data as well as virtualizing
visible rows. Use realistic content sizes and the actual build. Report code-based
expectations separately from measurements; animation cannot repair dropped input.
