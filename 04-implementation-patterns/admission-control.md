# Admission Control Guardrails

Admission control guardrails are **preventive runtime controls** that stop unsafe
configurations from entering a Kubernetes cluster.

They are enforced **before workload creation or mutation** and form one of the
strongest safety boundaries in the runtime system.

This document describes the **design pattern**, not a specific tool or policy language.

---

## Why Admission Control Exists

Admission control exists to:

- Prevent unsafe states from ever reaching the cluster
- Enforce platform-wide invariants consistently
- Replace manual approvals with automated, explainable enforcement

Admission guardrails operate at the **API boundary**, where:
- Context is richest
- Blast radius is lowest
- Enforcement is deterministic

---

## What Belongs in Admission Guardrails

Admission control is appropriate for constraints that are:

- Structural (spec shape, required fields)
- Deterministic (true or false at request time)
- Non-negotiable once the system matures

Examples:
- Required resource limits
- Forbidden privilege escalation
- Approved image sources
- Mandatory labels or annotations
- Disallowed capabilities

---

## What Does NOT Belong in Admission Guardrails

Avoid placing the following in admission control:

- Performance heuristics
- Behavioral or temporal conditions
- Signals that require runtime observation
- Policies that frequently change or are subjective

These belong in **detective** or **corrective** guardrails instead.

---

## Core Pattern: Warn → Block Progression

Admission control should almost never start in **hard-blocking mode**.

The standard progression is:

### Phase 0: Define the Boundary
- Agree on the invariant (what must eventually be true)
- Document the rationale
- Socialize intent with teams

No enforcement yet.

---

### Phase 1: Observe
- Evaluate policies
- Record violations
- Do not surface feedback to teams

Purpose:
- Understand impact
- Discover edge cases
- Build trust in signal quality

---

### Phase 2: Warn
- Surface violations clearly
- Allow workloads to proceed
- Provide actionable guidance

Purpose:
- Enable self-correction
- Validate policy correctness
- Avoid surprise failures

---

### Phase 3: Block
- Reject non-compliant requests
- Provide deterministic error messages
- Enforce uniformly

Purpose:
- Make the safe path the only path
- Remove ambiguity
- Scale governance without human gates

---

## Enforcement Maturity Over Time

Admission guardrails typically mature along two dimensions:

- **Strictness** (observe → warn → block)
- **Scope** (subset of namespaces → cluster-wide)

Mature systems:
- Start narrow
- Expand gradually
- Never skip stages

---

## Environment-Specific Enforcement

It is common for enforcement strength to vary by environment:

- Development: observe / warn
- Staging: warn / selective block
- Production: block

This allows learning without sacrificing safety where it matters most.

---

## Relationship to CI/CD Guardrails

Admission control complements CI/CD guardrails:

- CI/CD prevents known-bad changes earlier
- Admission control protects against:
  - Bypasses
  - Drift
  - Emergency changes
  - Unknown clients

Both are required for defense in depth.

---

## Common Failure Modes

- Starting in block mode without signal confidence
- Encoding organizational politics into policy
- Using admission control to compensate for missing platforms
- Creating opaque or unhelpful error messages

---

## Key Principle

> **Admission control protects the system, not the process.**

When designed well, it is:
- Predictable
- Explainable
- Invisible during normal operation
