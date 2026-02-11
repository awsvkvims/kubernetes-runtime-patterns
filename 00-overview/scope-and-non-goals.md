# Scope and Non-Goals

This document defines **what this repository is explicitly responsible for**
and, just as importantly, **what it is not**.

Clear boundaries prevent misuse, overextension, and misaligned expectations —
especially in large organizations.

---

## In Scope

This repository focuses on **runtime guardrails in Kubernetes-based platforms**.

Specifically, it covers:

### 1. Runtime Safety and Control
Guardrails that:
- Prevent unsafe configurations from entering a cluster
- Detect drift, violations, or anomalous behavior at runtime
- Correct or contain risk automatically when possible

These guardrails operate **inside the running system**, not only before deployment.

---

### 2. Platform-Enforced Constraints
Controls that are:
- Centrally defined by platform teams
- Enforced consistently across workloads
- Transparent and explainable to teams

Examples include:
- Admission policies
- Resource and isolation boundaries
- Network segmentation
- Runtime enforcement of platform contracts

---

### 3. Architectural Patterns (Not Tool Tutorials)
The repository provides:
- Conceptual models
- Reference architectures
- Implementation patterns
- Rollout playbooks

It emphasizes **why and where** guardrails belong,
before **how** they are implemented.

---

### 4. Organizational Enablement
This repository also covers:
- How guardrails replace manual approvals
- How enforcement matures over time
- How trust is scaled without slowing teams

These are **socio-technical systems**, not just Kubernetes configurations.

---

## Explicit Non-Goals

This repository intentionally does **not** attempt to do the following:

---

### 1. CI/CD Pipeline Governance
This repo does **not** define:
- Pipeline design standards
- Build or test strategies
- Artifact promotion workflows
- Release orchestration

Those concerns belong in:
- Platform CI/CD Guardrails
- Engineering Productivity Metrics

See also:
- `runtime-guardrails-vs-cicd-guardrails.md`

---

### 2. Tool-Specific How-To Guides (by Default)
This repository avoids:
- Step-by-step vendor tutorials
- Opinionated tooling mandates
- Environment-specific scripts

Tool-specific examples live under:
- `08-opinionated-implementations/`
and are clearly marked as such.

---

### 3. Application-Level Design
This repository does **not** prescribe:
- Service architectures
- Framework choices
- Coding standards
- Business logic patterns

Guardrails operate **around applications**, not inside their codebases.

---

### 4. Human Approval Processes
This repository explicitly rejects:
- Manual gates
- Approval boards
- Ticket-driven deployment permissioning

If humans are required to approve every change,
the system has already failed.

---

### 5. Compliance Checklists
This repository does **not** provide:
- Audit checklists
- Certification mappings
- Regulatory interpretations

Instead, it focuses on **building systems that make compliance emergent**.

---

## Why These Boundaries Matter

Runtime guardrails are most effective when:
- Their scope is narrow and intentional
- Their enforcement is systemic, not discretionary
- Their purpose is safety, not control

Blurring boundaries leads to:
- Over-centralization
- Loss of team trust
- Guardrails being bypassed or disabled

---

## Where to Go Next

If you are:
- Clarifying **who this repository is for** → see `audiences-and-use-cases.md`
- Comparing runtime vs pipeline controls → see `runtime-guardrails-vs-cicd-guardrails.md`
- Looking for enforcement models → see `02-runtime-model/`

---

> **Guardrails succeed when teams rarely notice them —  
> and trust them when they do.**