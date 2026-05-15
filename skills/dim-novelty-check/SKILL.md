---
name: dim-novelty-check
description: >
  Enforces Dim 05 (Novelty) on contribution claims and positioning. Use
  during Phase 6 (Communication). A contribution is novel if it is
  positioned against existing work with evidence, not asserted.
---

# Dim 05 — Novelty check

**Source of truth.** [`references/dim-framework.md`](../../references/dim-framework.md)
section "Dim 05 — Novelty".

## Enforcement rules

- **N1.** Positioning evidence. Prior work that the contribution differs
  from is named — with citations, not "as is common in the literature".
- **N2.** Existing work acknowledged. The artifact's domain has prior
  work; pretending it doesn't is a fast path to a reviewer telling you it
  does. Acknowledge the closest existing artifact even when defending
  novelty against it.
- **N3.** Differentiation on a named dimension. "We are different in some
  way" is not novelty. "We differ in metric M, which prior work P does not
  address" is.
- **N4.** No rediscovery. The contribution is not already in the
  literature under another name. The novelty-articulator must search for
  near-synonyms before claiming novelty.
- **N5.** Contribution claim falsifiable. Could a future paper prove the
  contribution is null (e.g., by showing the artifact is no better than a
  baseline that already exists)? If no, the claim is too vague.

## When this skill is consumed

Phase 6: contribution-claim-writer applies N5 to the contribution claim
itself; novelty-articulator applies N1-N4 to the positioning matrix.

## Review checklist

- [ ] N1 — Prior work is cited and named.
- [ ] N2 — Closest existing artifact is acknowledged.
- [ ] N3 — Differentiation is on a named dimension.
- [ ] N4 — Near-synonym search was conducted.
- [ ] N5 — The contribution claim is falsifiable.

## Common failure patterns

- **"To the best of our knowledge, no prior work exists."** Almost always
  wrong; reviewers find prior work the author missed. Reject N1 / N2.
- **"Our approach is novel because it combines X and Y."** Combination
  itself is not novelty unless the combination produces a non-obvious
  capability. Reject N3.
- **Rediscovering a known concept under a new name.** Common in
  practitioner-driven research. Reject N4.
- **Vague contribution.** "We contribute insights into X" allows the
  contribution to be anything; reject N5.

## Refuse-if-empty

If `references/dim-framework.md` is empty or templates unfilled, halt.
