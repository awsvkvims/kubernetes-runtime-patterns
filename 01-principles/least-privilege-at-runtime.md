# Least Privilege at Runtime

This principle states that **workloads should run with the minimum privileges required to function — and no more**.

At runtime, excess privilege is not convenience.
It is **latent blast radius**.

---

## Why Runtime Privilege Is Different

At build time, privilege is mostly theoretical.
At runtime, privilege is **executable**.

Excess runtime privilege allows:
- Cross-namespace access
- Data exfiltration
- Lateral movement
- Accidental or malicious cluster impact

Least privilege at runtime is about **containing failure**, not distrusting teams.

---

## Core Principle

> **Every workload should be constrained to the smallest possible scope — by default.**

Access must be:
- Explicit
- Justified
- Observable
- Revocable

---

## What Least Privilege Means in Practice

Least privilege at runtime applies across multiple dimensions:

### Identity & Access
- Service accounts are namespace-scoped
- No default cluster-wide permissions
- RBAC grants are narrow and role-specific

---

### Network Access
- Default-deny network policies
- Explicit egress and ingress rules
- No implicit trust between workloads

---

### Execution Context
- No privileged containers by default
- No hostPath mounts without justification
- No host networking unless explicitly allowed

---

### Resource Consumption
- CPU and memory limits enforced
- No unlimited requests
- Fair usage across tenants

---

## Why This Is a Platform Responsibility

Expecting teams to self-enforce least privilege does not scale.

Reasons:
- Teams optimize for delivery, not containment
- Runtime risk is cross-cutting
- One misconfigured workload can impact many teams

Therefore:

> **Least privilege must be enforced by the platform, not requested by teams.**

---

## How This Principle Shows Up in Guardrails

Least privilege is enforced through:
- Admission policies
- Namespace isolation
- RBAC boundaries
- Network policies
- Resource quotas and limits

See:
- `04-implementation-patterns/namespaces-and-rbac.md`
- `04-implementation-patterns/network-policies.md`
- `04-implementation-patterns/resource-baselines.md`

---

## What This Principle Is NOT

Least privilege does **not** mean:
- Zero flexibility
- Excessive friction
- Manual approvals for access
- One-size-fits-all lockdowns

It means:
- Safe defaults
- Explicit escalation paths
- Progressive enforcement

---

## Relationship to Other Principles

This principle directly supports:
- **Platform Runtime Contract** — constraints are predictable
- **Default Secure, Default Operable** — safety without friction
- **Guardrails over approvals** — systems enforce boundaries

Least privilege is the **foundation** that makes all other runtime guardrails effective.
