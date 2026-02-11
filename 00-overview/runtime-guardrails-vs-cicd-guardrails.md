# Runtime Guardrails vs CI/CD Guardrails

This document clarifies the **boundary, responsibilities, and handoff**
between **CI/CD guardrails** and **runtime guardrails**.

Both are necessary.
Neither is sufficient on its own.

---

## The Core Distinction

**CI/CD guardrails** operate *before* software reaches production.  
**Runtime guardrails** operate *while* software is running.

They solve different problems at different points in time.

| Dimension | CI/CD Guardrails | Runtime Guardrails |
|---------|------------------|-------------------|
| When enforced | Before deployment | Continuously at runtime |
| Scope | Code, artifacts, configs | Live workloads and behavior |
| Primary goal | Prevent known bad changes | Maintain safety under change |
| Failure mode | Block or fail builds | Isolate, correct, or constrain |
| Ownership | Platform + DevSecOps | Platform + Runtime |
| Feedback speed | Fast, but static | Continuous, dynamic |

---

## What CI/CD Guardrails Are Good At

CI/CD guardrails are strongest when enforcing **known, static properties**.

Examples:
- Artifact provenance and signing
- Branch protections and required checks
- IaC policy checks (plan-time)
- Secrets scanning
- Release rules (flags present, approvals removed)

CI/CD answers:
> “Should this change be allowed to reach the cluster?”

Relevant sections:
- `platform-cicd-guardrails` offering
- `08-opinionated-implementations/github-actions/`

---

## What CI/CD Guardrails Cannot Guarantee

CI/CD **cannot**:
- Enforce safety after deployment
- Detect drift introduced by operators or controllers
- Observe runtime behavior under load
- Correct unsafe states automatically

Passing CI is **necessary but not sufficient**.

---

## What Runtime Guardrails Are Good At

Runtime guardrails enforce **system safety continuously**.

Examples:
- Admission control blocking unsafe specs
- Resource limits preventing noisy neighbors
- Network policies enforcing isolation
- Detecting drift from desired state
- Auto-remediating or isolating unsafe workloads

Runtime answers:
> “Is the system still safe *right now*?”

Relevant sections:
- `02-runtime-model/runtime-guardrail-categories.md`
- `03-reference-architecture/system-overview.md`
- `04-implementation-patterns/`

---

## The Handoff: CI/CD → Runtime

CI/CD and runtime guardrails are not competing systems.
They are **layered controls**.

CI/CD responsibilities:
- Ensure only *compliant artifacts* are deployable
- Encode organizational policy early
- Reduce the number of unsafe changes reaching runtime

Runtime responsibilities:
- Enforce safety regardless of how change enters the system
- Protect against drift, misconfiguration, and emergent behavior
- Reduce blast radius when things go wrong

This handoff is intentional.

---

## A Simple Rule of Thumb

- If a violation can be determined **from static inputs**, enforce it in CI/CD
- If a violation depends on **live state or behavior**, enforce it at runtime

When in doubt:
- Prefer **runtime enforcement** for safety
- Prefer **CI/CD enforcement** for developer feedback

---

## Why This Separation Matters

Blurring this boundary leads to:
- Overly complex pipelines
- False confidence in pre-deploy checks
- Runtime incidents that “should not have happened”

Clear separation enables:
- Faster pipelines
- Stronger runtime safety
- Fewer manual approvals
- Better platform ownership boundaries

---

## How This Repository Uses This Model

This repository focuses on **runtime guardrails**.

It assumes:
- CI/CD guardrails already exist or are being modernized
- Runtime guardrails complete the safety model

See:
- `ARCHITECTURE-AT-A-GLANCE.md` (Diagram 5)
- `02-runtime-model/`
- `04-implementation-patterns/`

---

> **CI/CD builds confidence.  
> Runtime guardrails preserve safety.  
> You need both to scale trust.**