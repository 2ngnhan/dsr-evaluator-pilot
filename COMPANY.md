---
schema: agentcompanies/v1
kind: company
slug: dsr-evaluator-pilot
name: DSR Evaluator (Pilot)
description: >
  Evaluates and co-creates Design Science Research projects from ignition point
  to contribution claim, across 6 Peffers phases x 6 rigor dimensions, with a
  cross-model judging panel and human-reviewable gate evidence. For MBA capstone
  candidates and DSR practitioners.
version: 0.1.0
license: MIT
tags:
  - dsr
  - mba-capstone
  - research-methodology
  - generative-edsr
metadata:
  primary_language: en
  secondary_language: vi
  target_audience: mba-capstone-students,dsr-practitioners
  parent_org: VinUniversity MBA
  approval_required: true
---

## Terminology: Phase ≠ Step (READ FIRST)

**Phase N** = a Peffers DSRM phase. Six total: 1=Discovery, 2=Objectives & Requirements, 3=Design & Development, 4=Demonstration, 5=Evaluation, 6=Communication.

**Step N** = a sub-unit *within Phase 1 Discovery only*. Five total: 1=Deconstruct, 2=Literature scan, 3=Adversarial verify, 4=Gap construction, 5=Grid populate.

When creating subtasks or hand-off messages, ALWAYS use the form `Phase 1 Step <N>: <name>` (e.g. `Phase 1 Step 2: Literature Scan`). NEVER use `Phase <N>: <name>` for Phase 1 sub-units — that collides with the real Phase 2 (Objectives), which comes only AFTER Phase 1 produces an approved gap statement.

# DSR Evaluator

A company of 27 agents that walks a Design Science Research project from a
vague practitioner intuition ("ignition point") through the full Peffers DSRM
six-phase lifecycle, producing reviewable artifacts at every phase. Each
phase is evaluated against the dimensions that matter for that phase by a
panel of three independent LLM judges, with Cohen's kappa as the agreement
metric. Disagreement routes to a human; agreement promotes the artifact to
the next phase.

This template is intended for VinUniversity MBA capstone candidates and DSR
practitioners. Bilingual output (English primary, Vietnamese summary) is
mandatory on all phase-final deliverables and human-facing gate evidence.

## Charter

The company does three things, in order:

1. **Discovery (Phase 1).** Take an ignition point string in. Produce a
   DSR-compliant gap statement plus Vom Brocke Cells 1, 4, 5. This phase
   alone is a complete deliverable for capstone Chapter 1 / 2 scaffolding.
2. **Build (Phases 2-4).** Co-create objectives, design, and demonstration
   artifacts, with the human author doing the actual creative work and the
   agents enforcing rigor.
3. **Evaluate and publish (Phases 5-6).** Stress-test the artifact across
   five Hevner evaluation axes and produce a sharp, falsifiable contribution
   claim with academic and practitioner versions.

**Target audience.** VinUniversity MBA capstone candidates working on
artifact-oriented projects (frameworks, models, tools, systems), and DSR
practitioners outside the academy who need rigor scaffolding.

**Scope.** The company does not collect field data on behalf of the human.
It surfaces what data the human must collect, then ingests that data once
collected. It does not publish to journals or write Chapter prose; it
produces structured artifacts that feed into human-authored prose.

## Input / Output

**Input.** A single ignition point string from the human, e.g. "Effort-based
management is not effective anymore — we need a new approach."

**Output (Phase 1 standalone).** A bilingual deliverable containing:

- DSR-compliant gap statement (problem, context, evidence, gap,
  falsification, motivation).
- Vom Brocke Cell 1 (Problem), Cell 4 (Input Knowledge), Cell 5 (Key
  Concepts as cross-cutting vocabulary).

**Output (full lifecycle).** Progressive artifacts across all six phases,
each gated by cross-model judge panel. Phase-final deliverables and gate
evidence packets are bilingual; internal intermediate artifacts are English
only.

## Architecture — Peffers x Dim matrix

Six Peffers phases on rows, six rigor dimensions on columns. `*` marks the
dimensions actively scored in that phase. Every phase scores at least one
dimension; Phase 5 (Evaluation) scores all six because evaluation is the
phase where rigor claims are stress-tested.

```
                  01 falsi   02 tech   03 design   04 scope   05 novel   06 reliv
P1 Discovery         *                              *
P2 Objectives        *        *         *
P3 Design                     *         *
P4 Demonstration                                    *
P5 Evaluation        *        *         *           *          *          *
P6 Communication                                               *          *
```

Legend: `*` = active dimension (judge panel scores it). Empty = inactive
in that phase. Active matrix per phase:

- P1: {01 falsifiability, 04 scope}
- P2: {01 falsifiability, 02 technical, 03 design}
- P3: {02 technical, 03 design}
- P4: {04 scope}
- P5: all six
- P6: {05 novelty, 06 relevance}

## Cross-model judging panel

Three independent judges score each phase deliverable against the active
dimensions for that phase, using the rubrics in
[references/dim-framework.md](references/dim-framework.md):

```
judge-gemini-pro    (adapter: gemini-local,  model: gemini-2.5-pro)
judge-deepseek      (adapter: codex-local,    model: deepseek/deepseek-r1, routed via OpenRouter)
```

The `gate-evaluator` agent computes Cohen's weighted kappa across the two
judge score sets using the [`cohens-kappa`](skills/cohens-kappa/SKILL.md)
skill. `k >= 0.60` promotes the artifact to the next phase; `k < 0.60` routes
to the human `disagree-resolver` (the human author, in this template).

## Org structure

```
discovery-orchestrator  (gemini-2.5-pro)             // Phase 1 lead
|
+-- ignition-deconstructor    (gemini-2.5-pro)       // Step 1
+-- literature-scanner        (gemini-2.5-flash)     // Step 2
+-- adversarial-verifier      (claude-opus-4-7)      // Step 3 — cross-model
+-- gap-constructor           (gemini-2.5-pro)       // Step 4
+-- grid-populator            (gemini-2.5-pro)       // Step 5

Phase 2 — Objectives:
  objectives-formulator       (gemini-2.5-pro)
  metric-designer             (gemini-2.5-pro)
  kernel-theory-mapper        (gemini-2.5-pro)

Phase 3 — Design:
  artifact-classifier         (gemini-2.5-pro)
  design-principle-extractor  (gemini-2.5-pro)
  alternative-explorer        (gemini-2.5-pro)

Phase 4 — Demonstration:
  demo-protocol-designer      (gemini-2.5-pro)
  case-context-mapper         (gemini-2.5-pro)
  protocol-vs-delivery-checker (gemini-2.5-pro)

Phase 5 — Evaluation:
  eval-strategy-engine        (gemini-2.5-pro)
  instrument-validator        (gemini-2.5-pro)
  efficacy-analyzer           (gemini-2.5-pro)
  utility-assessor            (gemini-2.5-pro)
  generalization-prober       (gemini-2.5-pro)

Phase 6 — Communication:
  contribution-claim-writer   (gemini-2.5-pro)
  audience-translator         (gemini-2.5-pro)
  novelty-articulator         (gemini-2.5-pro)

Cross-cutting (gate panel):
  judge-gemini-pro            (gemini-2.5-pro)
  judge-deepseek              (deepseek-r1 via OpenRouter)
  gate-evaluator              (gemini-2.5-pro)
```

## Phase-by-phase responsibility

### Phase 1 — Discovery

| Step | Agent makes | Human makes |
|---|---|---|
| 1 Deconstruct | hidden-assumption list, falsifiable sub-claims | confirms scope decisions |
| 2 Literature scan | strength-tagged evidence list | none |
| 3 Adversarial verify | hallucination flags, contested-vs-accepted split | spot-checks top 3 sources directly |
| 4 Gap statement | bilingual gap statement (5 criteria met) | reads, confirms or asks for revision |
| 5 Grid populate | Cells 1 / 4 / 5 populated, bilingual | approves Phase 1 exit |

### Phase 2 — Objectives

| Agent | Makes | Human |
|---|---|---|
| objectives-formulator | falsifiable "if-then-measured-by" objectives | picks primary objective |
| metric-designer | measurement instruments per objective | sanity-checks feasibility |
| kernel-theory-mapper | justificatory knowledge mapping (Gregor #6) | confirms theory fit |

### Phase 3 — Design

| Agent | Makes | Human |
|---|---|---|
| artifact-classifier | construct / model / method / instantiation tag | confirms or contests |
| design-principle-extractor | principles with theory traces | adds principles agents miss |
| alternative-explorer | 2-3 plausible alternatives with rationale | picks which to seriously consider |

### Phase 4 — Demonstration

| Agent | Makes | Human |
|---|---|---|
| demo-protocol-designer | who-uses-what-doing-what-measured-how protocol | confirms feasibility |
| case-context-mapper | scope and boundary description | names the actual case |
| protocol-vs-delivery-checker | flags "this is delivery, not demonstration" | resolves flags |

### Phase 5 — Evaluation

| Agent | Makes | Human |
|---|---|---|
| eval-strategy-engine | Venable axes selection + method | approves strategy |
| instrument-validator | validity and reliability checks per metric | runs validation if needed |
| efficacy-analyzer | outcomes vs baseline (only if data exists) | provides field data |
| utility-assessor | data-collection plan (NOT data) | collects from field |
| generalization-prober | stress tests outside original context | optional follow-up |

### Phase 6 — Communication

| Agent | Makes | Human |
|---|---|---|
| contribution-claim-writer | sharp falsifiable contribution claim | approves the wording |
| audience-translator | academic + practitioner versions, both bilingual | picks venue / channel |
| novelty-articulator | positioning matrix vs existing work | confirms positioning is accurate |

## Skills attached

- [`dim-falsifiability-check`](skills/dim-falsifiability-check/SKILL.md) —
  enforces Dim 01: explicit measurement, contradiction-possible, scope-bounded.
- [`dim-technical-check`](skills/dim-technical-check/SKILL.md) — Dim 02:
  validity, reliability, sensitivity, replicability, instrument fit.
- [`dim-design-check`](skills/dim-design-check/SKILL.md) — Dim 03: principle
  rationale, theory-traced, alternatives, coherence, mutability.
- [`dim-scope-check`](skills/dim-scope-check/SKILL.md) — Dim 04: boundary
  explicit, out-of-scope named, applicability and failure conditions.
- [`dim-novelty-check`](skills/dim-novelty-check/SKILL.md) — Dim 05:
  positioning evidence, no rediscovery, falsifiable contribution claim.
- [`dim-relevance-check`](skills/dim-relevance-check/SKILL.md) — Dim 06:
  practitioner evidence, real-problem, stakeholder named, utility measurable.
- [`cohens-kappa`](skills/cohens-kappa/SKILL.md) — weighted kappa over N
  judges x M items x 1-5 ordinal scores, with interpretation.
- [`grid-6cell-populator`](skills/grid-6cell-populator/SKILL.md) — Vom Brocke
  6-cell grid with the Cell 5 cross-cutting vocabulary rule.
- [`bootstrap-guardrail`](skills/bootstrap-guardrail/SKILL.md) — refuses to
  operate if any rigor reference file is empty or TEMPLATE-only.

## References

- [`verma-gedsr-summary.md`](references/verma-gedsr-summary.md) — Verma et
  al. 2026 GeDSR paper summary (four echelons, eDSR origin, AI-as-a-User-of-AI).
- [`peffers-dsrm-stages.md`](references/peffers-dsrm-stages.md) — Peffers et
  al. 2007 DSRM six-phase model.
- [`hevner-eval-axes.md`](references/hevner-eval-axes.md) — Venable et al.
  FEDS axes and Hevner 2004 evaluation table.
- [`vom-brocke-6grid.md`](references/vom-brocke-6grid.md) — Vom Brocke and
  Maedche DSR Grid with cross-cutting Cell 5.
- [`workshop-discovery-workflow.md`](references/workshop-discovery-workflow.md)
  — the verbatim 5-step Discovery workflow that Phase 1 implements.
- [`dim-framework.md`](references/dim-framework.md) — Dim 01-06 definitions,
  rubrics, score interpretation, active-matrix table.
- [`bootstrap-circularity-note.md`](references/bootstrap-circularity-note.md)
  — why the rigor rubrics are human-curated and read-only.

## Governance

| Action | Approval level |
|---|---|
| Generate intermediate internal artifacts | none — agents proceed |
| Generate phase-final deliverable | judge panel + gate-evaluator |
| Promote artifact to next phase (k >= 0.60) | gate-evaluator auto |
| Override gate-evaluator decision | human only |
| Modify any file in `references/` | human only — agents are read-only |
| Use `claude-local` or `codex-local` adapter when not registered | DEGRADED fallback to `gemini-local` + `gemini-2.5-flash`, flag in packet |
| Publish anywhere outside this company workspace | human only |

## Output language convention

All phase-final deliverables and human-facing gate evidence packets use this
structure verbatim:

```
## English (primary)
<full artifact content in English>

## Tiếng Việt (summary)
<100-200 word Vietnamese summary>
```

Established terms (DSR, Peffers, Hevner, eDSR, GeDSR, falsifiability, kernel
theory, Cohen's kappa, etc.) are not translated in the Vietnamese summary.

Internal intermediate artifacts (e.g., literature-scanner output passed to
adversarial-verifier) may be English-only — the bilingual rule applies only
to outputs that reach the human or close a phase gate.

The `audience-translator` agent translates across audiences (academic <->
practitioner), not across languages. Both audience versions must themselves
be bilingual EN + VI.

## Stack constraint note — cross-model judging

The cross-model judge panel requires `claude-local` and `codex-local` adapters
to be registered in the n-clerk runtime. If either is missing at run time,
the affected judge agent falls back to `gemini-local` + `gemini-2.5-flash`
with a prompt-family variance trick, and emits a `DEGRADED` flag.

When the panel runs in `DEGRADED` mode, the gate evidence packet states
prominently:

> DEGRADED: same-provider judging — Cohen's kappa from this run is not
> cross-model valid.

A human must approve any promotion that occurred under `DEGRADED` mode.

To register the missing adapters, see the n-clerk infra repo's adapter
registration docs and patch the Dockerfile to install `@anthropic-ai/sdk`
and `openai` for the `claude-local` and `codex-local` adapters respectively.

## Bootstrap circularity guardrail

The rigor rubrics in `references/dim-framework.md`, the discovery workflow
in `references/workshop-discovery-workflow.md`, and the Verma summary in
`references/verma-gedsr-summary.md` are the ground truth this company
evaluates against. If those files were themselves AI-generated and not
human-curated, the entire evaluation chain is circular — the AI would be
grading its own homework against rules another AI invented.

The [`bootstrap-guardrail`](skills/bootstrap-guardrail/SKILL.md) skill
refuses operation when any of those files is empty or still showing
TEMPLATE placeholders. See
[`references/bootstrap-circularity-note.md`](references/bootstrap-circularity-note.md)
for the full argument.

Agents in this company are **read-only with respect to `references/`**.
They may consult those files but never write to them.

## What to customize when instantiating

When you copy this template into a real capstone repo:

1. Fill in [`references/dim-framework.md`](references/dim-framework.md) —
   replace every `<REPLACE: ...>` placeholder with a real threshold and rubric.
2. Fill in [`references/workshop-discovery-workflow.md`](references/workshop-discovery-workflow.md)
   if you want to adapt the 5-step workflow for a non-MBA context (the
   default targets MBA capstone scope).
3. Set `ANTHROPIC_API_KEY` and `OPENAI_API_KEY` in n-clerk env. Dockerfile already installs `@anthropic-ai/claude-code` and `@openai/codex` CLIs (lines 44-48); `claude-local` and `codex-local` adapters are bundled in upstream Paperclip. Without the env keys, those adapters fail and the panel runs DEGRADED.
4. Add project-specific vocabulary to a new file `references/project-vocab.md`
   (the `grid-populator` will read it when populating Cell 5).
5. Edit `agents/discovery-orchestrator/AGENTS.md` to point at the actual
   ignition point for your project.
