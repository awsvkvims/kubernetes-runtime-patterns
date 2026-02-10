# Pod Security Standards Guardrails

Pod Security Standards (PSS) guardrails define **what workloads are allowed to do**
once they are running in the cluster.

They protect:
- cluster integrity
- node security
- shared infrastructure

This pattern focuses on **preventing unsafe workload behavior by default**,
not auditing after the fact.

---

## Why This Pattern Exists

Common enterprise risks:
- Privileged containers running unnecessarily
- Host filesystem mounts used casually
- Containers running as root by default
- Capabilities granted without justification

Once a pod is running, these risks are:
- invisible to CI/CD
- difficult to detect at runtime
- catastrophic when exploited

PSS guardrails stop unsafe workloads **before they run**.

---

## What Pod Security Standards Govern

Pod Security guardrails constrain:

- Privileged containers
- Host namespace access (PID, IPC, network)
- HostPath volumes
- Linux capabilities
- Running as root
- Seccomp and security profiles

They do **not**:
- replace image scanning
- replace runtime monitoring
- guarantee application-level security

They define **baseline safety for execution**.

---

## Conceptual Security Levels

Pod Security Standards define increasing levels of restriction.

### Privileged
- No meaningful restrictions
- Intended for infrastructure components only

Use sparingly and explicitly.

---

### Baseline
- Prevents known dangerous configurations
- Allows most application workloads

Good default for:
- general application namespaces
- early adoption phases

---

### Restricted
- Enforces least privilege
- Strong isolation from the host

Best for:
- production workloads
- sensitive services
- multi-tenant clusters

---

## Progressive Enforcement Model

Pod security should follow a **maturity-based rollout**.

### Phase 1: Observe
- Enable audit/warn modes
- Identify violations
- Understand workload impact

Goal:
- learn before enforcing
- avoid breaking production

---

### Phase 2: Warn
- Surface violations early
- Require teams to acknowledge and remediate

Goal:
- shift left awareness
- build muscle memory

---

### Phase 3: Enforce
- Block non-compliant pods
- Allow explicit, documented exceptions

Goal:
- establish safe defaults
- reduce systemic risk

---

## Namespace-Based Guardrails

PSS is most effective when applied per namespace.

Typical model:
- Platform namespaces → privileged (explicit)
- Shared services → baseline
- Application namespaces → restricted

This aligns security posture with **risk and ownership**.

---

## Relationship to Other Guardrails

- **Admission Control**
  - enforces pod security at creation time
- **Namespaces & RBAC**
  - define scope of enforcement
- **Network Policies**
  - control lateral movement after execution

PSS guardrails ensure that even allowed workloads
cannot compromise the cluster.

---

## Common Failure Modes

- Enforcing restricted everywhere immediately
- Granting blanket exemptions without expiry
- Treating violations as team failures
- Allowing “temporary” exceptions to become permanent

---

## Key Principle

> **Most workloads do not need privilege — they inherit it by accident.**

Pod Security guardrails remove accidental power
and make intentional risk explicit.