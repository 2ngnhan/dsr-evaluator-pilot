# Hevner evaluation axes + Venable FEDS

References:

- Hevner, A. R., March, S. T., Park, J., & Ram, S. (2004). Design Science
  in Information Systems Research. *MIS Quarterly*, 28(1), 75-105. Table 2
  on evaluation methods.
- Venable, J., Pries-Heje, J., & Baskerville, R. (2016). FEDS: A Framework
  for Evaluation in Design Science Research. *European Journal of
  Information Systems*, 25(1), 77-89.

DSR evaluation is multi-axis. A single "did it work?" check is insufficient.
This template selects axes per project from the FEDS framework and uses the
Hevner 2004 method table as a menu of how-to evaluate.

## The five FEDS-derived axes

This template scores each artifact along five axes during Phase 5. Phase
exit requires that each axis has a defensible method, not necessarily a
positive result.

1. **Instrument validity** — does the measurement actually measure what it
   claims to measure? (Construct validity, content validity, criterion
   validity.)
2. **Technical efficacy** — does the artifact perform its function under
   controlled conditions? (Internal validity.)
3. **Design fidelity** — is the artifact a coherent realization of its
   principles? Are principles traceable to theory?
4. **Purpose / utility** — does the artifact solve the problem for real
   stakeholders? (External validity, practitioner relevance.)
5. **Generalization** — does the artifact transfer outside its original
   context? Under what conditions does it fail?

## Mapping to Hevner 2004 Table 2 — methods

| Axis | Hevner method (excerpts) | Metric type |
|---|---|---|
| Instrument validity | Static analysis, structural testing | Coverage, completeness |
| Technical efficacy | Functional testing, performance testing | Pass/fail, latency, accuracy |
| Design fidelity | Architecture analysis, descriptive scenarios | Coherence score (judge panel) |
| Purpose / utility | Case study, field study, action research | Stakeholder reported utility, adoption rate |
| Generalization | Multiple case study, simulation | Coverage of contexts, stress-test pass rate |

## When to use which axis

| Project stage | Axes most likely active |
|---|---|
| Early prototype | Instrument validity, Technical efficacy |
| Maturing artifact | + Design fidelity |
| First field deployment | + Purpose / utility |
| Published artifact | All five, generalization most critical |

## FEDS strategy quadrant

Venable et al. distinguish four high-level strategies, plotted on two axes:

- **Naturalistic vs artificial** — real users in real context vs simulated.
- **Ex ante vs ex post** — before the artifact is built vs after.

| | Ex ante | Ex post |
|---|---|---|
| **Artificial** | Mathematical proofs, simulation, lab experiments | Lab experiments with prototype |
| **Naturalistic** | Pilot interviews, focus groups | Field study, case study, action research |

A complete DSR evaluation usually combines ex ante artificial (cheap,
catches obvious flaws) with ex post naturalistic (expensive, catches
real-world failures).

## What this template enforces

The `eval-strategy-engine` agent picks at least two cells from the FEDS
quadrant for Phase 5 evaluation — one ex ante, one ex post. If only one
cell is selected, the agent must justify why the other is infeasible.

The `instrument-validator` agent runs the **Instrument validity** axis on
every metric introduced in Phase 2 (Objectives).

The `efficacy-analyzer` and `utility-assessor` cover the next three axes.
`generalization-prober` covers the fifth.

## Common failure modes

- Reporting only ex post naturalistic ("we deployed it and people liked it")
  without ex ante validity work — confounds adoption with efficacy.
- Reporting only ex ante artificial ("the simulation worked") with no
  field contact — common in dissertation work, weak in publication review.
- Using one method for all axes — different axes need different methods.

## TEMPLATE placeholders

- `<REPLACE: minimum number of FEDS quadrant cells covered, default 2>` —
  the threshold below which Phase 5 cannot exit.
- `<REPLACE: minimum number of evaluation cycles before publication,
  default 2>` — many published DSR artifacts go through 2-4 build/eval
  cycles before final contribution.
