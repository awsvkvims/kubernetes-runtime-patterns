# Runtime Guardrail Categories

## Purpose

Define a **tool-agnostic taxonomy** for Kubernetes runtime guardrails.

This is a thinking model used to:
- classify controls by intent
- design layered enforcement
- avoid “one tool = one guardrail” thinking

This document does **not** prescribe tools, YAML, or vendor products.

---

## How to Think About Guardrail Categories

Runtime guardrails are **not a maturity ladder** where teams “graduate” from one type to another.

Healthy production systems require **all three categories operating together**:

- **Preventive guardrails** reduce the likelihood of unsafe states
- **Detective guardrails** surface risk and drift that inevitably emerges
- **Corrective guardrails** limit blast radius and restore safety when prevention fails

As systems scale, **no amount of prevention eliminates the need for detection and correction**.
The goal is not perfection — it is *resilience*.

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

**Decision Focus**
Preventive guardrails support decisions such as:

- *“What must never be allowed to enter the cluster?”*
- *“Which configurations are fundamentally unsafe regardless of context?”*
- *“What defaults should teams inherit so they don’t have to think about safety every time?”*

These guardrails are cheapest to enforce and reduce downstream operational load,
but they are intentionally conservative and cannot cover every runtime risk.

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

**Decision Focus**
Detective guardrails support decisions such as:

- *“Where is the system drifting away from intended state?”*
- *“What risk is accumulating silently over time?”*
- *“Which teams or workloads need enablement or attention — without blame?”*

Detection does not imply failure.
In complex systems, **drift is expected** — the question is whether it is visible early enough to act safely.

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

**Decision Focus**
Corrective guardrails support decisions such as:

- *“How do we limit blast radius when something goes wrong?”*
- *“What actions can be automated to restore safety faster than humans?”*
- *“Which failures should self-heal vs. escalate to operators?”*

Corrective guardrails acknowledge reality:
some unsafe states will reach production despite prevention and detection.
Automation here is about **speed, consistency, and safety**, not punishment.

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

## Relationship to Enforcement Levels

Each runtime guardrail category can exist at **different enforcement strengths**:

- Observe (signal only)
- Warn (visible feedback)
- Block (hard enforcement)
- Auto-correct (self-healing)

For example:
- A preventive guardrail may start as *warn-only* before becoming *blocking*
- A detective guardrail may surface signals long before automation is introduced
- A corrective guardrail may begin as manual runbooks before automation is added

Enforcement strength evolves over time as trust, maturity, and confidence increase.

---

## Outcome: What This Enables

Using this model, you can answer:
- What are we preventing vs detecting vs correcting?
- What are we warning on today that we might enforce later?
- Where should we invest to improve safety without approvals?

---

## Related Model Elements

This conceptual model connects directly to:

- **[Enforcement Levels](enforcement-levels.md)** — how strongly guardrails act
- **[Shared Responsibility](shared-responsibility.md)** — who owns which controls
- **[Service Runtime Contract](service-runtime-contract.md)** — expectations placed on workloads
- **[Architecture at a Glance](../ARCHITECTURE-AT-A-GLANCE.md)** — visual mapping of this model

Together, these documents form the **runtime governance backbone** of this repository.
