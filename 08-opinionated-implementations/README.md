# Opinionated Implementations

This section provides **concrete, tool-shaped examples** of how the concepts in this repository
*can be implemented in practice* — without redefining or constraining the underlying model.

These examples are **deliberately opinionated**, but **not prescriptive**.

They exist to help readers move from *conceptual understanding* to *practical application*,
while preserving flexibility, context, and engineering judgment.

---

## Why This Section Exists

The core of this repository focuses on:
- Principles
- Models
- Architecture
- Safe rollout patterns

However, at some point readers ask:

- “What does this look like in GitHub Actions?”
- “Where do these guardrails actually live in Kubernetes?”
- “How do policy-as-code tools fit into this without taking over everything?”

This section answers those questions **by example**, not by mandate.

---

## What This Section Is (and Is Not)

### This section **is**:
- A set of **illustrative implementations**
- A way to ground abstract ideas in real systems
- A bridge between design intent and execution
- A reference for platform and enablement teams building internal solutions

### This section **is not**:
- A complete reference implementation
- A copy-paste production solution
- A tool comparison or vendor evaluation
- A replacement for platform-specific design work

If you are looking for “the right YAML,” you are in the wrong place.
If you are looking for *how to think about applying guardrails in real systems*, you are in the right place.

---

## How to Use These Examples

Each example in this section follows the same principles:

- Start with **intent**, not tooling
- Show **where guardrails live**, not just how they’re coded
- Emphasize **progressive enforcement**, not hard gates
- Prefer **clarity over completeness**

You are encouraged to:
- Adapt patterns, not clone them
- Adjust enforcement levels to your maturity
- Replace tools while keeping architectural intent intact

---

## Structure of This Section

### GitHub Actions

`github-actions/`

Examples showing how CI/CD guardrails can be embedded into
shared workflows and pipelines using GitHub Actions.

Focus areas:
- Admission-style checks in CI
- Progressive hardening (warn → block)
- Reusable workflows vs bespoke pipelines
- Guardrails as shared platform capabilities

---

### Kubernetes Runtime

`kubernetes/`

Examples showing how guardrails are enforced **at runtime**,
inside the cluster, rather than only at build or deploy time.

Focus areas:
- Admission policies
- Runtime detection and signals
- Corrective and containment patterns
- Separation of prevention, detection, and correction

---

### Policy-as-Code

`policy-as-code/`

Guidance on where policy-as-code tools fit — and where they don’t.

Focus areas:
- Decision-making, not syntax
- When policy adds leverage vs friction
- How to avoid policy sprawl
- Choosing tools based on enforcement intent

---

## Important Boundaries

To keep this repository healthy and scalable, this section intentionally avoids:

- Full production-grade configurations
- Deep vendor-specific tuning
- Exhaustive policy libraries
- Environment-specific assumptions

Those belong in **downstream repositories**, not here.

---

## If You’re Short on Time

- Want **real examples** → start with `github-actions/`
- Working on **runtime safety** → start with `kubernetes/`
- Debating **policy tooling** → read `policy-as-code/decision-guide.md`
- Unsure how to use any of this → read `disclaimers.md`

---

## Guiding Reminder

> **Examples should illuminate the model — not replace it.**

If an implementation obscures intent, adds ceremony, or creates fear,
it is working against the goals of guardrails — even if it is technically correct.
