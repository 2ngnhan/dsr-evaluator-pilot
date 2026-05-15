---
name: dim-scope-check
description: >
  Enforces Dim 04 (Scope / boundary) on gap statements, case context
  descriptions, and generalization claims. Use during Phase 1, Phase 4,
  and Phase 5. An artifact's scope is rigorous if its domain of
  applicability is explicit, including where it works and where it fails.
---

# Dim 04 — Scope / boundary check

**Source of truth.** [`references/dim-framework.md`](../../references/dim-framework.md)
section "Dim 04 — Scope / boundary".

## Enforcement rules

- **S1.** Boundary explicit. The artifact / claim states the domain it
  applies to in named terms, not "modern contexts" or "knowledge work
  generally".
- **S2.** Out-of-scope named. Concrete contexts where the artifact does
  *not* apply are named, not just implied. "Not applicable to X" tells
  reviewers and adopters where to stop.
- **S3.** Conditions for applicability. What must be true about the
  context for the artifact to function? Team size, tooling, organizational
  culture, prior knowledge — name the preconditions.
- **S4.** Conditions for failure. What would make the artifact fail?
  Symmetric to S3 but harder to surface. Often discovered only through
  honest negative-case analysis.
- **S5.** Generalization claim disciplined. Claims about generalization
  are bounded by evidence. "Generalizes to other industries" without a
  cross-industry case rejects under S5.

## When this skill is consumed

Phase 1: gap-constructor scopes the problem itself. Phase 4:
case-context-mapper applies S1-S4 to the demonstration case. Phase 5:
generalization-prober applies S5 specifically to stress-test generalization
claims.

## Review checklist

- [ ] S1 — Domain is named in concrete terms.
- [ ] S2 — Out-of-scope contexts are explicitly listed.
- [ ] S3 — Preconditions for applicability are stated.
- [ ] S4 — Failure conditions are stated.
- [ ] S5 — Generalization claims are bounded by evidence.

## Common failure patterns

- **"Works for modern knowledge work."** Unbounded. Reject S1.
- **"Applicable to any team."** No team is "any team". Reject S1 and S2.
- **No failure conditions stated.** Suggests the author has not stress-
  tested mentally. Reject S4.
- **Generalizes from one case to "any organization."** N=1 evidence does
  not support general claims. Reject S5.

## Refuse-if-empty

If `references/dim-framework.md` is empty or templates unfilled, halt.
