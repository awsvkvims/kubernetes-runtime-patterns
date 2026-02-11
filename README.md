# Kubernetes Runtime Guardrails

This repository defines a **platform-first approach to runtime governance in Kubernetes**.

It focuses on enforcing **safety, isolation, and reliability guarantees at runtime** —
*inside the cluster* — without relying on manual approvals, ticket-based processes,
or brittle pre-deployment gates.

Runtime guardrails complement CI/CD guardrails.
They do not replace them.

---

## Core Idea

> **CI/CD guardrails protect artifacts.  
> Runtime guardrails protect the system.**

Once workloads are running in a shared Kubernetes environment:
- Drift is possible
- Behavior matters more than intent
- Safety must be enforced continuously

Runtime guardrails exist to:
- Prevent unsafe states from entering the cluster
- Detect risk and drift while workloads are running
- Correct or contain failures automatically
- Preserve team autonomy while scaling trust

---

## What This Repository Is

- A **reference model** for Kubernetes runtime guardrails
- A **platform design guide** for shared and multi-tenant clusters
- A collection of **patterns, playbooks, and opinionated examples**
- A companion to:
  - **Platform CI/CD Guardrails**
  - **Engineering Productivity Metrics**

---

## What This Repository Is Not

- A CI/CD pipeline guide
- A shift-left security checklist
- A vendor or tool comparison
- A replacement for engineering ownership

This repository intentionally avoids:
- Approval workflows
- Team-level policing
- Policy sprawl without platform support

---

## How This Fits Into the Portfolio

This repository is one part of a larger, cohesive platform story:

- **Platform CI/CD Guardrails**  
  Enforce policy *before* artifacts reach the cluster  
  → provenance, release controls, pipeline governance

- **Kubernetes Runtime Guardrails** *(this repo)*  
  Enforce safety *inside* the cluster, continuously  
  → isolation, admission control, runtime detection, correction

- **Engineering Productivity Metrics**  
  Provide signals that guide investment and improvement  
  → flow, reliability, enablement

Together, they replace approvals with architecture.

---

## Repository Orientation

If you are new, start with:

- **[Architecture at a Glance](ARCHITECTURE-AT-A-GLANCE.md)**  
  Visual map of how all concepts fit together

- **[Runtime Guardrail Categories](02-runtime-model/runtime-guardrail-categories.md)**  
  The conceptual model: preventive, detective, corrective

- **[System Overview](03-reference-architecture/system-overview.md)**  
  Where runtime guardrails live in Kubernetes

---

## Who This Is For

### Platform & SRE Teams
Designing and operating shared Kubernetes platforms.

Start here:
- `02-runtime-model/`
- `03-reference-architecture/`
- `04-implementation-patterns/`
- `08-opinionated-implementations/kubernetes/`

---

### Application Teams & Tech Leads
Running workloads in governed clusters without losing autonomy.

Start here:
- `06-rollout-playbooks/onboarding-a-team.md`
- `06-rollout-playbooks/moving-from-dev-to-prod.md`
- `04-implementation-patterns/`

---

### Engineering Leadership
Funding platforms instead of approvals.

Start here:
- `ARCHITECTURE-AT-A-GLANCE.md`
- `07-leadership-conversations/`
- `06-rollout-playbooks/`

---

## How to Read This Repository

This repository is **not meant to be read linearly**.

Start with the question you are trying to answer:

- *“What must be enforced at runtime vs CI/CD?”*  
  → `00-overview/runtime-guardrails-vs-cicd-guardrails.md`

- *“What kinds of runtime guardrails exist?”*  
  → `02-runtime-model/runtime-guardrail-categories.md`

- *“Where do these guardrails actually live in Kubernetes?”*  
  → `03-reference-architecture/system-overview.md`

- *“How do we roll this out without breaking trust?”*  
  → `06-rollout-playbooks/`

---

## Guiding Principle

> **If teams experience governance as friction, the platform has failed.**

Well-designed runtime guardrails:
- Are invisible during normal operation
- Provide fast, clear feedback when violated
- Reduce blast radius instead of assigning blame
- Scale trust through system design

---

## Status

Reference architecture and core patterns established.  
Starter assets and opinionated implementations continue to evolve.
