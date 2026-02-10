# Namespaces & RBAC Guardrails

Namespaces and RBAC guardrails define **who can act, where they can act,
and what impact their actions can have at runtime**.

They exist to:
- Contain blast radius
- Prevent accidental privilege escalation
- Enable multi-team clusters without chaos

This is an **authorization and isolation pattern**, not an access convenience.

---

## Why This Pattern Exists

Common failure modes in Kubernetes environments:
- Everyone is cluster-admin “temporarily”
- Teams share namespaces “for speed”
- Service accounts are reused across workloads
- Access is granted once and never revisited

These failures are systemic — not individual mistakes.

Namespaces and RBAC guardrails prevent them **by design**.

---

## Core Guardrail Principles

### 1. Namespaces Are Isolation Boundaries
Namespaces are not folders.

They define:
- Resource scope
- Network boundaries
- Policy application zones
- Failure containment

Key invariant:
> **A namespace should represent a meaningful blast-radius boundary.**

---

### 2. RBAC Is a Safety System, Not a Convenience Tool
RBAC exists to:
- Limit impact of mistakes
- Prevent privilege creep
- Make unsafe actions impossible

RBAC should:
- Be minimal by default
- Be explicit when elevated
- Expire when no longer needed

---

### 3. Separation of Human and Workload Identity

Human access and workload access serve different purposes.

Guardrails enforce:
- Humans do not impersonate workloads
- Workloads do not inherit human permissions
- Automation uses scoped, purpose-built identities

Why:
- Reduces credential misuse
- Improves auditability
- Enables safer automation

---

## Namespace Guardrail Patterns

Common guardrails include:
- One workload domain per namespace
- No shared “catch-all” namespaces
- Explicit ownership per namespace
- Policy applied at namespace boundaries

Anti-patterns:
- “default” namespace usage
- Environment-per-namespace without isolation
- Shared namespaces across teams

---

## RBAC Guardrail Patterns

Effective RBAC guardrails:
- Prefer deny-by-default models
- Grant verbs intentionally (read vs write vs admin)
- Separate deploy permissions from operate permissions
- Scope access to namespaces, not clusters

Avoid:
- Broad wildcard permissions
- Cluster-admin for day-to-day work
- Long-lived elevated roles

---

## Progressive Enforcement Model

### Phase 1: Observe
- Inventory existing permissions
- Identify over-privileged roles
- Map namespace ownership

---

### Phase 2: Warn
- Surface risky access patterns
- Highlight shared or privileged roles
- Provide safer defaults

---

### Phase 3: Enforce
- Block unsafe role bindings
- Require namespace ownership metadata
- Prevent cross-namespace privilege escalation

---

## Environment-Aware Enforcement

Typical progression:
- Development: flexible, observable
- Staging: scoped, warned
- Production: strict, enforced

This supports learning without compromising safety.

---

## Relationship to Other Guardrails

- **Admission Control**
  - Prevents unsafe specs
  - Ensures RBAC rules are applied consistently

- **Config & Secrets Guardrails**
  - Limit access to sensitive data
  - Enforce least privilege at runtime

- **Runtime Detection**
  - Surfaces anomalous access
  - Detects drift from intended permissions

---

## Key Principle

> **Access should be easy to do safely, and hard to do dangerously.**

Namespaces and RBAC guardrails scale trust by shrinking blast radius,
not by slowing teams down.
