# Design family release record

## 0.1.0 — 2026-09-29

Implemented six portable skills with bundled references for five surfaces,
official-first shadcn discovery, optional Shoogle and evidence-source routes,
state/gesture judgment, matched exploration, critique, and adoption.

Added a standard `skills/` collection layout, a design-family Claude marketplace
entry, cross-agent lifecycle documentation, and separate maintenance metadata.
This repository is the source owner for this and future families.

### Validation completed

- The standard installer discovers exactly six skills. Strict Claude marketplace
  validation reports no errors or warnings.
- Actual isolated project/global installation preserved complete bundle bytes
  and Claude links; removal succeeded. A single-leaf `--copy` install preserved
  its references without requiring sibling skills. Claude's plugin inventory
  listed exactly six skills, zero hooks, and zero MCPs.
- Codex 0.159.1 `skills/list` found all six, with no skill parsing errors, in a
  disposable project/profile. No model turn was needed for this catalog check.
- OpenCode 2.0.16 loaded all six skills in a fresh isolated session directly
  from `.agents/skills`, without native-directory copies or explicit config.
  Each resulting skill message's body matched the source. Activation used
  `resume: false`; the session retained zero model tokens and zero cost.
  Its cold standalone skill-list API had returned an empty catalog (including
  no built-ins); actual session activation supplied the decisive proof. A
  separate HTTP-server probe hit a health-compatibility error and was abandoned
  in favor of the supported standalone session API.
- Four paired planning-only model cases covered all five surfaces and standalone
  component selection. With skill: **17/17** assertions; baseline: **15/17**.
  The baseline was strong; two narrow handoff omissions and ambiguous compound
  rubric terms account for the entire difference. No broad quality improvement,
  actual-device outcome, timing, or cost advantage is established.
- Frontmatter identities, runtime-relative resource containment, metadata JSON,
  manifest membership, and documentation links checked successfully. Root skill
  body: 851 words; leaves: 553–622 words, before conditional references.
- The required fleet route map was updated at
  `../agentstart/skills/fleet/MAP.md`. Its documentation check passed. AgentStart's
  validation suite passed with canonical `TMPDIR`; the first run exposed its
  existing `/var` versus `/private/var` temporary-path comparison sensitivity.

See `validation.json` for packaging/native probe scope and `evals/results.json`
for the behavioral record. The generated local review viewer is
`design-workspace/iteration-1/review.html` (ignored workspace, human review
pending). Runtime files were not revised after this evaluation snapshot.

### Integration boundary

The operator confirmed that this repo should own skills and reusable connective
definitions, composed into personal Stack manager/worker roles. The next
discussion is captured in `docs/stack-integration-handoff.md`: verify additive
role amendments and resource bindings before implementing integration. The
authored collection is not a hosted release or live Role deployment.
