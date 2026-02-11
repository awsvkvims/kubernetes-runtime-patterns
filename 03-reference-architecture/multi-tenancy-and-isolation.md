# Multi-Tenancy & Isolation

## Multi-Tenant Cluster Isolation Boundaries

**Purpose:**  
Show how a shared Kubernetes cluster can safely host multiple teams by making **tenancy boundaries explicit**.

This diagram answers:
- “What is the tenant boundary in Kubernetes?”
- “What is isolated per team vs shared cluster-wide?”
- “Where do namespaces, RBAC, NetworkPolicy, quotas, and Pod Security fit together?”

**How to read:**  
- **Namespace** is the *primary* tenancy boundary for workloads  
- **RBAC** controls who can do what (API permissions)  
- **NetworkPolicy** controls who can talk to whom (network permissions)  
- **Quotas/LimitRanges** prevent noisy-neighbor resource exhaustion  
- **Pod Security** prevents risky runtime configurations  
- Some controls are **cluster-scoped** (platform-owned), some **namespace-scoped** (team-owned with constraints)

```mermaid
flowchart TB
  subgraph Cluster["Cluster (Shared) — Platform-Owned"]
    APIServer["API Server"]
    Admission["Admission / Policy Enforcement<br/>(cluster-scoped)"]
    Obs["Observability Stack<br/>(cluster-scoped)"]
    Nodes["Nodes / Runtime"]
  end

  subgraph TeamA["Team A Namespace (Tenant Boundary)"]
    A_RBAC["RBAC RoleBindings<br/>(who can change what)"]
    A_NP["NetworkPolicy<br/>(who can talk to whom)"]
    A_Quota["ResourceQuota + LimitRange<br/>(noisy-neighbor control)"]
    A_PSS["Pod Security (baseline/restricted)<br/>(risky spec prevention)"]
    A_Work["Workloads (Pods/Services)"]
  end

  subgraph TeamB["Team B Namespace (Tenant Boundary)"]
    B_RBAC["RBAC RoleBindings"]
    B_NP["NetworkPolicy"]
    B_Quota["ResourceQuota + LimitRange"]
    B_PSS["Pod Security (baseline/restricted)"]
    B_Work["Workloads (Pods/Services)"]
  end

  %% Change path
  TeamA -->|kubectl/apply| APIServer
  TeamB -->|kubectl/apply| APIServer
  APIServer --> Admission --> APIServer

  %% Runtime placement
  APIServer --> Nodes
  Nodes --> A_Work
  Nodes --> B_Work

  %% Isolation layers applied “around” the workloads
  A_RBAC --> A_Work
  A_NP --> A_Work
  A_Quota --> A_Work
  A_PSS --> A_Work

  B_RBAC --> B_Work
  B_NP --> B_Work
  B_Quota --> B_Work
  B_PSS --> B_Work

  %% Shared systems observe everything
  A_Work --> Obs
  B_Work --> Obs
```

## Key Points From The Diagram

### 1) Namespace is the tenancy boundary (not the node)
Multiple teams can share nodes safely if their workload boundaries are enforced at the API and runtime layers.

### 2) Isolation is layered (not a single control)
A safe multi-tenant setup relies on multiple controls working together:

- **RBAC** prevents unauthorized API actions (e.g., Team A can’t edit Team B’s objects)
- **NetworkPolicy** prevents unwanted network access (e.g., deny-all by default, allow explicit)
- **ResourceQuota + LimitRange** prevents resource starvation and runaway usage
- **Pod Security** prevents risky container runtime capabilities and unsafe specs
- **Admission / Policy Enforcement** ensures the cluster never accepts disallowed configurations

### 3) Cluster-scoped vs Namespace-scoped (ownership clarity)
- **Cluster-scoped controls** are platform-owned because they protect *everyone*:
  - Admission/policy enforcement
  - Default-deny baselines
  - Global observability and audit
- **Namespace-scoped controls** can be team-managed within guardrails:
  - Fine-grained RBAC bindings
  - Allow-list NetworkPolicies for dependencies
  - Namespace quotas aligned to team capacity

## Cross-links to Add (or verify)
- Implementation patterns:
  - RBAC: `../04-implementation-patterns/namespaces-and-rbac.md`
  - Network policies: `../04-implementation-patterns/network-policies.md`
  - Resource baselines: `../04-implementation-patterns/resource-baselines.md`
  - Pod Security: `../04-implementation-patterns/pod-security-standards.md`
- Starter assets (defaults you can apply immediately):
  - `../05-starter-assets/manifests/namespace.yaml`
  - `../05-starter-assets/manifests/default-networkpolicy-deny.yaml`
  - `../05-starter-assets/manifests/resourcequota.yaml`
  - `../05-starter-assets/manifests/limitrange.yaml`


> “In Kubernetes, tenancy isn’t one feature — it’s a layered boundary: namespace + RBAC + network policy + resource limits + pod security, enforced at admission and validated by signals.”

## Multi-tenancy & Isolation Architecture

**Why this exists (1 line):** The “Isolation Boundaries” diagram shows *where* isolation exists; this section shows *how* isolation is enforced, owned, and evolved over time.

This diagram explains:
- **Ownership:** what the platform owns vs what teams own
- **Enforcement surfaces:** where isolation is actually enforced (admission, runtime, network, quotas)
- **Evolution:** how controls harden from dev → prod without adding human gates

> See also: **Isolation Boundaries** (static containment model) in this same document.

### Multi-tenancy & Isolation Architecture (ownership + enforcement)

```mermaid
flowchart TB
  %% Legend:
  %% Solid arrows = enforcement path / control
  %% Dotted arrows = feedback / visibility

  subgraph PLATFORM["Platform-owned control plane & shared services"]
    APISERVER["Kubernetes API Server"]
    ADMISSION["Admission Control<br/>(policies, validation)"]
    POLICY["Policy Engine<br/>(constraints as code)"]
    IDP["Identity Provider + RBAC Model<br/>(groups/roles)"]
    OBS["Observability Plane<br/>(logs/metrics/traces/events)"]
    RESP["Response Automation<br/>(alerts, runbooks, remediation controllers)"]
  end

  subgraph TENANT["Tenant isolation surface (per team / per namespace)"]
    NS["Namespace Boundary"]
    RBAC["RBAC Roles & Bindings<br/>(least privilege)"]
    NET["NetworkPolicy Boundary<br/>(default deny + allowlists)"]
    QUOTA["ResourceQuota + LimitRange<br/>(fair-share + safety)"]
    PSS["Pod Security Baseline<br/>(workload safety defaults)"]
    WL["Workloads (Deployments/Pods)"]
  end

  subgraph CHANGE["Change entering the cluster"]
    CI["Delivery System (CI/CD)<br/>(deploy request)"]
    REQ["API Request<br/>(apply/patch)"]
  end

  subgraph FEEDBACK["Signals & governance feedback"]
    SIG["Policy Violations / Drift / Risk Signals"]
    REV["Decision Forum<br/>(team / enablement / leadership)"]
    HARDEN["Progressive Hardening<br/>(warn → block → auto-correct)"]
  end

  CI --> REQ --> APISERVER --> ADMISSION --> POLICY
  POLICY -->|allow/deny/transform| APISERVER

  APISERVER --> NS --> WL
  NS --> RBAC
  NS --> NET
  NS --> QUOTA
  NS --> PSS

  %% Runtime visibility and response
  WL -.-> OBS
  POLICY -.-> OBS
  NET -.-> OBS
  QUOTA -.-> OBS

  OBS -.-> SIG --> REV --> HARDEN --> POLICY
  SIG -.-> RESP
  RESP -->|remediate / isolate / rollback| WL
```

### How to Read This Diagram

- **Platform-owned** components (top-left) define the “rules of the road” and enforcement points.
- **Tenant isolation surface** (middle) is where teams live: namespaces and their guardrails.
- **Change flow** (left) shows how deployments enter and are evaluated.
- **Feedback loop** (bottom-right) shows how signals lead to better policies over time.

This is an **architecture diagram**, not a tool diagram:
- No vendor choices
- No YAML
- No single “right” product
- Focus is on **responsibility boundaries** and **enforcement surfaces**

---

## What This Diagram Adds Beyond “Isolation Boundaries”

The Isolation Boundaries view answers:  
> “How far can a failure or misconfiguration spread?”

This Architecture view answers:  
> “How do we *consistently enforce* those boundaries without human gates?”

Specifically, it adds:
- **Ownership clarity** (platform vs teams)
- **Where enforcement happens** (admission, policy engine, runtime controls)
- **How enforcement evolves** (progressive hardening)
- **How exceptions are handled** (signals → decision forum → policy changes)

---

## Practical Interpretation (What Each Role Does)

### Platform / Runtime Team
Owns:
- Admission policies and enforcement level strategy
- RBAC group model and tenant onboarding patterns
- Baseline NetworkPolicy, quotas, and pod security baselines
- Observability + response automation integration

### Engineering Teams
Own:
- Namespace-level configuration within constraints
- Service-to-service allowlists required for their workloads
- Remediation of violations surfaced by signals
- Evidence and exception requests (when needed)

### Security / Risk / Compliance
Own:
- Control objectives and acceptable risk posture
- Required policy categories (e.g., isolation, least privilege)
- Audit expectations (e.g., exceptions, enforcement levels, evidence)

---

## Links to Related Sections

- **Runtime Guardrail Categories:** `../../02-runtime-model/runtime-guardrail-categories.md`
- **Enforcement Levels:** `../../02-runtime-model/enforcement-levels.md`
- **Admission Control Patterns:** `../../04-implementation-patterns/admission-control.md`
- **Network Policies:** `../../04-implementation-patterns/network-policies.md`
- **Namespaces & RBAC:** `../../04-implementation-patterns/namespaces-and-rbac.md`
- **Progressive Hardening:** `../../04-implementation-patterns/progressive-hardening.md`
