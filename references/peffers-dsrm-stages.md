# Peffers DSRM — six-phase process model

Reference: Peffers, K., Tuunanen, T., Rothenberger, M. A., & Chatterjee, S.
(2007). A Design Science Research Methodology for Information Systems
Research. *Journal of Management Information Systems*, 24(3), 45-77.

Peffers et al. 2007 turns Hevner's three-cycle model into an executable
process. The six phases are sequential in description but iterative in
practice — a project loops back to earlier phases when evaluation surfaces
problems.

This template treats the six phases as gates: each produces a phase-final
deliverable scored by the cross-model judge panel before the project moves
to the next phase.

## Phase 1 — Problem identification and motivation

- **Motivation.** A vague intuition is not yet a research problem.
  Practitioners feel pain; researchers state it falsifiably.
- **Deliverable.** A DSR-compliant gap statement plus Vom Brocke Cells 1, 4,
  5 (Problem / Input Knowledge / Key Concepts).
- **Gate criteria (Dim 01, 04).** Statement is falsifiable. Scope is
  explicit. Evidence is verified (not AI-hallucinated). Counter-arguments
  are acknowledged.

## Phase 2 — Define objectives of a solution

- **Motivation.** Without measurable objectives, the artifact has no way to
  fail and therefore no way to teach.
- **Deliverable.** A list of "if artifact X is used in context C, outcome Y
  will occur, measured by instrument M" statements. Each objective has a
  measurement instrument and a kernel theory it draws from.
- **Gate criteria (Dim 01, 02, 03).** Each objective is falsifiable. Each
  metric has documented validity / reliability. Theory backing is named.

## Phase 3 — Design and development

- **Motivation.** Building the artifact. Every design decision needs a
  reason; otherwise the artifact is craft, not research.
- **Deliverable.** Artifact classified (construct / model / method /
  instantiation per March & Smith 1995). Design principles extracted, each
  traced to a kernel theory. At least two alternative designs surfaced with
  rationale for the chosen one.
- **Gate criteria (Dim 02, 03).** Principles are coherent. Alternatives
  were considered, not strawmen. Mutability — what could change without
  invalidating the artifact — is acknowledged.

## Phase 4 — Demonstration

- **Motivation.** Show the artifact can be used to solve at least one
  instance of the problem. This is the first contact with reality.
- **Deliverable.** A protocol — who uses the artifact, in what context,
  doing what task, measured how. Scope and boundary are named explicitly.
- **Gate criteria (Dim 04).** Boundary is explicit. The protocol is
  demonstration (problem-solving with measurement), not delivery (using the
  artifact in production without evaluation lens).

## Phase 5 — Evaluation

- **Motivation.** Measure how well the artifact supports a solution.
  Compare to objectives from Phase 2.
- **Deliverable.** Evaluation strategy (which Venable et al. FEDS axes,
  what method, what comparators). Instrument validation. Efficacy analysis
  vs baseline. Utility assessment (what humans need to collect). Stress
  tests outside the original context.
- **Gate criteria (all six dims).** This is the phase where every rigor
  claim is stress-tested.

## Phase 6 — Communication

- **Motivation.** A contribution that is not communicated does not
  contribute. Both academic and practitioner audiences must receive it.
- **Deliverable.** A sharp, falsifiable contribution claim. Academic
  version and practitioner version, both bilingual EN + VI. Positioning
  matrix against existing work.
- **Gate criteria (Dim 05, 06).** Novelty is positioned, not asserted.
  Relevance is evidenced from practitioner contact, not assumed.

## Iteration

Peffers et al. explicitly state that the six phases are not strictly
linear. Real projects:

- loop back from Phase 5 (Evaluation) to Phase 3 (Design) when efficacy
  shortfalls indicate a design flaw;
- loop back from Phase 2 (Objectives) to Phase 1 (Problem) when objectives
  expose that the problem statement was too narrow;
- loop within Phase 5 when a single evaluation method is insufficient.

This template's gate-evaluator records loops and surfaces them in the
phase-final packet so the human can decide whether to iterate or proceed.

## Mapping to this template

| Peffers phase | Lead orchestrator (this template) | Active rigor dims |
|---|---|---|
| 1 Problem identification | discovery-orchestrator | 01, 04 |
| 2 Define objectives | objectives-formulator | 01, 02, 03 |
| 3 Design and development | artifact-classifier (de facto lead) | 02, 03 |
| 4 Demonstration | demo-protocol-designer | 04 |
| 5 Evaluation | eval-strategy-engine | all six |
| 6 Communication | contribution-claim-writer | 05, 06 |
