# Kubernetes Opinionated Implementations

This folder provides an **opinionated, tool-agnostic** view of how runtime guardrails are commonly implemented
inside Kubernetes clusters.

It is intentionally **practical**:
- What gets enforced at admission time
- What gets detected at runtime
- What gets corrected automatically (or safely isolated)

This is not a full production blueprint. It is a starting point that maps cleanly to the repository’s runtime model.

---

## What You’ll Find Here

- **[Admission Policies](admission-policies.md)**  
  Prevent unsafe specs and configurations from entering the cluster (validate/mutate/deny).

- **[Runtime Detection](runtime-detection.md)**  
  Detect drift, violations, and anomalous behavior after workloads are running.

- **[Corrective Patterns](corrective-patterns.md)**  
  Safely reduce blast radius through isolation, remediation, and controlled rollback patterns.

---

## How This Connects to CI/CD Guardrails

CI/CD guardrails (from the platform CI/CD offering) enforce:
- Provenance, integrity, and policy before deploy

Kubernetes runtime guardrails enforce:
- Safety, isolation, and behavior while running

A healthy platform uses both:
- **CI/CD ensures “what we deploy is trusted.”**
- **Kubernetes ensures “what runs stays safe.”**

---

## Quick Role-Based Entry Points

- **Platform / Runtime Engineers**
  - Start with: [Admission Policies](admission-policies.md)
  - Then: [Runtime Detection](runtime-detection.md)
  - Then: [Corrective Patterns](corrective-patterns.md)

- **Developers / Teams**
  - Start with: [Admission Policies](admission-policies.md)
  - Focus on: “what will be rejected and why”

- **Leaders**
  - Start with: the repo-level Architecture at a Glance
  - Use these docs to understand “runtime enforcement boundaries”

---

## Guiding Principle

> **Runtime guardrails should be systemic, explainable, and boring.**

If runtime safety depends on manual review, it will not scale.
