# Default Secure, Default Operable

This principle states that **the safest configuration should also be the easiest one to use**.

Security and operability must not compete.
If teams must choose between “working” and “secure,” the system has already failed.

---

## Core Principle

> **Security should be the default, not a tax.  
> Operability should be preserved, not negotiated.**

Teams should not need:
- Special knowledge
- Exception requests
- Custom workarounds

to run workloads safely.

---

## Why Defaults Matter More Than Policies

Most runtime risk is introduced:
- By omission, not malice
- By copy-paste, not intent
- By time pressure, not ignorance

When secure behavior requires *extra effort*, it will be skipped.

Therefore:
> **Defaults determine outcomes far more than documentation or training.**

---

## What “Default Secure” Means

Out of the box:
- Namespaces are isolated
- Network traffic is denied unless allowed
- Service accounts are scoped
- Privileged execution is blocked
- Resource limits are enforced

Teams get safety **without asking for it**.

---

## What “Default Operable” Means

Defaults must also:
- Allow applications to start
- Support common workload patterns
- Fail fast with clear feedback
- Be easy to override *through explicit, visible mechanisms*

Security that breaks workflows creates shadow systems.

---

## Operability Is Not an Exception Path

Operability does **not** mean:
- Blanket exemptions
- Permanent relaxations
- Turning off guardrails

It means:
- Progressive enforcement
- Context-aware constraints
- Clear escalation paths with visibility

---

## How This Shows Up in the Platform

This principle drives:
- Secure base Helm charts
- Namespace templates with sane defaults
- Admission policies that start in warn mode
- Gradual tightening over time

See:
- `04-implementation-patterns/resource-baselines.md`
- `04-implementation-patterns/pod-security-standards.md`
- `04-implementation-patterns/progressive-hardening.md`

---

## Common Failure Mode This Prevents

Without this principle:
- Teams bypass guardrails
- Exceptions become permanent
- Platform trust erodes
- Security becomes performative

With it:
- Teams stay inside the system
- Guardrails become invisible
- Safety improves organically

---

## Relationship to Other Principles

This principle reinforces:
- **Least Privilege at Runtime** — safe does not mean unusable
- **Guardrails over Approvals** — defaults replace manual review
- **Platform Runtime Contract** — predictable behavior across environments

Default secure + default operable is how platforms scale trust **without slowing delivery**.