# Mobile: the device participates in the design

Establish iOS, Android, React Native, Flutter, or mobile web from project
evidence. Preserve its navigation and control conventions. For mobile web,
retain web semantics and also check the constraints below. Native SDK is a
specific toolkit, not a synonym for native mobile development.

## Shape the task around real use

- Prioritize the object, primary action, and recovery for the attention and
  reach available. Check one-handed use, grip, thumb reach, and occlusion when
  they affect the task. A desktop composition scaled down rarely suffices.
- Respect system navigation/back, modal dismissal, and return-to-work behavior.
  A custom gesture needs discoverability and an equivalent accessible outcome.
- Separate full-bleed backgrounds from safe content. Cutouts, system bars,
  keyboard, and physical orientation can change usable bounds independently.
- Use the platform's current target-size and spacing guidance for the actual
  toolkit. A CSS pixel, point, dp, and physical pixel are not interchangeable.
- Let long labels, localization, and larger text recompose the screen. Preserve
  essential meaning before shortening; avoid hiding recovery behind overflow.

## Own the complete gesture

For holds/drags, define acquisition, immediate feedback, ownership, commit,
cancellation, and release. Test pointer movement out, second touch, focus loss,
backgrounding, view removal/disable, and navigation away. Reappearing controls
must not inherit an old finger. Late acknowledgements must not reactivate a
canceled session; bind them to the interaction identity/generation.

Permission, preference, active capture, transport, and received output are
different facts. Show the states that change what the person should do. Keep
local input feedback distinct from confirmed remote completion.

Preserve drafts, selection, and useful content across lifecycle transitions as
the product promises. Retry a failed save without rerunning successful work.
Check keyboard entry/return, focus visibility, and scroll-to-field behavior.

## Accessibility and expression

Give controls meaningful names, roles, states, and reading order for VoiceOver
or TalkBack. Support text scaling and reduced motion. Pair essential state
with text/shape rather than color alone. Haptics and sound can reinforce an
accepted action; they cannot be its sole explanation. In voice products,
audition cues through actual capture paths for feedback into speech detection.

## Verify the actual target

Use the project's available device/emulator tooling. Record platform, device,
OS/build, orientation, text scale, content, and tested input path. Exercise the
specific lifecycle/gesture boundary, not only a simulated state transition.
Combine screenshots with observed interactions; browser emulation cannot prove
native back behavior, keyboard insets, or canceled capture. If device access is
missing, implement/inspect what is possible and state the unverified boundary.

Use current [Apple HIG](https://developer.apple.com/design/human-interface-guidelines/)
or [Android design guidance](https://developer.android.com/design/ui) for the
chosen target. Apply platform-specific conventions deliberately rather than
copying one operating system's geometry and gestures to another.
