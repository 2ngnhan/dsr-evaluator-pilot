# Dim framework — six rigor dimensions

The dimensions are the *what* of evaluation. Peffers phases are the *when*.
The active-matrix table at the bottom of this file specifies which
dimensions are active in which phase.

Each dimension has:

- a one-line criterion,
- 5-7 rubric questions (each scored 1-5),
- score interpretation,
- the agents and skills that consume it.

The judge panel scores against the rubric questions. The gate-evaluator
aggregates with Cohen's kappa across the three judges.

## Score interpretation (applies to every dimension)

| Score | Meaning |
|---|---|
| 1 | Absent / not addressed |
| 2 | Mentioned but unresolved |
| 3 | Partially addressed, gaps remain |
| 4 | Substantively addressed, minor issues |
| 5 | Fully addressed, defensible to external reviewer |

A phase exits only if the average across all active dimensions is
`>= 3.5` AND no single rubric
question scores `< 2`.

## Dim 01 — Falsifiability

**Criterion.** A claim is falsifiable if there is a state of the world that
would prove it wrong, and that state can be detected with a defensible
measurement.

**Rubric questions.**

- F1. Is there an explicit measurement instrument for the claim?
- F2. Is contradiction logically possible (the claim is not tautological)?
- F3. Is the scope of the claim bounded (when does it apply, when not)?
- F4. Is the claim free of shifting goalposts (success criteria fixed
  in advance)?
- F5. Does the gap statement / objective state explicitly what would prove
  it wrong?

**Consumers.** Phase 1 (gap-constructor), Phase 2 (objectives-formulator),
Phase 5 (eval-strategy-engine). Skill: `dim-falsifiability-check`.

## Dim 02 — Technical rigor

**Criterion.** The measurement and evaluation machinery is psychometrically
sound and replicable.

**Rubric questions.**

- T1. Construct validity — does the instrument measure what it claims to?
- T2. Reliability — would the instrument produce similar results across
  runs / raters?
- T3. Sensitivity — can the instrument distinguish meaningful differences?
- T4. Replicability — is there enough method detail for another team to
  reproduce?
- T5. Instrument fit for purpose — is this the right kind of measurement
  for this kind of claim?

**Consumers.** Phase 2 (metric-designer), Phase 3
(design-principle-extractor — for theory tracing rigor), Phase 5
(instrument-validator). Skill: `dim-technical-check`.

## Dim 03 — Design coherence

**Criterion.** The artifact is a coherent realization of its principles,
and the principles are theory-traced.

**Rubric questions.**

- D1. Are design principles stated with rationale, not just description?
- D2. Is each principle traced to a kernel theory or empirical finding?
- D3. Were alternatives considered (not strawmen)?
- D4. Are the principles coherent across cells (no internal contradictions)?
- D5. Is mutability acknowledged — what could change without invalidating
  the artifact?

**Consumers.** Phase 2 (kernel-theory-mapper), Phase 3
(design-principle-extractor, alternative-explorer), Phase 5
(design fidelity axis). Skill: `dim-design-check`.

## Dim 04 — Scope / boundary

**Criterion.** The artifact's domain of applicability is explicit, including
where it works and where it fails.

**Rubric questions.**

- S1. Is the boundary of applicability stated explicitly?
- S2. Are out-of-scope contexts named (not just implied)?
- S3. Are conditions for applicability stated (what must be true for the
  artifact to help)?
- S4. Are conditions for failure stated (what would make it fail)?
- S5. Are generalization claims disciplined (not over-claimed)?

**Consumers.** Phase 1 (gap-constructor — bounding the problem), Phase 4
(case-context-mapper), Phase 5 (generalization-prober). Skill:
`dim-scope-check`.

## Dim 05 — Novelty

**Criterion.** The contribution is positioned against existing work with
evidence, not asserted.

**Rubric questions.**

- N1. Is positioning evidence given (named prior work)?
- N2. Is existing work acknowledged (not pretending the problem is new)?
- N3. Is differentiation on a named dimension (not "we're different in some
  way")?
- N4. Is there a "no rediscovery" check — confirming the contribution is
  not already in the literature under another name?
- N5. Is the contribution claim itself falsifiable (could a future paper
  prove the contribution is null)?

**Consumers.** Phase 6 (contribution-claim-writer, novelty-articulator).
Skill: `dim-novelty-check`.

## Dim 06 — Relevance

**Criterion.** The problem is real to practitioners, and the artifact's
utility is measurable.

**Rubric questions.**

- R1. Is there practitioner evidence the problem exists (not imagined by
  the researcher)?
- R2. Is the problem stated as something practitioners would recognize?
- R3. Are stakeholders named explicitly (who benefits, who is affected)?
- R4. Is an adoption path articulated (how does this get used)?
- R5. Is utility measurable (not just claimed)?

**Consumers.** Phase 5 (utility-assessor, generalization-prober), Phase 6
(audience-translator, novelty-articulator). Skill: `dim-relevance-check`.

## Active matrix — which dimensions are scored per phase

```
                  01 falsi   02 tech   03 design   04 scope   05 novel   06 reliv
P1 Discovery         *                              *
P2 Objectives        *        *         *
P3 Design                     *         *
P4 Demonstration                                    *
P5 Evaluation        *        *         *           *          *          *
P6 Communication                                               *          *
```

A phase that has only one active dimension still requires all three judges
to score independently (the kappa calculation needs N >= 3 raters minimum
to be meaningful, and N >= 10 items minimum to be stable — see
`cohens-kappa` skill).

For phases with very few rubric items, the gate-evaluator should pool items
across the active dimensions before computing kappa (so P1 pools F1-F5 + S1-S5
= 10 items, meeting the stability floor).

## TEMPLATE placeholders (you must fill before this template is operational)

- `3.5` — phase exit floor.
- `2` — no question may
  score below this even if the average passes.
- `0.60` — kappa below
  this routes to human disagree-resolver.
- `10` — below this,
  the kappa value is flagged as unstable.

The `bootstrap-guardrail` skill refuses operation if any of the above
placeholders are still unfilled.
