## Anomaly Grid — Platform Architecture

### The Elevator Pitch

_"What if you could offer any business their own red pill? Anomaly Grid is a multi-tenant AI-powered threat detection platform built on NVIDIA Morpheus. Companies plug into the Grid, and the Grid shows them what's really happening on their network."_

### The Matrix Theming (Woven Into the Architecture)

Every major component gets a Matrix-inspired codename that also describes its function:

- **The Oracle** — the agentic AI layer that predicts threats before they materialize
- **The Architect** — the admin control plane where you manage tenants, RBAC, and platform config
- **Nebuchadnezzar (Neb)** — the Morpheus compute engine, the ship that carries the crew through the Matrix
- **Zion** — the secure tenant portal where subscribing companies access their dashboards
- **The Construct** — the honeypot environment, a simulated reality designed to trap threats
- **Sentinel Swarm** — the digital fingerprinting collectors deployed across tenant networks
- **The Red Pill** — the onboarding process for new tenant companies joining the Grid


---

## Anomaly Grid — Platform Architecture

### The Elevator Pitch

_"What if you could offer any business their own red pill? Anomaly Grid is a multi-tenant AI-powered threat detection platform built on NVIDIA Morpheus. Companies plug into the Grid, and the Grid shows them what's really happening on their network."_

---

### The Matrix Theming (Woven Into the Architecture)

Every major component gets a Matrix-inspired codename that also describes its function:

- **The Oracle** — the agentic AI layer that predicts threats before they materialize
- **The Architect** — the admin control plane where you manage tenants, RBAC, and platform config
- **Nebuchadnezzar (Neb)** — the Morpheus compute engine, the ship that carries the crew through the Matrix
- **Zion** — the secure tenant portal where subscribing companies access their dashboards
- **The Construct** — the honeypot environment, a simulated reality designed to trap threats
- **Sentinel Swarm** — the digital fingerprinting collectors deployed across tenant networks
- **The Red Pill** — the onboarding process for new tenant companies joining the Grid

---

### Multi-Tenant Architecture

This is the big shift from a personal lab to a commercial platform. Each subscribing company is a **tenant** on the Grid.

```
┌──────────────────────────────────────────────────────────────────┐
│                     ANOMALY GRID PLATFORM                        │
│                                                                  │
│  ┌────────────────────────────────────────────────────────────┐  │
│  │              THE ARCHITECT (Control Plane)                 │  │
│  │  ┌──────────────┐ ┌──────────────┐ ┌───────────────────┐  │  │
│  │  │ Tenant Mgmt  │ │ RBAC Engine  │ │ Billing / Usage   │  │  │
│  │  │ (Onboarding) │ │ (Entra ID)   │ │ Metering          │  │  │
│  │  │ "Red Pill"   │ │              │ │                   │  │  │
│  │  └──────────────┘ └──────────────┘ └───────────────────┘  │  │
│  └────────────────────────────────────────────────────────────┘  │
│                                                                  │
│  ┌────────────────────────────────────────────────────────────┐  │
│  │           NEBUCHADNEZZAR (Morpheus Compute Engine)         │  │
│  │                                                            │  │
│  │   ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌─────────┐    │  │
│  │   │Tenant A │  │Tenant B │  │Tenant C │  │Tenant D │    │  │
│  │   │Pipeline │  │Pipeline │  │Pipeline │  │Pipeline │    │  │
│  │   └────┬────┘  └────┬────┘  └────┬────┘  └────┬────┘    │  │
│  │        │             │            │             │          │  │
│  │        └─────────────┴─────┬──────┴─────────────┘          │  │
│  │                            │                               │  │
│  │                   ┌────────▼────────┐                      │  │
│  │                   │ Triton Inference│                      │  │
│  │                   │ Server (Shared) │                      │  │
│  │                   └─────────────────┘                      │  │
│  └────────────────────────────────────────────────────────────┘  │
│                                                                  │
│  ┌──────────────┐  ┌──────────────────┐  ┌─────────────────┐   │
│  │THE CONSTRUCT │  │ SENTINEL SWARM   │  │   THE ORACLE    │   │
│  │(Honeypots)   │  │ (Digital         │  │   (Agentic AI)  │   │
│  │              │  │  Fingerprinting) │  │                 │   │
│  │ Per-tenant   │  │ Lightweight      │  │ Predicts,       │   │
│  │ isolated     │  │ agents deployed  │  │ responds,       │   │
│  │ instances    │  │ on tenant        │  │ investigates    │   │
│  │              │  │ networks         │  │                 │   │
│  └──────────────┘  └──────────────────┘  └─────────────────┘   │
│                                                                  │
│  ┌────────────────────────────────────────────────────────────┐  │
│  │                ZION (Tenant Portal)                        │  │
│  │  ┌──────────┐ ┌──────────┐ ┌────────────┐ ┌───────────┐  │  │
│  │  │Dashboard │ │Threat    │ │Incident    │ │API Access │  │  │
│  │  │& Reports │ │Feed      │ │Response    │ │& Webhooks │  │  │
│  │  └──────────┘ └──────────┘ └────────────┘ └───────────┘  │  │
│  └────────────────────────────────────────────────────────────┘  │
└──────────────────────────────────────────────────────────────────┘
```

---

### Tenant Isolation Model

This is critical for a multi-tenant platform. Each company's data has to be completely isolated.

**Data Isolation** — Every tenant gets their own partition in Cosmos DB or their own Azure Blob Storage container. Morpheus pipelines are tagged with a `tenant_id` so data never crosses boundaries. Think of it like apartments in a building — shared infrastructure, completely separate living spaces.

**Compute Isolation** — Morpheus pipelines run per-tenant on the shared GPU cluster, but with resource quotas. Tenant A's spike in traffic can't starve Tenant B's anomaly detection. Azure Kubernetes Service (AKS) with NVIDIA GPU operator handles this orchestration, using namespaces per tenant.

**Network Isolation** — Each tenant's Construct (honeypot) runs in its own VNet. Sentinel Swarm agents deployed on tenant networks send data through encrypted tunnels (WireGuard or Azure VPN Gateway) back to Nebuchadnezzar.

---

### RBAC Structure (Per Tenant)

The Architect manages a layered permission model:

**Platform-Level Roles (your team):**

- **Grid Admin** — full platform control, tenant provisioning, infrastructure management
- **Grid Operator** — monitors platform health, manages Morpheus pipelines, no billing access
- **Grid Support** — can view tenant dashboards to troubleshoot, no config changes

**Tenant-Level Roles (the subscribing company's team):**

- **Tenant Admin** — manages their company's users, configures alert thresholds, views all data
- **Security Analyst** — views dashboards, investigates alerts, interacts with The Oracle
- **External Auditor** — read-only access to compliance reports and historical threat data, time-limited via PIM

**External Collaborator Roles (outside the tenant company):**

- **Consultant** — scoped access to specific datasets, can submit investigation queries to The Oracle, no infrastructure visibility
- **Red Team Partner** — can interact with The Construct (honeypot) for authorized pen testing, sandboxed from production data

All of this runs through Entra ID with B2B for external users, Conditional Access enforcing MFA and location policies, and PIM for just-in-time elevation.

---

### The Oracle — Agentic AI Detail

The Oracle operates as a multi-agent system with three specialized agents per tenant:

**Prediction Agent** — continuously analyzes Morpheus output, identifies emerging patterns, and generates threat forecasts. "Based on fingerprinting data from the last 72 hours, there's a 78% probability of credential stuffing attacks targeting your authentication endpoints."

**Response Agent** — when anomaly scores breach thresholds, this agent takes automated actions within guardrails: isolates compromised honeypot instances, updates Sentinel Swarm fingerprint rules, creates incident tickets, and notifies the tenant's Security Analyst through Zion.

**Investigation Agent** — the conversational interface. A tenant analyst opens Zion and asks: "Show me everything related to the suspicious TLS fingerprint from last night." The agent queries across Morpheus results, honeypot logs, and fingerprint databases, then returns a correlated timeline.

---

### Subscription Tiers

Since this is a business, you'd structure it like:

**Red Pill (Entry)** — Single Morpheus pipeline, shared Construct honeypot, basic Sentinel Swarm fingerprinting, Zion dashboard access, Oracle in read-only mode (insights but no automated response)

**Operator (Mid)** — Dedicated Morpheus pipeline, dedicated Construct instance, full Sentinel Swarm deployment, Oracle with automated response, API access and webhooks, 5 tenant user seats

**The One (Enterprise)** — Everything in Operator plus custom anomaly models trained on the tenant's data, dedicated GPU allocation, red team Construct access, unlimited seats, SLA guarantees, direct Grid Support channel

---

### How External Collaboration Works

Say a managed security service provider (MSSP) wants to collaborate with one of your tenant companies:

1. Tenant Admin sends a B2B invite through Zion
2. MSSP analyst gets a "Red Pill" onboarding email
3. They authenticate through their own identity provider via Entra External ID
4. Conditional Access checks MFA, device compliance, location
5. They land in Zion with the **Consultant** role — scoped to only the datasets the Tenant Admin approved
6. They can query The Oracle, view dashboards, export reports
7. Their access automatically expires after the engagement window (PIM time-bound)

The entire collaboration happens without the MSSP ever touching your infrastructure directly.
---

## Related Notes
- [[SOC Fundamentals]]
- [[Introduction to SIEM]]
- [[Splunk Basics]]
- [[Intro to Logs]]
