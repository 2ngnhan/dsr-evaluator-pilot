---
name: dim-technical-check
description: >
  Enforces Dim 02 (Technical rigor) on measurement instruments, evaluation
  methods, and design tracing. Use when drafting metrics, validating
  instruments, or reviewing technical claims. A claim has technical rigor
  if the measurement and evaluation machinery is psychometrically sound
  and replicable.
---

# Dim 02 — Technical rigor check

**Source of truth.** [`references/dim-framework.md`](../../references/dim-framework.md)
section "Dim 02 — Technical rigor". Always read that file first.

If `references/dim-framework.md` is empty or shows TEMPLATE placeholders,
refuse and ask the human to fill it. The `bootstrap-guardrail` skill runs
the empty-check.

## Enforcement rules

- **T1.** Construct validity. The instrument measures what it claims to
  measure, not a proxy that drifts. Operationalization is explicit:
  "delivery confidence" is measured by *what specific items, scored how*.
- **T2.** Reliability. Repeating the measurement on the same subject /
  artifact yields similar results. For self-report instruments,
  test-retest. For rater judgments, inter-rater agreement (kappa or ICC).
- **T3.** Sensitivity. The instrument can distinguish meaningful
  differences. A 5-point Likert that yields all 4s and 5s in pilot data
  has no sensitivity and rejects under T3.
- **T4.** Replicability. Another team could reproduce the measurement
  from the documented method. If the prompt template, scoring rules, and
  scoring rater training are not specified, reject under T4.
- **T5.** Instrument fit for purpose. The kind of measurement matches the
  kind of claim. A behavioral claim wants behavioral measurement, not
  self-report; a feasibility claim wants execution data, not survey.

## When this skill is consumed

Phase 2: metric-designer applies T1-T5 to each metric defined for each
objective. Phase 3: design-principle-extractor checks T4 (replicability)
on traced theory references. Phase 5: instrument-validator runs the full
T1-T5 check on every metric used in evaluation.

## Review checklist

- [ ] T1 — Construct validity is documented (operationalization explicit).
- [ ] T2 — Reliability is documented (test-retest, inter-rater, or
       internal consistency).
- [ ] T3 — Sensitivity is established in a pilot (no ceiling / floor
       effects).
- [ ] T4 — Method is replicable from the documentation alone.
- [ ] T5 — Instrument matches the kind of claim being made.

## Common failure patterns

- **Inventing a new instrument for a measurement that has a validated one.**
  Reject under T5: use the validated instrument unless there is a stated
  reason it is unfit.
- **Using "expert judgment" as the only validation.** Subject to rater
  bias; reject T2 unless inter-rater agreement is reported.
- **Self-report for behavior.** Self-report measures *attitude about
  behavior*, not behavior. Reject T5 if behavioral claims rest on
  self-report.

## Refuse-if-empty

If `references/dim-framework.md` is empty or templates unfilled, halt and
post the standard refusal message.
