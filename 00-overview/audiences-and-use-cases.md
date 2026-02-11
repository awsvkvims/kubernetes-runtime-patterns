# Audiences and Use Cases

This document explains **who this repository is for**, **what problems each audience is trying to solve**, and **how different roles use runtime guardrails differently**.

Runtime guardrails are a shared system — but **not everyone interacts with them the same way**.

---

## Primary Audiences

This repository serves three main audiences, with different responsibilities and decision horizons.

---

## 1. Platform & Runtime Engineering Teams (Primary)

### Who They Are
- Platform engineers
- SREs
- Kubernetes platform owners
- Runtime and infrastructure architects

### Problems They Are Solving
- Preventing unsafe workloads from entering clusters
- Reducing blast radius of failures
- Scaling multi-tenant Kubernetes safely
- Replacing manual approvals with systemic controls
- Providing safe defaults without blocking teams

### How They Use This Repository
Platform teams use this repository to:
- Design runtime guardrail models
- Decide *what belongs in admission vs detection vs correction*
- Implement reusable enforcement patterns
- Roll out guardrails incrementally across environments

Key entry points:
- `02-runtime-model/runtime-guardrail-categories.md`
- `03-reference-architecture/system-overview.md`
- `04-implementation-patterns/`
- `06-rollout-playbooks/`

---

## 2. Application & Engineering Teams (Primary)

### Who They Are
- Application developers
- Service owners
- Engineering managers
- Technical leads

### Problems They Are Solving
- Shipping changes without unexpected blocks
- Understanding why workloads are rejected or constrained
- Avoiding last-minute compliance surprises
- Retaining autonomy while meeting platform constraints

### How They Use This Repository
Engineering teams use this repository to:
- Understand *what guardrails exist and why*
- Learn platform expectations early
- Debug admission failures or runtime enforcement
- Design services that align with platform contracts

Key entry points:
- `01-principles/`
- `04-implementation-patterns/`
- `05-starter-assets/`
- `06-rollout-playbooks/onboarding-a-team.md`

---

## 3. Technology & Engineering Leadership (Secondary)

### Who They Are
- Directors
- VPs
- CTOs
- Heads of Platform / Infrastructure

### Problems They Are Solving
- Scaling delivery without increasing risk
- Removing approval bottlenecks
- Funding platform capabilities instead of adding process
- Creating consistent governance across teams

### How They Use This Repository
Leadership uses this repository to:
- Understand why approvals don’t scale
- See how guardrails reduce risk systemically
- Align investment with platform leverage points
- Defend architectural decisions during audits or incidents

Key entry points:
- `ARCHITECTURE-AT-A-GLANCE.md`
- `07-leadership-conversations/`
- `06-rollout-playbooks/`

---

## Common Use Cases

Below are common scenarios this repository is designed to support.

---

### Use Case 1: Replacing Deployment Approvals

**Situation:**  
Teams are blocked by manual approval gates before production deploys.

**How this repository helps:**
- CI/CD guardrails ensure only compliant artifacts reach clusters
- Runtime guardrails enforce safety continuously
- Approvals are replaced with policy and automation

Relevant sections:
- `runtime-guardrails-vs-cicd-guardrails.md`
- `02-runtime-model/enforcement-levels.md`
- `04-implementation-patterns/admission-control.md`

---

### Use Case 2: Scaling Multi-Tenant Kubernetes Safely

**Situation:**  
Multiple teams share clusters with inconsistent safety practices.

**How this repository helps:**
- Defines isolation boundaries (namespaces, RBAC, networks)
- Establishes default-safe resource baselines
- Enforces contracts uniformly at runtime

Relevant sections:
- `03-reference-architecture/multi-tenancy-and-isolation.md`
- `04-implementation-patterns/namespaces-and-rbac.md`
- `04-implementation-patterns/network-policies.md`

---

### Use Case 3: Reducing Runtime Incidents

**Situation:**  
Incidents are frequent, and recovery is manual and slow.

**How this repository helps:**
- Detective guardrails surface drift early
- Corrective guardrails automate containment
- Guardrails generate signals for system improvement

Relevant sections:
- `02-runtime-model/runtime-guardrail-categories.md`
- `04-implementation-patterns/progressive-hardening.md`
- `06-rollout-playbooks/incident-readiness.md`

---

### Use Case 4: Audits Without Panic

**Situation:**  
Audits trigger ad-hoc control reviews and manual evidence collection.

**How this repository helps:**
- Guardrails create enforceable, repeatable controls
- Enforcement is visible and explainable
- Compliance emerges from system design

Relevant sections:
- `03-reference-architecture/policy-enforcement.md`
- `08-opinionated-implementations/`
- `07-leadership-conversations/`

---

## A Shared Mental Model

All audiences benefit from a shared understanding:

- Guardrails are **system protections**, not team punishments
- Enforcement increases with maturity
- Runtime safety is continuous, not a one-time gate

This repository exists to make that shared understanding explicit.

---

## Where to Go Next

- To understand **what runtime guardrails are** → `02-runtime-model/`
- To understand **where they live** → `03-reference-architecture/`
- To understand **how they are rolled out** → `06-rollout-playbooks/`

---

> **Runtime guardrails work best when everyone knows  
> what problem they solve — and what they don’t.**
