# Runtime Detection (Detective Guardrails)

Runtime detection guardrails observe **live system behavior** to surface
risk, drift, and policy violations that cannot be fully prevented ahead of time.

They do not block execution.
They **create awareness and trigger response**.

---

## What Runtime Detection Is

Runtime detection:
- Observes workloads *after they are running*
- Detects unsafe, unexpected, or drifting behavior
- Produces signals for humans or automation

Detection answers:
- “What is happening right now?”
- “Is this within expected bounds?”
- “Has something changed that we should care about?”

---

## What Runtime Detection Is Not

Runtime detection is not:
- Admission control
- CI/CD enforcement
- Manual audits
- Alerting on every metric

Detection without intent creates noise.

---

## Common Runtime Detection Categories

### 1. Configuration Drift

Examples:
- Resource limits removed post-deploy
- Labels or annotations changed manually
- Policy exceptions lingering past expiry

Why it matters:
- Drift erodes trust in declarative systems
- Drift often precedes incidents

---

### 2. Behavioral Risk

Examples:
- Unexpected network communication
- Privilege escalation attempts
- Abnormal restart patterns
- Unusual API usage

Why it matters:
- Some risks only appear at runtime
- Behavior reveals intent more than config

---

### 3. Platform Safety Signals

Examples:
- Node pressure patterns
- Pod eviction frequency
- Scheduler backoffs
- Quota exhaustion trends

Why it matters:
- These indicate systemic stress
- Teams usually cannot see these signals themselves

---

## Enforcement Philosophy

Runtime detection should:
- Prefer **signals over alerts**
- Emphasize **trends over spikes**
- Correlate context before escalation

Not every violation is an incident.
Not every incident requires blocking.

---

## Detection → Response Flow

Detection guardrails typically feed:
- Human review
- Automated remediation
- Policy refinement
- Investment decisions

Detection without a response path is wasted effort.

---

## Platform vs Team Responsibilities

**Platform owns:**
- Signal definitions
- Noise reduction
- Cross-namespace visibility

**Teams own:**
- Understanding impact
- Fixing underlying causes
- Improving workload behavior

---

## CI/CD vs Runtime Boundary

CI/CD answers:
- “Is this change allowed?”

Runtime detection answers:
- “Is this change behaving as expected?”

Both are required for safe autonomy.

---

## Interview / Review Talk Track

> “Runtime detection lets us see reality, not just intent.  
> CI/CD tells us what should happen. Runtime signals tell us what actually did.”

---

## What This Document Avoids (Intentionally)

- Tool choices
- Metrics lists
- Alert thresholds
- Vendor dashboards

Those belong in **implementation examples**, not in the core pattern.