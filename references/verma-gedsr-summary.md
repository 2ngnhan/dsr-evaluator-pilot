# Verma 2026 — Generative echeloned DSR (GeDSR)

Reference: Verma, D., Terziyan, V., Tuunanen, T., & Shukla, A. K. (2026).
Toward an artifact that designs itself: generative design science research
approach. *AI and Ethics*, 6:104.
https://doi.org/10.1007/s43681-025-00965-5

## What the paper does

Verma et al. 2026 propose an adaptation of the echeloned design science
research (eDSR) methodology — originally from Tuunanen — for the case where
the AI system being designed is itself capable of design, audit, and
evolution. They call this Generative eDSR or GeDSR.

The motivating context is autonomous AI that must self-regulate within
ethical constraints. The paper aligns its scope with regulatory frameworks
(EU AI Act, NIST AI RMF, ISO/IEC 23053, 42001).

## The four echelons

Each echelon produces an intermediate artifact with explicit gate evidence
that must be satisfied before progression to the next echelon.

| Echelon | Name | Produces | Gate evidence |
|---|---|---|---|
| 1 | Responsible Autonomy | ethical-constraint models | stress tests for constraint robustness |
| 2 | Self-Explainability | explanation-faithfulness audits | quantitative measures of explanation fidelity |
| 3 | AI Bootstrapping | self-refinement logs, capability improvement regressions | performance stability bounds |
| 4 | KIML (Knowledge-Informed Machine Learning) | integrated domain-knowledge models | consistency checks and alignment audits |

The four-echelon pipeline is traceable: each gate produces an evidence
artifact that the next echelon depends on, so progression is empirically
grounded rather than designer-judgment.

## eDSR origin (Tuunanen)

The "echelon" concept comes from Tuunanen's eDSR work, which extends Peffers
DSRM with modular layers for managing design complexity across iterative
build-evaluate cycles. Verma et al. adapt this for AI systems that must
learn, explain, and govern themselves.

## AI-as-a-User-of-AI

A core concept from the paper. AI systems behave as collaborative entities
that engage in structured dialogues with other AI systems to refine
decisions and enforce ethical alignment. Unlike traditional human-in-the-loop
oversight, AI agents critique each other.

Note Verma's careful framing: "AI systems are not attributed agency,
intentionality, or moral reasoning. Terms such as critique, evaluation, or
judgment refer to algorithmic assessments performed according to
human-defined rubrics and constraints, not to autonomous moral
deliberation."

This template inherits that framing. Our judge panel performs algorithmic
assessment against human-curated rubrics; it does not "decide" in any moral
sense.

## What this template borrows

- The principle of intermediate artifacts gated by evidence.
- The principle of multiple judging perspectives (Verma's AI-to-AI
  collaboration is realized here as a cross-model judge panel).
- The framing that AI assessments are rubric-following, not deliberative.

## What this template explicitly does NOT use

Verma's four echelons (Responsible Autonomy / Self-Explainability / AI
Bootstrapping / KIML) are **not adopted** in this template.

**Reason.** Verma's echelons are domain-specific to *AI that designs itself
ethically*. Our input artifact is a generic DSR project (MBA capstone,
practitioner framework), not an autonomous AI system. The four echelons
would force-fit a structure that doesn't match the project class.

Instead this template uses **Peffers x Dim** — six Peffers phases crossed
with six rigor dimensions — as the gating structure. This matches the
generic DSR class better.

## Why we keep the spirit

The methodological innovations from GeDSR that this template DOES use:

- **Gate evidence per echelon -> gate evidence per phase.** Each Peffers
  phase produces a packet that the gate-evaluator scores.
- **Modular interface contracts.** Each agent's output has a defined shape
  that the next agent consumes.
- **Empirically grounded promotion.** k >= 0.60 promotes, k < 0.60 routes
  to human. Promotion is data-driven, not designer-judgment.

## Citing this paper in your own work

If you build on this template for an MBA capstone or paper, cite Verma et
al. 2026 alongside Peffers 2007 and vom Brocke & Maedche 2019.

## TEMPLATE placeholders

- `n/a (fill if quoting directly)` — the
  template cites the paper at the abstract / introduction level. For
  specific quotes, get page numbers from the PDF.
