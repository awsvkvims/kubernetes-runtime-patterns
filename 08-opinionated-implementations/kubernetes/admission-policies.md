# Admission Policies (Runtime Prevention)

Admission policies are **preventive runtime guardrails** enforced at the Kubernetes API boundary.

They stop unsafe or non-compliant workloads from ever entering the cluster — regardless of
how they were built or deployed.

---

## What Admission Policies Are

Admission policies:
- Intercept requests to the Kubernetes API
- Validate or mutate resource specifications
- Allow or deny objects before persistence

They operate **before anything runs**.

---

## What Admission Policies Are Not

Admission policies are not:
- CI/CD checks
- Code review gates
- Runtime monitoring
- Incident response mechanisms

They are **last-line prevention**, not first-line feedback.

---

## Common Admission Policy Categories

### 1. Security & Isolation

Examples:
- Block privileged containers
- Enforce non-root execution
- Restrict hostPath volumes
- Enforce namespace isolation boundaries

Why:
- Prevent high-blast-radius workloads
- Enforce baseline security posture uniformly

---

### 2. Configuration Safety

Examples:
- Require resource requests/limits
- Enforce PodDisruptionBudgets
- Block unsafe replica counts
- Enforce image pull policies

Why:
- Prevent noisy neighbors
- Protect cluster stability

---

### 3. Policy Compliance

Examples:
- Require labels/annotations
- Enforce ownership metadata
- Require approved runtime classes
- Enforce scheduling constraints

Why:
- Enable traceability
- Support automation and governance

---

## Enforcement Progression (Opinionated)

Admission policies should **progress over time**, not start fully blocking.

| Maturity Stage | Enforcement Mode | Typical Use |
|----------------|------------------|-------------|
| Observe        | Audit only       | Learn current behavior |
| Warn           | Allow + warn     | Socialize expectations |
| Block          | Deny unsafe specs| Protect production |
| Mutate         | Auto-fix defaults| Reduce friction |

Blocking is **earned**, not imposed.

---

## Platform vs Team Responsibilities

**Platform owns:**
- Policy definitions
- Enforcement consistency
- Exception mechanisms

**Teams own:**
- Meeting policy intent
- Fixing violations
- Requesting justified exceptions

---

## CI/CD vs Runtime Boundary

CI/CD guardrails should:
- Catch most violations early
- Provide fast feedback

Admission policies exist because:
- CI/CD can be bypassed
- Runtime drift happens
- Not all risks are visible pre-deploy

> **If something must never run, it belongs here.**

---

## Interview / Review Talk Track

> “Admission policies are our safety net.  
> CI/CD helps teams move fast, but admission control ensures the cluster never accepts unsafe workloads — consistently, automatically, and without human approval.”

---

## What This Document Avoids (Intentionally)

- Vendor tools
- YAML examples
- Policy syntax
- Environment-specific rules

Those belong in **example repos**, not in the core pattern.
