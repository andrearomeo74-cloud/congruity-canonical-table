# Formal Spec (Minimal) — Canonical Admissibility Grammar

**Status:** minimal, structural, domain-agnostic  
**Goal:** make the canonical layer *verifiable* (not predictive).  
This spec defines **states**, **transitions**, and **admissibility** as a closed pre-operational grammar.

---

## 1. Objects

### 1.1 Canonical State (S)
A **canonical state** is a structural configuration class, defined only by invariants and constraints.
It encodes **no utility, performance, desirability, or goal**.

We denote the set of canonical states as:

- **S** = { s₀, s₁, ... }

Each state **s ∈ S** is identified by a finite set of constraints:

- **K(s)** = { k₁, k₂, ... }

---

### 1.2 Canonical Transition (T)
A **canonical transition** is a candidate passage between two canonical states:

- **t : sᵢ → sⱼ**

We denote the set of transitions as:

- **T ⊆ S × S**

A transition is not an action, not a causal mechanism, and not a policy.
It is only a **structural possibility** under constraints.

---

## 2. Ordering and Prerequisites

We define a prerequisite relation (partial order) over states:

- **≼ ⊆ S × S**

Interpretation:
- **sᵢ ≼ sⱼ** means: state **sⱼ** does not violate prerequisites required by **sᵢ**.
Equivalently: **sⱼ** is reachable without skipping required structural conditions.

This order is domain-agnostic and only expresses **constraint precedence**.

---

## 3. Admissibility (Boolean)

Admissibility is a **boolean predicate**:

- **A : (S ∪ T) → {0, 1}**

Where:
- **A(s) = 1** means state **s** is structurally admissible (internally consistent).
- **A(t) = 1** means transition **t** preserves admissibility and prerequisite order.

No scores, probabilities, or gradients exist at the canonical level.

---

## 4. Canonical Axioms

### AX-1 (Internal Consistency)
A state is admissible only if its constraints are jointly satisfiable:

- **A(s) = 1 ⇔ SAT(K(s))**

If constraints conflict, then:

- **A(s) = 0**

---

### AX-2 (Prerequisite Preservation)
A transition **t : sᵢ → sⱼ** is admissible only if it respects the prerequisite order:

- **A(t) = 1 ⇒ sᵢ ≼ sⱼ**

Forbidden cases include “backward jumps” that violate prerequisites.

---

### AX-3 (No Contradiction Introduction)
A transition is admissible only if it does not introduce an inconsistent target state:

- **A(t) = 1 ⇒ A(sⱼ) = 1**

---

### AX-4 (Local Rejection)
If a proposed path contains a non-admissible element, the path is rejected immediately:

Let a path be:

- **p = (s₀, s₁, ..., sₙ)**

Then:

- **p is admissible ⇔ ∀ i, A(sᵢ)=1 and ∀ i<n, A(sᵢ→sᵢ₊₁)=1**

No global optimization is required; rejection is local and deterministic.

---

## 5. Closure

The canonical layer is **closed**:
- new metrics do not modify admissibility
- new objectives do not modify admissibility
- new domain models do not modify admissibility

All domain work must appear as **projections** of this grammar, never as edits to it.

---

## 6. Notes (Non-goals)

This spec does not:
- predict outcomes
- optimize behavior
- guarantee correctness, safety, or ethics
- prescribe decisions

It only determines whether a configuration or transition is **structurally admissible**.

---

## 7. Implementation Hint (Toy Checker Alignment)

A toy checker can represent:
- **S** via a finite `states.json`
- **T** via a finite `transitions.json`
- **A(·)** via deterministic checks on constraints and ordering

This is only a demonstration of the grammar’s *verifiability*, not its final form.
