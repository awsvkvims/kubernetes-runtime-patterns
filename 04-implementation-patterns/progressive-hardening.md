# Progressive Hardening

Progressive hardening is the practice of **introducing guardrails gradually**,
increasing enforcement only as confidence, coverage, and trust grow.

It ensures guardrails:
- reduce risk without stopping delivery
- build adoption instead of resistance
- scale across teams and environments safely

---

## Why Progressive Hardening Matters

Most guardrail failures are not technical —
they are **change management failures**.

Common failure modes:
- enforcing too early
- enforcing without visibility
- enforcing without escape hatches
- enforcing without explaining intent

Progressive hardening avoids these by aligning
**enforcement strength with organizational maturity**.

---

## The Hardening Spectrum

Guardrails typically progress through three stages:

### 1. Observe

- Guardrail logic exists
- Violations are detected and surfaced
- No blocking occurs

Purpose:
- Build visibility
- Establish baselines
- Educate teams

Example:
- Detect missing resource limits
- Report insecure configurations
- Surface drift signals

---

### 2. Warn

- Violations generate visible warnings
- Pipelines or systems continue
- Teams are expected to respond

Purpose:
- Shift behavior without stopping flow
- Validate rules before enforcing
- Create shared understanding

Example:
- Warning on privileged pods
- Warning on missing probes
- Warning on policy violations

---

### 3. Enforce

- Violations block or auto-correct
- Unsafe states are prevented
- System protects itself

Purpose:
- Eliminate known failure modes
- Scale safety automatically
- Remove reliance on human review

Example:
- Block unsafe admissions
- Enforce quotas
- Auto-isolate risky workloads

---

## Environment-Based Progression

Hardening often progresses **by environment**:

- Development
  - Observe → Warn
- Staging
  - Warn → Enforce
- Production
  - Enforce by default

This allows:
- learning without impact
- safe iteration on policies
- confidence before production enforcement

---

## Capability-Based Progression

Hardening may also vary by **guardrail type**:

- Identity and isolation guardrails harden early
- Resource and reliability guardrails harden after usage data
- Corrective guardrails harden last

Not all guardrails move at the same speed.

---

## What Progressive Hardening Is Not

- Not a one-time migration
- Not a blanket toggle
- Not a maturity scorecard

Hardening decisions are **intentional, contextual, and reversible**.

---

## Relationship to Other Patterns

Progressive hardening influences:

- Admission Control
- Pod Security Standards
- Resource Baselines
- Network Policies
- Runtime Remediation

Each pattern should clearly state:
- what it observes
- when it warns
- when it enforces

---

## Key Principle

> **Guardrails earn the right to enforce by first proving they are correct.**

Trust is built by visibility first,
then guidance,
then enforcement.