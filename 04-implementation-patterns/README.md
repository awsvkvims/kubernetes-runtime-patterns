# Implementation Patterns

This section describes **how runtime guardrails are implemented in practice**
across Kubernetes control-plane surfaces.

These documents focus on **patterns**, not tools.

They are intended to:
- Be reused across environments and platforms
- Scale with organizational maturity
- Remain stable even as tooling changes

---

## How to Use This Section

Start with the pattern that matches **where enforcement happens**, not the tool you plan to use.

Each pattern document explains:
- When the guardrail applies
- What problems it is best suited for
- How enforcement should mature over time
- How it connects to other guardrails

---

## Patterns in This Section

### Admission Control
**Prevent unsafe configurations from entering the cluster**

- API-level enforcement
- Strongest preventive boundary
- Suitable for non-negotiable invariants

→ [Admission Control Guardrails](admission-control.md)

---

### Configuration & Secrets
**Protect sensitive configuration and secret handling**

- Separation of config vs code
- Secret injection patterns
- Runtime exposure boundaries

→ [Configuration & Secrets](config-and-secrets.md)

---

### Namespaces & RBAC
**Isolate workloads and control access**

- Multi-tenancy boundaries
- Least-privilege access
- Blast-radius containment

→ [Namespaces & RBAC](namespaces-and-rbac.md)

---

### Network Policies
**Control east–west and north–south traffic**

- Default-deny models
- Service-level isolation
- Runtime communication constraints

→ [Network Policies](network-policies.md)

---

### Pod Security Standards
**Enforce baseline workload security posture**

- Privilege constraints
- Capability restrictions
- Host access controls

→ [Pod Security Standards](pod-security-standards.md)

---

### Resource Baselines
**Prevent noisy-neighbor and cluster exhaustion**

- Requests and limits
- Quotas
- Disruption protection

→ [Resource Baselines](resource-baselines.md)

---

### Progressive Hardening
**Safely increase enforcement over time**

- Maturity-based rollout
- Environment-specific enforcement
- Trust-preserving adoption

→ [Progressive Hardening](progressive-hardening.md)

---

## Relationship to Other Sections

- **Runtime Model** explains *what* guardrails exist  
  → `02-runtime-model/`

- **Reference Architecture** explains *where* they live  
  → `03-reference-architecture/`

- **Sample Assets** show *how they look in practice*  
  → `05-sample-assets/`

---

## Guiding Principle

> **Patterns should outlive tools.**

If a pattern becomes tightly coupled to a specific product,
it no longer scales across teams or time.