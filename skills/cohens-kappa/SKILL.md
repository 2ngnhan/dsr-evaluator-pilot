---
name: cohens-kappa
description: >
  Computes weighted Cohen's kappa across N judges scoring M items on a 1-5
  ordinal scale. Use to assess inter-rater reliability of the cross-model
  judge panel. Produces a kappa value, an interpretation, a stability
  flag (when item count is too low), and the per-pair agreement matrix.
---

# Cohen's kappa — inter-rater reliability for ordinal scores

**Source of truth.** Cohen, J. (1968). Weighted kappa: nominal scale
agreement with provision for scaled disagreement or partial credit.
*Psychological Bulletin*, 70(4), 213-220.

This skill operationalizes weighted kappa for the cross-model judge panel
in this template. The panel has two judges (Gemini Pro, Claude Opus, GPT-5)
each scoring M rubric items on a 1-5 ordinal scale.

## Why weighted kappa, not unweighted

Unweighted kappa treats any disagreement equally. For a 1-5 ordinal scale,
a 1 vs 5 disagreement is much more serious than a 4 vs 5 disagreement.
Weighted kappa with quadratic weights penalizes large disagreements
quadratically and small disagreements lightly. This is the right choice
for rubric scoring.

## Procedure

Inputs:

- `judges`: list of N >= 2 judges, each producing one score per item.
- `items`: list of M rubric items being scored.
- `scores[judge_i][item_j]`: integer in {1, 2, 3, 4, 5}.

Steps:

1. **Validate inputs.**
   - If N < 3, halt with `INSUFFICIENT_JUDGES` (this template requires 3
     for cross-model independence).
   - If M < `10`,
     compute kappa anyway but flag `UNSTABLE_KAPPA` (low item count
     produces high-variance estimates).
2. **Compute pairwise weighted kappa.** For each pair of judges (i, j),
   compute weighted kappa with quadratic weights:
   - Observed agreement weight `w[r1][r2] = 1 - ((r1 - r2)^2) / ((K-1)^2)`
     where K = number of categories (here, 5).
   - Observed weighted agreement `p_o` = sum over items of average
     `w(score_i, score_j)` for items.
   - Expected weighted agreement `p_e` from the marginal distributions.
   - `kappa(i,j) = (p_o - p_e) / (1 - p_e)`.
3. **Aggregate across all pairs.** For N=2 judges this yields three
   pairwise kappas. Report:
   - mean kappa across all pairs (primary number),
   - min kappa across pairs (worst-case agreement),
   - the full pairwise matrix.
4. **Apply interpretation table** (Landis & Koch 1977, widely cited):

   | kappa range | interpretation |
   |---|---|
   | < 0.00 | Poor / worse than chance |
   | 0.00 - 0.20 | Slight |
   | 0.21 - 0.40 | Fair |
   | 0.41 - 0.60 | Moderate |
   | 0.61 - 0.80 | Substantial |
   | 0.81 - 1.00 | Near-perfect |

5. **Apply this template's promotion gate.** Promote the artifact if
   `mean_kappa >= 0.60`
   AND `min_kappa >= 0.40`.
   Otherwise route to human disagree-resolver.

## Hard rules

- **N < 2 judges.** Halt with `INSUFFICIENT_JUDGES`. This template
  requires cross-model independence for the kappa to be meaningful.
- **M < 10.** Compute kappa but flag
  `UNSTABLE_KAPPA: low item count, kappa estimate has high variance`.
  Always surface this flag in the gate evidence packet.
- **Identical scores across all judges (every cell agrees).** The kappa
  is 1.0 but this can indicate the panel is degenerate (e.g., both
  judges are the same model under DEGRADED mode). Cross-check whether
  DEGRADED is flagged; if so, do not treat kappa = 1 as meaningful.
- **Ties in marginal distribution producing `1 - p_e = 0`.** Kappa is
  undefined. Halt with `UNDEFINED_KAPPA` and surface the marginal
  distribution; this typically means one score (often 3) dominates and
  the panel has no discriminating power.
- **Missing scores.** A judge that failed to score an item must be
  reported, not interpolated. Compute kappa over items where all judges
  scored; surface the number of missing items in the packet.

## Output format

```yaml
kappa:
  mean: <float>            # primary number
  min:  <float>            # worst pairwise
  pairwise:
    - judges: [gemini-pro, claude]
      value: <float>
    - judges: [gemini-pro, gpt]
      value: <float>
    - judges: [claude, gpt]
      value: <float>
  interpretation: <slight | fair | moderate | substantial | near-perfect>
  decision: <promote | human-required>
flags:
  - UNSTABLE_KAPPA   # only if M below stability floor
  - DEGRADED         # only if any judge is in fallback mode
  - INSUFFICIENT_JUDGES
  - UNDEFINED_KAPPA
items_scored: <int>
items_missing: <int>
```

## When this skill is consumed

The `gate-evaluator` agent calls this skill once per phase. Inputs are the
three judge score sets for the active rubric dimensions in that phase.
The agent uses the `decision` field to either promote the artifact or
route to a human; in either case, the full packet (including the matrix)
is preserved in the gate evidence packet.

## Refuse-if-empty / pre-flight

Before computing, verify:

- `references/dim-framework.md` is populated (rubrics exist).
- The judge agents have actually run (otherwise their scores are nonexistent).
- No judge's output is empty or all-zeroes (likely a model failure).

If any pre-flight fails, halt with `PREFLIGHT_FAILED` and do not produce a
kappa value. A kappa from missing or fabricated scores is misleading.

## Sanity-check example

Three judges, ten items:

```
              item1 item2 item3 item4 item5 item6 item7 item8 item9 item10
gemini-pro:    4     4     5     3     4     4     5     4     3     4
claude:        4     5     5     3     4     3     5     4     2     4
gpt:           4     4     5     2     5     4     5     3     3     4
```

Pairwise weighted kappa:

- (gemini, claude): ~0.71
- (gemini, gpt): ~0.65
- (claude, gpt): ~0.59

Mean = ~0.65, min = ~0.59. Interpretation = substantial (mean). With the
default floor (0.60 mean, 0.40 min), promotion = yes.

## Common errors

- **Unweighted kappa on ordinal data.** Penalizes 1-vs-5 the same as
  1-vs-2. Use weighted kappa always for 1-5 rubrics.
- **Fleiss kappa with N=2.** Fleiss is for fixed raters across items, not
  the right generalization for this template. Pairwise weighted kappa
  averaged across pairs is the simpler and more interpretable choice for
  N=2.
- **Reporting only mean kappa.** Always report min kappa too — one judge
  drifting from the other two is operationally important.
