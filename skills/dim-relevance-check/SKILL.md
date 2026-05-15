---
name: dim-relevance-check
description: >
  Enforces Dim 06 (Relevance) on problem statements, utility claims, and
  practitioner-facing communications. Use during Phase 5 (utility
  assessment) and Phase 6 (Communication). An artifact is relevant if
  the problem is real to practitioners and the artifact's utility is
  measurable.
---

# Dim 06 — Relevance check

**Source of truth.** [`references/dim-framework.md`](../../references/dim-framework.md)
section "Dim 06 — Relevance".

## Enforcement rules

- **R1.** Practitioner evidence. There is evidence that practitioners
  encounter the problem — not just the researcher's intuition that it
  exists. Examples: industry reports, practitioner interviews,
  documented failures, market signals.
- **R2.** Real problem, not imagined. The problem is recognizable to a
  practitioner reading the statement. "The lack of a unified ontology for
  productivity" may be real to researchers but invisible to practitioners.
- **R3.** Stakeholders named. Who benefits from the artifact? Who is
  affected if it doesn't exist? Named roles, not "users".
- **R4.** Adoption path articulated. How does this get used? What does
  the first user / first organization look like? Adoption-by-magic doesn't
  count.
- **R5.** Utility measurable. Practitioner value can be measured, not just
  asserted. "Practitioners report finding it useful" with a method that
  could distinguish useful from socially-desirable.

## When this skill is consumed

Phase 5: utility-assessor applies R3-R5. generalization-prober applies R1
and R2 across contexts. Phase 6: audience-translator applies R3 and R4 to
the practitioner version; novelty-articulator references R1-R2 for the
practitioner-relevance pillar.

## Review checklist

- [ ] R1 — Practitioner evidence is cited (not just researcher intuition).
- [ ] R2 — The problem is recognizable to a practitioner.
- [ ] R3 — Stakeholders are named with concrete roles.
- [ ] R4 — Adoption path is articulated.
- [ ] R5 — Utility is measurable, not just claimed.

## Common failure patterns

- **Researcher-only problem.** "Lack of theoretical integration between X
  and Y" — researchers care, practitioners don't notice. Reject R2.
- **Vague stakeholder.** "Knowledge workers" is a population, not a
  stakeholder. Name specific roles: "engineering managers at firms with
  >20 reports". Reject R3.
- **Adoption-by-magic.** "After publication, practitioners will adopt the
  framework." How? Through what channel? Reject R4.
- **Self-report utility only.** "Users said it was useful" is socially-
  desirable response unless an alternative is measured. Reject R5.

## Refuse-if-empty

If `references/dim-framework.md` is empty or templates unfilled, halt.
