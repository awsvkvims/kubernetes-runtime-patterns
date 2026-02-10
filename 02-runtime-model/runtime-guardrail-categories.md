# Runtime Guardrail Categories

## Purpose

Define a **tool-agnostic taxonomy** for Kubernetes runtime guardrails.

This is a thinking model used to:
- classify controls by intent
- design layered enforcement
- avoid “one tool = one guardrail” thinking

This document does **not** prescribe tools, YAML, or vendor products.

---

## What is a Runtime Guardrail?

A **runtime guardrail** is a control that operates **after workloads reach the cluster** and helps keep the system safe by:

- preventing unsafe states from entering
- detecting unsafe conditions while running
- correcting or containing problems automatically

Runtime guardrails exist because:
- not all risks can be detected pre-deploy
- live systems drift
- incidents happen even with strong CI/CD controls

---

## The Three Categories

This repository groups runtime guardrails by **intent**:

### 1) Preventive Guardrails

**Goal:** Stop unsafe states from entering the system.

**Where they commonly live in Kubernetes:**  
Admission control and policy enforcement boundaries.

**Examples (conceptual, not tool-specific):**
- deny privileged containers
- require resource requests/limits
- require approved registries/images
- enforce namespace boundaries / labeling rules

**Typical failure mode if missing:**  
Unsafe configurations get deployed and become hard to unwind later.

---

### 2) Detective Guardrails

**Goal:** Detect risk, drift, or violations while the system is running.

**Where they commonly live in Kubernetes:**  
Observability pipelines, runtime signals, continuous evaluation.

**Examples (conceptual):**
- detect workloads violating network boundaries
- detect image drift or configuration drift
- detect anomalous behavior (spikes, unusual calls, unexpected egress)

**Typical failure mode if missing:**  
You learn about problems only after customer impact (or never).

---

### 3) Corrective Guardrails

**Goal:** Reduce blast radius and restore safety automatically.

**Where they commonly live in Kubernetes:**  
Controllers, operators, automation systems.

**Examples (conceptual):**
- quarantine or isolate suspicious workloads
- auto-rollback to last known safe version (under controlled conditions)
- apply compensating controls (tighten network policy, scale down, evict)

**Typical failure mode if missing:**  
Incidents require manual heroics and take too long to recover.

---

## How Categories Work Together

A mature system uses all three:

- **Preventive** reduces the chance of unsafe states
- **Detective** ensures unsafe behavior is visible quickly
- **Corrective** limits blast radius and speeds recovery

Many real controls span categories depending on enforcement mode:
- warn → block → auto-correct (maturity progression)

---

## Relationship to CI/CD Guardrails

CI/CD guardrails reduce risk **before deployment**.
Runtime guardrails manage risk **after deployment**.

Both are needed.

See:  
- `ARCHITECTURE-AT-A-GLANCE.md` → “CI/CD vs Runtime Guardrails (Boundary)”
- `03-reference-architecture/` → where runtime guardrails live in the cluster

---

## Outcome: What This Enables

Using this model, you can answer:
- What are we preventing vs detecting vs correcting?
- What are we warning on today that we might enforce later?
- Where should we invest to improve safety without approvals?
