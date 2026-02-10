# Resource Baselines Guardrails

Resource baseline guardrails protect **cluster stability and fairness**
by defining how workloads consume shared resources.

They prevent:
- noisy neighbor failures
- cascading outages
- accidental denial of service

This pattern focuses on **safe defaults**, not tight control.

---

## Why This Pattern Exists

Without resource guardrails:
- one misconfigured pod can starve a node
- runaway workloads destabilize unrelated services
- clusters fail in non-obvious ways

Most incidents are not caused by bad actors —
they are caused by **missing boundaries**.

Resource baselines create those boundaries.

---

## What Resource Baselines Govern

Resource guardrails include:

- CPU and memory requests
- CPU and memory limits
- Namespace-level quotas
- Pod Disruption Budgets (PDBs)

They do **not**:
- optimize performance
- guarantee efficiency
- replace scaling strategies

They ensure **predictable behavior under load**.

---

## Requests vs Limits (Conceptual)

- **Requests**
  - Define scheduling guarantees
  - Enable fair placement
  - Protect workloads from starvation

- **Limits**
  - Define hard ceilings
  - Prevent runaway consumption
  - Protect the node and cluster

Safe systems require **both**.

---

## Namespace-Level Quotas

Quotas protect the cluster by:
- preventing uncontrolled growth
- enforcing capacity awareness
- encouraging intentional scaling decisions

They:
- apply at the system boundary
- shift decisions earlier
- reduce surprise failures

Quotas should be:
- generous by default
- adjustable with justification
- visible and explainable

---

## Pod Disruption Budgets (PDBs)

PDBs are **availability guardrails**, not performance tools.

They ensure:
- critical workloads remain available during maintenance
- automated operations do not cause outages
- disruption is intentional, not accidental

PDBs express:
> “How much disruption is acceptable?”

---

## Progressive Enforcement Model

### Phase 1: Observe
- Collect resource usage signals
- Identify misconfigured workloads
- Educate teams on requests and limits

---

### Phase 2: Default
- Apply baseline requests and limits
- Provide opt-out paths with justification
- Avoid breaking existing workloads

---

### Phase 3: Enforce
- Require explicit requests
- Enforce minimum safety thresholds
- Protect system stability automatically

---

## Relationship to Other Guardrails

- **Admission Control**
  - Enforces presence of resource settings
- **Namespaces & RBAC**
  - Define scope of quotas
- **Pod Security**
  - Prevents privileged abuse of resources

Together, these guardrails protect **shared infrastructure**.

---

## Common Failure Modes

- Setting limits too low and blaming teams
- Treating quotas as performance tuning
- Applying one-size-fits-all defaults
- Enforcing before understanding usage

---

## Key Principle

> **Resource constraints protect everyone — including the team that sets them.**

Well-designed baselines enable autonomy
by removing accidental risk.
