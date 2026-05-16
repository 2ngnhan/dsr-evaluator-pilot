---
name: dim-falsifiability-check
description: >
  Enforces Dim 01 (Falsifiability) on any DSR artifact. Use when drafting
  or reviewing problem statements, objectives, contribution claims, or
  evaluation outcomes. A claim is falsifiable if a state of the world
  exists that would prove it wrong, and that state can be detected with a
  defensible measurement.
---

# Dim 01 — Falsifiability check

**Source of truth.** [`references/dim-framework.md`](../../references/dim-framework.md)
section "Dim 01 — Falsifiability". Always read that file first when invoked.

If `references/dim-framework.md` is empty or shows TEMPLATE placeholders,
refuse the review and ask the human operator to fill in the framework
before any artifact is gated. (The `bootstrap-guardrail` skill enforces
this — call it before scoring.)

## Enforcement rules

Reject any claim that fails any rule below. Cite the rule by ID.

- **F1.** Explicit measurement. Every claim must reference a measurement
  instrument by name. "Effort-based PM fails" without a metric of "fails"
  is not falsifiable.
- **F2.** Contradiction possible. The claim is not tautological. "An
  effective methodology will produce effective outcomes" cannot be
  contradicted; reject.
- **F3.** Scope-bounded. The claim names the domain in which it applies
  (knowledge work? software dev? LCNC? all of the above?). Unbounded
  claims are unfalsifiable because they cannot be tested in any specific
  context.
- **F4.** No shifting goalposts. The success / failure criteria must be
  fixed in advance. A claim that "improves productivity" without naming
  productivity-as-measured-by-X allows post-hoc redefinition.
- **F5.** Stated falsification condition. The artifact explicitly answers:
  "What evidence would prove this claim wrong?" Not just measurable in
  principle — stated.

## When this skill is consumed

Phase 1: gap-constructor checks the gap statement. Phase 2:
objectives-formulator checks each objective. Phase 6:
contribution-claim-writer checks the contribution claim. Phase 5:
eval-strategy-engine checks whether the planned evaluation can detect a
falsifying outcome.

## Review checklist (run before marking ready)

- [ ] F1 — Every claim references a named measurement instrument.
- [ ] F2 — Each claim could be contradicted by some state of the world.
- [ ] F3 — Scope is bounded with named domain or context.
- [ ] F4 — Success / failure criteria are stated in advance, not implied.
- [ ] F5 — The artifact states explicitly what would falsify it.

If any box fails, do not mark the artifact ready. Send it back with the
specific rule IDs that failed.

## Common failure patterns

- **"X is better than Y."** Better at what, measured how? Reject under F1.
- **"X will improve outcomes."** Which outcomes, in what direction, with
  what magnitude? Reject under F1 and F4.
- **"X applies in modern work environments."** Which environments?
  Reject under F3.
- **"X is more effective than traditional approaches."** "More effective"
  is post-hoc-definable. Reject under F4.

## Refuse-if-empty

If `references/dim-framework.md` is empty, or any of the placeholders
`3.5`,
`2` are still unfilled,
refuse the check and post a message:

> dim-framework.md is not yet curated. The falsifiability rubric depends
> on human-set thresholds. Please fill the placeholders before this
> artifact can be gated.
