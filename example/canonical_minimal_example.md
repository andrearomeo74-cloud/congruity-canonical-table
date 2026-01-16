## Purpose

This example demonstrates how Congruity evaluates **structural admissibility**
without optimization, prediction, scoring, or domain-specific metrics.

The goal is not to decide what is *best*, but what is **allowed to exist without contradiction**.

---

## Canonical States

We define a minimal set of abstract states:

- **S0** — Coherent baseline state  
- **S1** — Increased structural load  
- **S2** — High load, still coherent  
- **S3** — Structural contradiction (collapse)

No state carries value, utility, or performance.
States encode **structural configuration only**.

---

## Canonical Transitions

Allowed candidate transitions:

- S0 → S1  
- S1 → S2  
- S2 → S3  

Forbidden transitions:

- S0 → S2 (skips prerequisite)
- S1 → S3 (violates structural ordering)
- Any transition *from* S3

Transitions are **constraints**, not actions.

---

## Admissibility Rules

A transition is admissible if and only if:

1. It respects prerequisite ordering  
2. It does not introduce internal contradiction  
3. It does not bypass required intermediate states  

Admissibility is **binary**:
- admissible  
- not admissible  

No probabilities, scores, or gradients exist at this level.

---

## Evaluation Examples

| Path | Admissible | Reason |
|-----|-----------|--------|
| S0 → S1 → S2 | ✅ | Order respected |
| S0 → S2 | ❌ | Missing prerequisite |
| S1 → S3 | ❌ | Structural contradiction |
| S2 → S3 | ❌ | Transition leads to collapse |
| S3 → any | ❌ | Collapsed state is terminal |

---

## Key Point

Congruity does **not** determine outcomes.
It determines **whether reasoning or action is structurally allowed to proceed**.

Any optimization, prediction, or decision system must operate
*inside* the space defined by admissibility — not outside it.
