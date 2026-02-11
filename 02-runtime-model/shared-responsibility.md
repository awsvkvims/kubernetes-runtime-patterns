# Shared Responsibility at Runtime

This document defines **who owns what** when runtime guardrails are in place.

Runtime guardrails do not eliminate responsibility — they **redistribute it deliberately**
so that safety, autonomy, and scale can coexist.

---

## Why Shared Responsibility Matters

Without a clear responsibility model:

- Platform teams become approval bottlenecks
- Application teams disengage from runtime safety
- Security teams compensate with manual controls
- Incidents trigger blame instead of learning

Runtime guardrails work only when **ownership is explicit and respected**.

---

## Core Principle

> **The platform enforces guardrails.  
Teams own their workloads.  
Security defines intent.  
Leaders fund constraints removal.**

No single group owns runtime safety end-to-end.

---

## Responsibility Layers

### Platform Teams Own

Platform teams are responsible for **providing safe, consistent runtime boundaries**.

They own:
- Cluster architecture and control planes
- Admission control mechanisms
- Baseline policies and defaults
- Enforcement mechanisms and escalation paths
- Observability for guardrail behavior

They do **not**:
- Approve deployments
- Own application correctness
- Write application-specific policy logic
- Bypass guardrails on behalf of teams

---

### Application Teams Own

Application teams are responsible for **operating safely within guardrails**.

They own:
- Workload configuration
- Resource requests and limits
- Runtime behavior and health
- Responding to guardrail feedback
- Requesting changes via defined contracts

They do **not**:
- Modify cluster-wide enforcement
- Override guardrails unilaterally
- Depend on platform teams for routine decisions

---

### Security & Risk Teams Own

Security teams define **policy intent**, not enforcement mechanics.

They own:
- Risk models and threat assumptions
- Policy objectives (what must be prevented, detected, corrected)
- Exception criteria and escalation rules
- Review of guardrail effectiveness

They do **not**:
- Operate runtime systems
- Review every deployment
- Encode policy directly into pipelines or manifests

---

### Leadership Owns

Leadership owns **investment decisions and tradeoffs**.

They own:
- Funding platform capabilities
- Setting acceptable risk tolerance
- Prioritizing constraint removal
- Reinforcing non-punitive guardrail usage

They do **not**:
- Use guardrails for performance management
- Demand exceptions without tradeoff discussion
- Treat guardrails as a substitute for strategy

---

## How Guardrails Shift Responsibility

| Without Guardrails | With Guardrails |
|-------------------|-----------------|
| Humans review changes | Systems enforce constraints |
| Teams ask permission | Teams operate within contracts |
| Security chases violations | Policy is continuously enforced |
| Leaders intervene late | Leaders see risk early |

Guardrails **shift responsibility left and down**, not up.

---

## Shared Responsibility Is Enforced by Design

This model works because:
- Guardrails are embedded at control-plane boundaries
- Enforcement is automatic and consistent
- Exceptions are explicit and auditable
- Feedback is visible but non-punitive

Responsibility is not negotiated during incidents — it is **designed upfront**.

---

## Relationship to Other Model Elements

This document connects to:

- **[Runtime Guardrail Categories](runtime-guardrail-categories.md)** — what is enforced
- **[Enforcement Levels](enforcement-levels.md)** — how strongly enforcement acts
- **[Service Runtime Contract](service-runtime-contract.md)** — how teams interface with the platform
- **[Rollout Playbooks](../06-rollout-playbooks/)** — how this model is introduced safely
- **[Leadership Conversations](../07-leadership-conversations/)** — how responsibility is explained

Together, these define **runtime safety without centralized control**.