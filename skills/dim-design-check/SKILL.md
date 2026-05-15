---
name: dim-design-check
description: >
  Enforces Dim 03 (Design coherence) on design principles, theory tracing,
  and alternatives consideration. Use during Phase 3 (Design) and Phase 5
  (Evaluation of design fidelity). An artifact has design coherence if
  its principles are stated with rationale, traced to kernel theories,
  considered against alternatives, internally consistent, and mutability-
  aware.
---

# Dim 03 — Design coherence check

**Source of truth.** [`references/dim-framework.md`](../../references/dim-framework.md)
section "Dim 03 — Design coherence". Always read first.

## Enforcement rules

- **D1.** Principle rationale. Each design principle is stated with the
  reason it was chosen, not just the principle itself. "Principle: support
  uphill / downhill phases" without "because shape-up theory distinguishes
  exploration from commitment" rejects under D1.
- **D2.** Theory-traced. Each principle is traced to a kernel theory,
  prior empirical finding, or named design pattern. Untraced principles
  are intuition, not design.
- **D3.** Alternatives considered. At least 2-3 plausible alternative
  designs were surfaced. Alternatives must be plausible — strawmen reject
  under D3.
- **D4.** Coherence across cells. Principles in Cell 3 (Solution) align
  with the problem in Cell 1 and the input knowledge in Cell 4. If
  vocabulary differs (Cell 5 violation), reject D4.
- **D5.** Mutability acknowledged. What could change about the artifact
  without invalidating it? An artifact with no mutability statement is
  brittle — every detail is load-bearing by default, which is rarely true.

## When this skill is consumed

Phase 2: kernel-theory-mapper applies D2 to each objective's justificatory
knowledge. Phase 3: design-principle-extractor applies all of D1-D5;
alternative-explorer applies D3 specifically. Phase 5: design-fidelity
axis of FEDS applies D1-D5 to the final artifact.

## Review checklist

- [ ] D1 — Each principle has explicit rationale.
- [ ] D2 — Each principle traces to a kernel theory or named pattern.
- [ ] D3 — 2-3 plausible alternatives were considered and ruled out
       with reason.
- [ ] D4 — Principles are consistent across Cells 1, 3, 4, 5.
- [ ] D5 — Mutability is stated: what could change without invalidating
       the artifact.

## Common failure patterns

- **"Designed by intuition, theory added retroactively."** D2 fails when
  the theory citation feels like an afterthought. Symptom: the theory
  doesn't predict the principle, it merely permits it.
- **Strawman alternatives.** "We could also do X (which is obviously
  bad)" doesn't satisfy D3. The alternative must be plausible, defended
  by a reasonable practitioner, then ruled out with a real argument.
- **Cell 3 / Cell 5 drift.** The artifact uses "confidence" loosely while
  Cell 5 defines it precisely. D4 catches this.

## Refuse-if-empty

If `references/dim-framework.md` is empty or templates unfilled, halt
with the standard refusal.
