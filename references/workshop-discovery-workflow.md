# Workshop Discovery Workflow — 5 steps to a DSR-compliant gap statement

Source: Workshop 1, Part 3 Demo (16 May 2026), VinUniversity MBA AI
Research & Practice Series. Presenter: Luong Son Tinh. Facilitator:
Nguyen Ngoc Nhan.

This is the workflow Phase 1 of this template implements. Each agent in
Phase 1 owns one step. The prompts below are verbatim from the workshop
handout (originally in English with surrounding Vietnamese narration; only
the English prompts are reproduced here, with the narration translated).

**Total time.** ~20 minutes for a live demo. ~3-6 hours for serious work.

**Ignition point used in the demo (example):**

> "Effort-based management is not effective anymore — we need a new approach."

This is a *practitioner sentence*. It is **not** a DSR problem statement.
The workflow below transforms it into one.

---

## Step 1 — Deconstruct the ignition point

**Tool.** Claude or ChatGPT (any reasoning-strong general model).
**Timing.** 3 minutes.

**Task.** An ignition point contains many hidden assumptions. Before searching
literature, unpack them — because you don't know what to search for if you
don't know what you're claiming.

**Prompt (verbatim):**

```
I have an intuition about a research problem:
"Effort-based management is not effective anymore — we need a new approach."

Act as a rigorous DSR reviewer. Deconstruct this claim into:
1. Hidden assumptions (what must be true for this to be a valid problem?)
2. Scope ambiguities (effective for whom? in what context? compared to what baseline?)
3. 3 falsifiable sub-claims that could be tested empirically
4. What evidence would prove this claim wrong?

Do NOT suggest solutions. Only interrogate the problem.
```

**Expected output.** A list of hidden assumptions, e.g.:

- "Effort" — defined how? Story points? Billable hours? FTE?
- "Not effective" — measured by what? Delivery rate? Client satisfaction? Burnout?
- "Anymore" — implies it once worked. When did that change, why?
- "Context" — knowledge work generally, or software development specifically?

Plus 3-4 falsifiable sub-claims and a scope-decision list to settle before
literature search.

---

## Step 2 — Rapid literature scan (evidence and grounding)

**Tool.** Claude (web) / Perplexity / Connected Papers.
**Timing.** 5 minutes.

**Task.** Find two kinds of evidence at once, following the Hevner
Knowledge Base cycle:

- **Evidence A — Relevance.** Does this problem actually exist? Who has
  documented it?
- **Evidence B — Rigor.** What does the literature already know about this
  problem? Where is the gap?

**Prompt (verbatim):**

```
I'm doing a Design Science Research project on the failure of effort-based project
management in knowledge work, specifically in AI-assisted and low-code/no-code
development contexts.

Help me find evidence for both sides of the Hevner Knowledge Base cycle:

RELEVANCE CYCLE — real-world evidence:
- What industry data or practitioner reports document effort-based PM failures?
- Which specific failure modes are documented? (e.g., schedule overruns, scope creep, burnout)

RIGOR CYCLE — academic grounding:
- What established theories explain WHY effort-based measurement fails in
  non-linear, creative work?
- What methodological alternatives have been proposed and evaluated?
- What is the most-cited gap statement in this domain?

Format as: [Claim] → [Evidence/Source] → [Strength: strong/moderate/weak/speculation]
Flag any claims you're not certain about.
```

**Expected output (formatted evidence list):**

```
RELEVANCE:
[Claim] 66% of software projects fail or have significant issues
→ [Evidence] Standish Group CHAOS Report 2020
→ [Strength] Strong — longitudinal, large sample

[Claim] Story points don't predict delivery accuracy
→ [Evidence] Multiple Agile retrospective studies (2018-2023)
→ [Strength] Moderate — practitioner research, selection bias possible

RIGOR:
[Claim] Non-linear work violates Taylor's effort-output linearity assumption
→ [Evidence] Simon (1969) Sciences of the Artificial; Pink (2009) Drive
→ [Strength] Strong — theoretical foundation, widely cited

[Claim] Uncertainty quantification in PM is undertheorized
→ [Evidence] [AI will flag uncertainty]
→ [Strength] Speculation — needs verification
```

**Warning.** The model will hallucinate some sources — especially author
names and specific years. Step 3 handles this. Do not forward this output
to an advisor without going through Step 3.

---

## Step 3 — Adversarial verification (don't trust the AI)

**Tool.** A SECOND Claude / different model + Semantic Scholar + Google Scholar.
**Timing.** 4 minutes.

**Task.** This is the most important step and the one most often skipped.
Take the evidence list from Step 2 and run an adversarial prompt — then
verify the top 3 sources directly on Semantic Scholar.

**Prompt (verbatim):**

```
Here is a list of evidence claims I gathered about effort-based management failures:
[paste list from Step 2]

For each claim:
1. Challenge the evidence — what are the methodological weaknesses?
2. Flag any sources you cannot verify exist
3. Identify which claims are widely accepted vs. contested in the literature
4. Suggest the strongest counter-argument to the overall problem statement

Be ruthless. Your job is to break this argument, not support it.
```

**Parallel verification.** Open semanticscholar.org or scholar.google.com.
Search the paper titles, check citation count, read abstracts. A paper
whose abstract matches the AI's claim AND has citation count > 0 may be
retained. Others go.

**Outputs of this step:**

- Cleaned evidence list (speculation removed, strong/moderate kept).
- Known counter-arguments to address in the problem statement.
- The actual gap — because the model will tell you what is already studied.

---

## Step 4 — Construct the gap statement

**Tool.** Claude (same model as Step 1).
**Timing.** 4 minutes.

**Task.** Synthesis step. Use verified evidence to write a DSR-compliant
gap statement. The statement must simultaneously satisfy five criteria:
*falsifiable, scoped, grounded, novel, motivated*.

**Prompt (verbatim):**

```
Based on this verified evidence:
[paste cleaned evidence list]

Help me construct a DSR-compliant gap statement for the Problem cell of a
6-grid DSR model. The statement must:

1. Be FALSIFIABLE — state what evidence would prove it wrong
2. Be SCOPED — specify context (knowledge work? software dev? LCNC?)
3. Be GROUNDED — reference at least 2 theoretical foundations
4. Be NOVEL — explain what existing solutions miss or don't address
5. Be MOTIVATED — explain why this matters to practitioners NOW

Format:
PROBLEM: [one sentence]
CONTEXT: [boundaries of the claim]
EVIDENCE: [3 strongest supporting points]
GAP: [what existing literature/practice does NOT address]
FALSIFICATION: [what would prove this wrong]
MOTIVATION: [why now, why this matters]
```

**Expected output — DSR-compliant gap statement:**

```
PROBLEM: Existing project management methodologies, designed around effort
quantification, systematically fail to capture and communicate delivery
certainty in knowledge-intensive, iterative development contexts.

CONTEXT: Software development teams using Agile, Scrum, or Shape Up in
knowledge-intensive contexts, specifically including LCNC and AI-assisted
development where output is non-linear and uncertainty is primary risk.

EVIDENCE:
1. CHAOS Report: 66% failure rate despite widespread Agile adoption
2. Simon (1969): non-linear work violates effort-output linearity assumptions
3. Principal-agent theory: time-based billing misaligns incentives with outcomes

GAP: No existing methodology operationalizes uncertainty quantification as
a primary planning and tracking mechanism at the task/claim level.

FALSIFICATION: If a study demonstrates that effort-based metrics (velocity,
story points) significantly predict delivery outcomes (accuracy, scope,
quality) in LCNC contexts with n>50 projects, this problem statement fails.

MOTIVATION: With AI commoditizing execution effort, certainty — not effort —
becomes the scarce resource. Current tools have no mechanism to measure it.
```

---

## Step 5 — Populate Cell 1 and adjacent cells

**Tool.** Claude.
**Timing.** 4 minutes.

**Task.** Use the gap statement to populate not just Cell 1 but also
Cell 4 (Input Knowledge) and Cell 5 (Key Concepts).

**Important.** Cell 5 is **NOT** a description of the artifact — that's
Cell 3. Per Vom Brocke & Maedche, Cell 5 is a *cross-cutting vocabulary
layer* used across all other cells.

**Prompt (verbatim):**

```
Given this problem statement and gap:
[paste from Step 4]

Populate the DSR 6-grid for the left column:

CELL 1 — PROBLEM:
A concise version of the problem for the grid (2-3 sentences max)

CELL 4 — INPUT KNOWLEDGE:
- What existing literature informs this problem?
- What empirical evidence base supports it?
- What theoretical frameworks are relevant?
- How many papers should a proper literature review cover?

CELL 5 — KEY CONCEPTS:
What are the most important terms used across ALL dimensions
of this research — in the problem description, the solution,
the process, and the evaluation? For each term:
- Define it precisely AS USED in this project
- Note if it differs from common usage
- Note which other cells it appears in
Example terms to consider: effort, certainty, confidence,
knowledge work, delivery uncertainty, appetite, uphill/downhill.

Format each cell for direct insertion into a research document.
```

**Output populates 3 of 6 cells immediately.** Cells 2, 3, 6 (Research
Process, Solution Description, Output Knowledge) require an artifact that
exists. They cannot be AI-generated without actually doing the design work.

---

## Result after 20 minutes

Three of six cells populated:

- Cell 1 — Problem (full gap statement)
- Cell 4 — Input Knowledge (literature + frameworks)
- Cell 5 — Key Concepts (cross-cutting vocabulary)

Cells 2 / 3 / 6 remain TBD pending the Build phases.

## Downsides — know these before applying

1. **Hallucination risk in Step 2.** The model will confidently cite papers
   that don't exist, especially with specific author names and years.
   Mitigated by Step 3, but only if Step 3 is actually run.
2. **AI confirmation bias.** Prompting "effort-based is failing" steers the
   model to find supporting evidence and miss counter-evidence. Mitigation:
   add a "steelman the opposing view" prompt.
3. **Depth tradeoff.** 20 minutes yields a structured gap statement but
   lacks the depth of a proper systematic literature review (2-4 weeks).
   This is a skeleton, not a finished Chapter 2.
4. **Prompt engineering skill underestimated.** Prompts above were tuned
   over iterations. Audience may not reproduce with ad-hoc prompts.
5. **Context dependency.** Works well when practitioner grounding exists.
   For wholly new problems with no practitioner contact, Step 2 is thin.
6. **No replacement for domain expertise.** AI cannot judge novelty in
   niche domains. A human reviewer must validate.

## How this template wires to the workflow

| Step | Agent | Model |
|---|---|---|
| 1 Deconstruct | ignition-deconstructor | gemini-2.5-pro |
| 2 Literature scan | literature-scanner | gemini-2.5-flash (bulk reading) |
| 3 Adversarial verify | adversarial-verifier | claude-opus-4-7 (CROSS-MODEL) |
| 4 Gap statement | gap-constructor | gemini-2.5-pro |
| 5 Grid populate | grid-populator | gemini-2.5-pro |

The cross-model requirement at Step 3 is critical: an AI checking another
AI of the same family inherits the same training biases and tends to ratify
rather than challenge. A different model family at this step measurably
catches more hallucinations.
