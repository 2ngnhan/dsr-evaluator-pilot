# Bootstrap circularity — the problem and how this template prevents it

## The problem

If an AI judges DSR artifacts against rubrics, and the rubrics themselves
were authored by an AI, then the evaluation is circular. The AI is grading
its own homework against rules another AI invented. Two specific failure
modes follow:

1. **Rubric-AI bias.** If the rubrics were authored by GPT-4 (say), and
   the judge is also GPT-4, the rubric is implicitly tuned to what GPT-4
   considers "rigorous." Anything outside GPT-4's frame of reference is
   automatically marked low. A genuinely novel contribution that uses a
   methodology unfamiliar to GPT-4 will fail the rubric on form rather
   than on substance.
2. **No ground truth.** Validating an AI judge against another AI grader
   produces no information — they share training data. Without a
   human-curated gold standard, the "validation" is consensus, not
   correctness. A confident wrong consensus is worse than no judgement at
   all.

## Why this matters specifically for DSR

DSR rigor criteria (falsifiability, novelty, etc.) are themselves *opinions*
of the IS / methodology community. They are not natural laws. Hevner,
Peffers, vom Brocke, and Tuunanen disagree on emphasis. A human curator
must decide which version of "rigor" applies to a given capstone or paper.

If we let an AI decide, the AI will default to a consensus version that
exists in its training data — which may not match the version your advisor
or external reviewer expects.

## How this template prevents the problem

Three structural safeguards:

### Safeguard 1 — Human-curated rubrics, read-only to agents

The files in `references/` are the rigor ground truth. They were authored
by a human (Nguyen Ngoc Nhan, with the workshop content as substrate) and
remain under human control. Agents in this company are **read-only with
respect to references/**.

If an agent surfaces a useful rubric improvement during operation, the
agent must flag it as a suggestion to the human; the agent never edits
the file directly.

### Safeguard 2 — Cross-model judge panel

Three judges from two model families (Gemini, Claude, GPT) score
independently. If they agree (Cohen's kappa >= 0.60), agreement is
meaningful because they don't share weights. If they disagree (kappa <
0.60), the artifact routes to a human — agreement was the only signal
worth acting on.

A same-provider panel (both judges = Gemini) gives a kappa value but
the value is uninformative — it measures how consistent a model is with
itself, not how rigorous the artifact is. The `gate-evaluator` emits a
DEGRADED flag in that case.

### Safeguard 3 — `bootstrap-guardrail` skill

The `bootstrap-guardrail` skill (see
[`skills/bootstrap-guardrail/SKILL.md`](../skills/bootstrap-guardrail/SKILL.md))
refuses to operate if any of these files is empty or still showing
TEMPLATE placeholders:

- `references/dim-framework.md` — the rubrics themselves
- `references/workshop-discovery-workflow.md` — the Phase 1 workflow
- `references/verma-gedsr-summary.md` — the methodological grounding

The skill runs at every agent's startup. If any file is unfilled, the
agent halts and emits a message asking the human to curate the
reference before continuing.

## What this template does NOT claim

This template does not solve the bootstrap problem in general. It mitigates
it for a specific class of project (DSR capstones following Peffers DSRM)
by:

- having a human author the rigor ground truth once at template-fill time,
- isolating cross-model judges so panel agreement is informative,
- refusing to operate when the ground truth is suspicious (empty / template).

Any further mitigation requires extending the human-curated portion. For
example, when this template is used for a project in a domain the workshop
content does not cover, the human should add a domain-specific rubric
addendum to `references/dim-framework.md` before running.

## What the AI-judge ecosystem does NOT replace

- An external human reviewer in a capstone defense or peer review.
- A subject-matter expert checking novelty claims in a niche domain.
- The author's own conviction about what the artifact is.

The judges and the gate-evaluator are scaffolding for rigor, not substitutes
for judgment. Their highest-value output is consistent disagreement: when
three independent models agree something is wrong, that signal is hard to
get any other way.

## References

- Lyon, A. (2025). Bootstrapping bias in AI-evaluated AI work. (See also
  related work on circular validation in ML evaluation.)
- See `references/verma-gedsr-summary.md` for Verma's framing on
  AI-as-a-User-of-AI — which deliberately scopes AI agents to rubric-
  following rather than autonomous judgment.
