# Corrective Patterns (Automated Runtime Guardrails)

Corrective guardrails **act on detected risk** to restore or preserve system safety
without waiting for human intervention.

They reduce blast radius.
They restore invariants.
They protect availability.

---

## What Corrective Guardrails Are

Corrective guardrails:
- Trigger in response to runtime signals
- Take **bounded, automated action**
- Operate within predefined policy constraints

They answer:
- “What should the system do when something goes wrong?”
- “How do we limit impact before humans intervene?”

---

## What Corrective Guardrails Are Not

Corrective guardrails are not:
- Punitive actions
- Auto-fixing application bugs
- Replacing incident response
- Making irreversible decisions

Automation should be **conservative and reversible**.

---

## Common Corrective Patterns

### 1. Quarantine & Isolation

Examples:
- Move workload to restricted namespace
- Apply tighter network policies
- Revoke elevated permissions

Use when:
- Risk is uncertain
- Investigation is needed
- Safety is more important than availability

---

### 2. Automated Rollback or Restart

Examples:
- Restart unhealthy pods
- Roll back to last known-good ReplicaSet
- Disable feature flags automatically

Use when:
- Failure modes are well understood
- Recovery is safe and fast
- Rollback is reversible

---

### 3. Throttling & Circuit Breaking

Examples:
- Scale down misbehaving workloads
- Apply rate limits dynamically
- Shed load from unstable services

Use when:
- System-wide stability is at risk
- Partial degradation is acceptable
- Protecting the platform is critical

---

### 4. Policy Escalation

Examples:
- Convert warnings into enforcement
- Block future similar changes
- Require stronger guardrails next deploy

Use when:
- Repeated violations occur
- Signals show systemic risk
- Learning needs to be codified

---

## Control Boundaries

Corrective guardrails should:
- Act within **predefined limits**
- Prefer isolation over deletion
- Always emit signals explaining actions taken

Human override must always be possible.

---

## Platform vs Team Responsibilities

**Platform owns:**
- Automation logic
- Safety bounds
- Reversibility guarantees

**Teams own:**
- Root cause analysis
- Fixing application behavior
- Improving future guardrails

---

## Detection → Correction Flow

Detection without correction is noise.
Correction without detection is dangerous.

Well-designed systems:
- Detect early
- Correct narrowly
- Escalate deliberately

---

## CI/CD vs Runtime Boundary

CI/CD prevents known risks.
Runtime correction handles emergent behavior.

Both are required for resilient systems.

---

## Interview / Review Talk Track

> “Corrective guardrails let the system protect itself first —  
> humans step in to improve the system, not to stop the bleeding.”

---

## What This Document Avoids (Intentionally)

- Tool-specific implementations
- Controllers or operator code
- Alert thresholds
- Vendor-specific remediation engines

Those belong in **example implementations**, not in the core pattern.