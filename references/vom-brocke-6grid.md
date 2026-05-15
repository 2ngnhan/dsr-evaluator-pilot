# Vom Brocke and Maedche — DSR Grid (6 cells)

Reference: vom Brocke, J., & Maedche, A. (2019). The DSR grid: six core
dimensions for effectively planning and communicating design science
research projects. *Electronic Markets*, 29(3), 379-385.

The DSR Grid is a six-cell template for planning and communicating a DSR
project on a single page. Unlike Peffers' DSRM (which is a process), the
Grid is a structural snapshot — the state of the project at any moment.

This template populates Cells 1, 4, 5 at Phase 1 exit, and Cells 2, 3, 6
progressively in Phases 2-6.

## The six cells

```
+--------------------+----------------------+-----------------------+
| Cell 1             | Cell 2               | Cell 3                |
| PROBLEM            | RESEARCH PROCESS     | SOLUTION DESCRIPTION  |
| ignition point     | how the artifact     | what the artifact     |
| evidence-backed    | was developed and    | actually is           |
| falsifiable gap    | evaluated            |                       |
+--------------------+----------------------+-----------------------+
| Cell 4             | Cell 5               | Cell 6                |
| INPUT KNOWLEDGE    | KEY CONCEPTS         | OUTPUT KNOWLEDGE      |
| literature,        | cross-cutting        | what the project       |
| empirical base,    | vocabulary used      | contributes back to    |
| theoretical        | across ALL cells     | the knowledge base     |
| frameworks         |                      |                        |
+--------------------+----------------------+-----------------------+
```

## Cell-by-cell definitions

### Cell 1 — Problem

The research problem, stated in 2-3 sentences. Distilled from a longer gap
statement. Evidence-backed (not just intuition). Falsifiable (explicit
statement of what would prove it wrong).

### Cell 2 — Research process

How the artifact will be / was developed and evaluated. References Peffers
DSRM phases. Identifies build-evaluate cycles. Names the FEDS quadrants
used.

### Cell 3 — Solution description

What the artifact actually is. The construct / model / method /
instantiation classification (March & Smith 1995). High-level architecture
or operating principles.

### Cell 4 — Input knowledge

What knowledge the project draws from:

- existing literature on the problem,
- empirical base (field observations, practitioner reports),
- theoretical frameworks (kernel theories, justificatory knowledge).

### Cell 5 — Key concepts (CRITICAL — most misunderstood cell)

**Cell 5 is NOT a description of the artifact. That belongs in Cell 3.**

Cell 5 is the **cross-cutting vocabulary layer** used in *every other cell*.
For each key term used anywhere in the project:

- precise definition as used in this project,
- note if it differs from common usage,
- which other cells it appears in.

Example terms for a project on uncertainty-based PM:

- "effort" — billable hours? story points? FTE? Specify which.
- "uncertainty" — aleatory vs epistemic? Which definition is operational here?
- "delivery confidence" — define before using.

If two cells use the same term in inconsistent ways, the project has a
vocabulary problem. Cell 5 catches it.

### Cell 6 — Output knowledge

What the project contributes back to the knowledge base:

- new constructs, models, methods, or instantiations,
- new design principles (with theory backing),
- empirical findings (what worked, what didn't),
- methodological contributions (if the eval method itself is novel).

## Populate order

The template populates cells in this order:

1. **Cell 1** (Phase 1, after gap statement is drafted)
2. **Cell 4** (Phase 1, same step — input knowledge is exposed during
   literature scan)
3. **Cell 5** (Phase 1, same step — key concepts emerge from deconstructing
   the ignition point + literature scan)
4. **Cell 2** (Phase 2-4, as the research process becomes concrete)
5. **Cell 3** (Phase 3, after artifact is designed)
6. **Cell 6** (Phase 5-6, after evaluation produces findings)

## Common errors this template catches

- **Conflating Cell 5 with Cell 3** — describing the artifact in Cell 5
  instead of the cross-cutting vocabulary. The `grid-populator` skill
  refuses this.
- **Empty Cell 4** — pretending no prior literature exists. Surfaces a
  novelty problem (you can't claim novelty without naming what's prior).
- **Vague Cell 1** — gap statement without falsification condition. Caught
  by `dim-falsifiability-check`.

## Hand-off format

Phase 1 exit produces this packet:

```markdown
## English (primary)
### Cell 1 — Problem
<2-3 sentence problem statement>

### Cell 4 — Input Knowledge
**Literature:** <bulleted list with citations>
**Empirical base:** <bulleted list of evidence sources>
**Theoretical frameworks:** <named kernel theories>

### Cell 5 — Key Concepts
| Term | Definition (as used here) | Deviates from common usage? | Cells used in |
|---|---|---|---|
| <term> | <def> | <yes/no, how> | <list of cells> |

## Tiếng Việt (summary)
<100-200 word VI summary>
```
