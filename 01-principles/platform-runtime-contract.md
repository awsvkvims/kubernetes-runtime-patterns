# Platform Runtime Contract

A platform runtime contract defines the **explicit expectations** between
the platform and the teams running workloads on it.

It replaces implicit assumptions with **clear guarantees and responsibilities**.

---

## Core Principle

> **The platform provides safety, consistency, and guardrails.  
> Teams provide compliant workloads and operational ownership.**

Neither side succeeds without the other.

---

## Why a Runtime Contract Is Necessary

Without a contract:
- Guardrails feel arbitrary
- Teams experience surprise breakages
- Platform changes erode trust
- Exceptions proliferate

With a contract:
- Behavior is predictable
- Changes are intentional
- Guardrails feel fair
- Teams can design confidently

---

## What the Platform Guarantees

The platform guarantees:

### 1. Safety by Default
- Secure namespace isolation
- Baseline resource protections
- Restricted privilege escalation
- Network boundaries

Teams do not need to “opt in” to safety.

---

### 2. Stable Enforcement Semantics
- Clear enforcement levels (warn → block → correct)
- No sudden hard blocks without notice
- Consistent behavior across clusters and environments

See:
- `02-runtime-model/enforcement-levels.md`

---

### 3. Transparent Guardrails
- Guardrails are documented
- Violations produce clear feedback
- Signals explain *what* failed and *why*

No silent drops. No mystery denials.

---

### 4. Progressive Change
- Guardrails evolve gradually
- Migration paths are provided
- Deprecations are communicated

The platform does not change behavior without warning.

---

## What Teams Are Responsible For

Teams are responsible for:

### 1. Compliant Workloads
- Following supported workload patterns
- Staying within documented constraints
- Using provided templates and defaults

See:
- `05-starter-assets/`

---

### 2. Explicit Exceptions
- Declaring when they need deviations
- Understanding blast-radius implications
- Accepting increased scrutiny for exceptions

Exceptions are visible — not hidden.

---

### 3. Runtime Ownership
- Monitoring application health
- Responding to incidents
- Maintaining SLOs

Guardrails reduce risk — they do not run services.

---

## What This Contract Is Not

This contract is **not**:
- A compliance checklist
- A legal agreement
- A static document

It is a **living understanding** between platform and teams.

---

## How This Shows Up in Practice

This principle drives:
- Clear onboarding documentation
- Guardrail warnings before blocks
- Stable platform APIs
- Predictable rollout playbooks

See:
- `06-rollout-playbooks/onboarding-a-team.md`
- `06-rollout-playbooks/moving-from-dev-to-prod.md`

---

## Common Failure Mode This Prevents

Without a runtime contract:
- Teams blame the platform
- Platform blames teams
- Workarounds proliferate
- Trust collapses

With it:
- Tradeoffs are explicit
- Changes are expected
- Guardrails feel collaborative

---

## Relationship to Other Principles

This principle depends on:
- **Default Secure, Default Operable**
- **Least Privilege at Runtime**

It enables:
- **Guardrails over Approvals**
- **Progressive Hardening**

A clear runtime contract is how platforms scale governance **without friction**.