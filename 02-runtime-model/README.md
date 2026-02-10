# Runtime Model

This folder defines a **tool-agnostic model** for Kubernetes runtime guardrails.

Start here:

- **[Runtime Guardrail Categories](runtime-guardrail-categories.md)**  
  Preventive vs Detective vs Corrective — and how they work together.

## How to use this model

Use this model to:
- classify runtime controls by intent (not tooling)
- design layered enforcement (warn → block → auto-correct)
- avoid treating runtime safety as “just observability”

## Where this connects

- Visual orientation: [`../ARCHITECTURE-AT-A-GLANCE.md`](../ARCHITECTURE-AT-A-GLANCE.md)
- Kubernetes mapping (next): `03-reference-architecture/`