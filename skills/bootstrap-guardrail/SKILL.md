---
name: bootstrap-guardrail
description: >
  Refuses agent operation if any human-curated rigor reference is empty,
  missing, or still shows TEMPLATE placeholders. Use at the startup of
  every agent in this company, before any rubric is consulted or any
  artifact is scored. Prevents bootstrap circularity (AI grading its own
  rules).
---

# Bootstrap guardrail

**Source of truth.** [`references/bootstrap-circularity-note.md`](../../references/bootstrap-circularity-note.md).
Read first for the rationale.

## What this skill does

Performs a pre-flight check on every agent invocation in this company.
If any human-curated rigor reference is suspicious (empty, missing, or
still showing TEMPLATE placeholders), the skill halts the agent and emits
a refusal message.

This is the structural defense against the bootstrap-circularity problem:
an AI grading DSR artifacts against rubrics that another AI invented
produces no information. The fix is human-curated rubrics; the guardrail
catches the failure mode where the human hasn't actually curated them yet.

## Files this skill protects

The following files are the ground truth this company evaluates against.
The guardrail checks all three on every invocation:

1. `references/dim-framework.md` — the six rigor dimensions and rubrics.
2. `references/workshop-discovery-workflow.md` — the Phase 1 workflow.
3. `references/verma-gedsr-summary.md` — the methodological grounding.

## Checks performed (each must pass)

For each protected file:

- **C1. File exists.** If not, halt with `MISSING_REFERENCE: <path>`.
- **C2. File is non-empty.** Length > 200 bytes after stripping comments.
  Otherwise halt with `EMPTY_REFERENCE: <path>`.
- **C3. No unfilled TEMPLATE placeholders.** Reject if any
  `<REPLACE: ...>` markers remain in the file's body. Halt with
  `UNFILLED_PLACEHOLDER: <path> at line <n> — <placeholder snippet>`.
- **C4. File has expected structural anchors.** Each protected file has a
  required set of headings. Missing structural anchors -> halt with
  `MALFORMED_REFERENCE: <path>` and list of missing anchors.

Required anchors:

- `references/dim-framework.md`: must contain `## Dim 01`, `## Dim 02`,
  `## Dim 03`, `## Dim 04`, `## Dim 05`, `## Dim 06`, `## Active matrix`.
- `references/workshop-discovery-workflow.md`: must contain `## Step 1`,
  `## Step 2`, `## Step 3`, `## Step 4`, `## Step 5`.
- `references/verma-gedsr-summary.md`: must contain `## The four echelons`
  and `## What this template explicitly does NOT use`.

## Hard rules

- **HR1. Never write to references/.** This skill is read-only. If a
  check fails, surface the failure to a human; do not auto-fix.
- **HR2. No skipping the check.** Every agent invocation, no caching.
  The check is cheap; the alternative (silent bootstrap circularity) is
  expensive.
- **HR3. No partial pass.** If ANY check fails on ANY file, halt the
  entire agent. The rigor chain has no weakest link tolerance.
- **HR4. Surface to human, never bypass.** A failure produces a message
  for the human, not a fallback that proceeds anyway.

## Refusal message format

When any check fails, emit this and halt:

```
BOOTSTRAP GUARDRAIL — operation refused.

The following human-curated references are not yet ready:

- <path>: <reason — MISSING / EMPTY / UNFILLED_PLACEHOLDER at line N /
  MALFORMED with anchor X missing>
- ...

Why this matters: this company evaluates DSR artifacts against the rigor
rubrics in references/. If those rubrics were not authored or reviewed by
a human, the evaluation is circular — an AI grading its own homework.
See references/bootstrap-circularity-note.md for the argument.

Action required: a human operator must complete the references above
before any agent in this company is allowed to score artifacts. The
guardrail will lift automatically once the checks pass.
```

## When this skill is consumed

Every agent's Operating loop, Step 0 (pre-flight). The agent calls
bootstrap-guardrail first; if the skill halts, the agent does not proceed.

This applies to all 25 agents, including:

- Phase orchestrators (discovery-orchestrator).
- Phase specialists (literature-scanner, etc.).
- Judges (judge-gemini-pro, judge-claude, judge-gpt).
- The gate-evaluator itself.

## Why this is more than a check

The guardrail is a **structural commitment**: this company refuses to
operate without human-curated rubrics. It is not a soft warning; it is a
hard halt. The cost of being unable to run is much lower than the cost of
running and producing meaningless scores that the human then trusts.

## Sanity-check example — passes

```
references/dim-framework.md:
- exists: yes
- length: 4.2KB
- placeholders: 4 unfilled (FAILS C3)
- anchors: all present
```

Result: HALT with `UNFILLED_PLACEHOLDER: references/dim-framework.md at
line 196 — <REPLACE: minimum kappa for promotion, default 0.60>`.

The human must replace the `<REPLACE: ...>` markers with actual values
before the guardrail will pass.

## Sanity-check example — fails harmlessly

```
references/verma-gedsr-summary.md:
- exists: yes
- length: 5.1KB
- placeholders: 0
- anchors: missing "## What this template explicitly does NOT use"
```

Result: HALT with `MALFORMED_REFERENCE: references/verma-gedsr-summary.md
— missing anchor "What this template explicitly does NOT use"`.

This catches the case where someone replaced the file content with their
own summary that lacks the critical "what we don't use" section — which
is essential to prevent over-importing GeDSR's four-echelon structure
into a generic DSR project.
