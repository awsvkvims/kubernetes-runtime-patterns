# Network Policies Guardrails

Network policies guardrails define **which workloads can communicate**
inside the cluster (east–west) and, where applicable, what traffic is allowed
to/from the outside (north–south).

They exist to:
- Reduce blast radius
- Prevent lateral movement
- Make dependencies explicit
- Improve resilience during incidents

This is a runtime isolation pattern, not a firewall configuration exercise.

---

## Why This Pattern Exists

Common enterprise failure modes:
- Everything can talk to everything
- Incidents spread laterally across services
- Sensitive services are reachable from unrelated workloads
- Dependencies are implicit and undocumented

When the network is permissive, safety relies on:
- perfect application behavior
- perfect identity and secrets hygiene
- perfect human discipline

Network policy guardrails reduce the need for perfection.

---

## Core Guardrail Principles

### 1. Default Allow Is the Hidden Risk
In most clusters, if no policies exist, traffic is effectively open.

Key invariant:
> **If you don’t explicitly allow it, you should assume it is allowed.**

Guardrails invert this over time.

---

### 2. Policies Encode Intent, Not Implementation
Network policies should describe:
- what needs to talk to what
- on which ports/protocols
- within which boundaries (namespace, workload identity)

They should not become:
- a low-level IP management system
- a reactive incident patching tool

---

### 3. Make Dependencies Explicit
Network policies are a forcing function:
- service dependencies become visible
- undocumented coupling is exposed
- architecture drift becomes detectable

This improves both security and reliability.

---

## Progressive Enforcement Model

Network policies should be rolled out gradually.

### Phase 1: Observe (dependency discovery)
- Inventory service-to-service communication
- Identify critical dependency paths
- Do not enforce yet

Purpose:
- prevent surprise outages
- build an allow-list based on reality

---

### Phase 2: Constrain (soft boundaries)
- Introduce namespace boundary policies
- Allow intra-namespace traffic
- Restrict cross-namespace traffic

Purpose:
- reduce lateral blast radius
- avoid breaking common within-team communication

---

### Phase 3: Default-Deny (strict boundaries)
- Default-deny ingress for sensitive namespaces/workloads
- Allow only explicit callers
- Expand scope gradually

Purpose:
- enforce least privilege for network access
- stop implicit dependencies from growing

---

## Common Network Policy Guardrail Patterns

### Namespace Isolation
- Default-deny cross-namespace traffic
- Allow only approved flows (e.g., ingress controller → backend)

Use when:
- multiple teams share a cluster
- you need clear blast-radius boundaries

---

### Sensitive Workload Protection
- Default-deny ingress to high-risk services
- Allow only specific callers on specific ports

Use when:
- workloads handle credentials, PII, payments, identity, admin functions

---

### Egress Control (when needed)
- Restrict outbound traffic from workloads
- Allow only approved destinations

Use when:
- compliance requires outbound controls
- you want to reduce data exfiltration risk

Note:
Egress policy maturity tends to come later due to operational complexity.

---

## Environment-Aware Enforcement

Typical progression:
- Development: broad allow, observe dependencies
- Staging: namespace isolation, selective deny
- Production: explicit allow-lists for sensitive workloads

Goal:
- learn safely
- enforce where risk is highest

---

## Relationship to Other Guardrails

- **Namespaces & RBAC**
  - define who can act
  - define tenancy boundaries

- **Config & Secrets**
  - protect sensitive data
  - reduce impact of compromised access

- **Admission Control**
  - ensures policies are applied consistently
  - can prevent workloads from bypassing required labels/selectors

Network policy guardrails make runtime coupling visible and controllable.

---

## Common Failure Modes

- Starting with cluster-wide default-deny without discovery
- Treating policies as “security’s job” rather than architecture
- Encoding ephemeral implementation details (IPs, node ports)
- Allowing exceptions that never expire
- Not providing a clear “how to unblock safely” path

---

## Key Principle

> **The safest dependency is the one that is explicitly allowed.**

Network guardrails should make safe communication easy,
and unsafe lateral movement difficult by default.
