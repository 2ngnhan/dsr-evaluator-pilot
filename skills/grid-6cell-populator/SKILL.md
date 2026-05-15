---
name: grid-6cell-populator
description: >
  Populates the Vom Brocke & Maedche DSR 6-Grid (Cells 1-6). Use during
  Phase 1 (initial populate of Cells 1, 4, 5), Phase 3 (Cell 2, 3), and
  Phase 6 (Cell 6). Enforces the critical rule that Cell 5 is
  cross-cutting vocabulary, not artifact description.
---

# Grid 6-cell populator

**Source of truth.** [`references/vom-brocke-6grid.md`](../../references/vom-brocke-6grid.md).
Always read first.

## What this skill does

Populates one or more cells of the DSR 6-Grid. Output is direct-insertion
markdown formatted for the company's standard bilingual delivery packet.

## The six cells

```
+--------------------+----------------------+-----------------------+
| Cell 1 PROBLEM     | Cell 2 PROCESS       | Cell 3 SOLUTION       |
+--------------------+----------------------+-----------------------+
| Cell 4 INPUT KNOW. | Cell 5 KEY CONCEPTS  | Cell 6 OUTPUT KNOW.   |
+--------------------+----------------------+-----------------------+
```

## Cell-specific rules

### Cell 1 — Problem
- 2-3 sentences max for the grid (a full gap statement lives separately).
- Must be falsifiable (defer to `dim-falsifiability-check`).
- Must be scoped (defer to `dim-scope-check`).

### Cell 2 — Research process
- Reference Peffers phases used.
- Name FEDS quadrants used in evaluation.
- Identify build-evaluate cycles.

### Cell 3 — Solution description
- Classify per March & Smith 1995: construct / model / method /
  instantiation.
- High-level architecture or operating principles.

### Cell 4 — Input knowledge
- Three subsections: existing literature, empirical base, theoretical
  frameworks.
- Each citation must be verifiable (post-Step-3 of the discovery workflow).

### Cell 5 — Key concepts (THE CRITICAL RULE)

**Cell 5 is NOT a description of the artifact. That belongs in Cell 3.**

Cell 5 is a **cross-cutting vocabulary table**. For each term used
anywhere in the project:

- precise definition as used in *this* project,
- note if it differs from common usage,
- list which other cells it appears in.

A Cell 5 entry that describes only the artifact (e.g., "the framework
distinguishes effort from certainty") is wrong. The right entry is:

| Term | Definition (as used here) | Differs from common usage? | Cells |
|---|---|---|---|
| Effort | Billable hours allocated to a task | Yes — excludes context-switching cost typically counted in PM literature | 1, 3, 4 |
| Certainty | Probability assigned to delivery by a defined date with defined scope | Yes — common usage refers to general confidence; this project requires probability | 1, 3 |

### Cell 6 — Output knowledge
- New constructs, models, methods, or instantiations created.
- New design principles with theory backing.
- Empirical findings.
- Methodological contributions if any.

## Hard rules

- **R1. Cell 5 cross-cutting only.** Any Cell 5 entry that does not list
  at least 2 other cells in the "Cells" column is rejected — Cell 5 by
  definition is cross-cutting; a term used in only one cell does not
  qualify.
- **R2. Cell 5 vocabulary not artifact.** Reject entries that describe
  the artifact's structure or behavior. Those go in Cell 3.
- **R3. Vocabulary consistency.** Every term that appears in two or more
  cells must have a single definition in Cell 5. Inconsistent definitions
  across cells reject under R3.
- **R4. Empty cell exit ban.** A cell may be marked "TBD" with reason,
  but cannot be empty. If a phase exits, the cell either has content or
  has an explicit `TBD: <reason>` block.
- **R5. Verifiability.** Cell 4 citations must have been verified (Step 3
  of the discovery workflow). Unverified citations are quarantined in
  the packet and flagged.

## Output format

```markdown
### Cell 1 — Problem
<2-3 sentence problem statement>

### Cell 4 — Input Knowledge
**Literature:**
- <citation 1> [VERIFIED]
- <citation 2> [VERIFIED]

**Empirical base:**
- <evidence source 1>
- ...

**Theoretical frameworks:**
- <kernel theory 1>
- ...

### Cell 5 — Key Concepts
| Term | Definition (as used here) | Differs from common usage? | Cells |
|---|---|---|---|
| <term> | <def> | <yes/no, how> | <1, 3, 4 ...> |
| ... | ... | ... | ... |
```

## Refuse-if-empty

If `references/vom-brocke-6grid.md` is missing or empty, halt and ask the
human to provide the cell definitions before populating.

## Common errors caught

- "Cell 5: The LIFT framework consists of..." -> R2 violation. Move to
  Cell 3.
- "Cell 5: Effort (used in problem statement)" with no other cells
  listed -> R1 violation. Either add Cells or move to a project-glossary.
- Cells 1 and 3 use "uncertainty" with different definitions -> R3
  violation. Pick one definition and apply throughout.
