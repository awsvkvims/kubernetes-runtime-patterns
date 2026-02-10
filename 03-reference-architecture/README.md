# Reference Architecture

This folder describes **where runtime guardrails live** in a Kubernetes-based platform
and **how enforcement is distributed across control planes**.

It intentionally avoids:
- vendor-specific tooling
- YAML or policy syntax
- environment-specific layouts

The goal is architectural clarity, not implementation detail.

---

## What this section answers

Use this section to understand:

- Where preventive guardrails are enforced
- Where runtime signals are generated
- Where corrective action is safely applied
- Why Kubernetes is a natural enforcement surface

This maps directly to **Diagram 3** in the architecture overview.

---

## Key concepts

Runtime guardrails align to **Kubernetes control-plane responsibilities**, not pipelines:

- Admission control → prevent unsafe states
- Controllers → enforce desired state
- Observability → detect drift and violations

Guardrails are strongest when embedded at these boundaries,
not bolted on as reactive tooling.

---

## Start here

- **[System Overview](system-overview.md)**  
  High-level mapping of guardrail types to Kubernetes control planes

---

## How this connects

- Conceptual model: `02-runtime-model/`
- Implementation patterns: `04-implementation-patterns/`
- Visual orientation: [`../ARCHITECTURE-AT-A-GLANCE.md`](../ARCHITECTURE-AT-A-GLANCE.md)
