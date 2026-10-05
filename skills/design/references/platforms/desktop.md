# Desktop: window and input fidelity

Identify the operating system, toolkit, window roles, and rendering boundaries.
Native desktop, Electron/Tauri/WebView content, and browser apps have different
owners. Use Native SDK instructions only when the project actually uses it.
Hybrid work needs web-surface checks and native-shell checks.

## Preserve the person's workspace

- Establish window/content geometry, resizing, minimum usable dimensions,
  placement persistence, menus, and supported shortcuts. Compare content bounds
  as well as outer frames when investigating apparent alignment errors.
- Treat deliberate user placement as intent. Pinning or switching a view need
  not reset position. A transition cannot repair incorrect geometry.
- Keep selection, disclosure, drafts, reading position, and focused input
  stable as work arrives. Distinguish activation of a window from selection of
  its first control.
- Separate durable inbox/work storage from arrival presentation. Read,
  dismissed, responded, and completed are different actions and counts.

## Make event ownership explicit

For moving panels, preserve the original grab point and use one coordinate
model/movement owner. Drag regions yield to text, controls, scrolling, and
resize edges. Decorative layers should not intercept input. Dismissing an
overlay should not click the covered action accidentally.

Bind activation to the item identity at pointer-down, or preserve the visible
pressed item until completion. A new arrival between down/up must not redirect
the action. Verify focus loss and modifier release, first-click delivery,
repeated/reversed drag, new grab, and resizing while relevant.

Text entry includes IME composition, familiar editing shortcuts, selection,
and scroll momentum. Pointer use should not discard text focus or assistive
navigation unexpectedly. Advertise essential commands somewhere discoverable;
an internal team's memorized shortcut is not sufficient.

Arrival surfaces usually avoid stealing keyboard focus. Timed dismissal should
pause or otherwise respect editing, menus, keyboard use, and assistive access.
Cancel old deadlines so an unrelated callback cannot dismiss newer content.
Essential recovery needs a durable return path after transient feedback ends.

## Inspect the real window

Use available native automation or computer-use tools and their runbook.
Agentdesk/`desktop`, when available, covers macOS observation, not every desktop
platform. Use the appropriate Windows/Linux route for those targets.

Verify screenshots, accessibility names/state, and real input together. An AX
node or successful command does not prove a control is visible, unclipped, or
clickable. Measure input-to-visible response at realistic data sizes when
latency is the defect. Record app/build, window dimensions, state, and observed
sequence. For WebViews, confirm shell focus, IME, resizing, and packaged assets
in addition to browser-level behavior.

Platform entrypoints: [Apple Design](https://developer.apple.com/design/) and
[Windows app design](https://learn.microsoft.com/en-us/windows/apps/design/).
Consult the current toolkit's own guidance for other desktop targets.
