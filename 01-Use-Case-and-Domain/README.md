# Section 1 — Use Case and Domain

## What I'm Designing

I'm designing an **IT Support Ticketing System** for TechCare Solutions, a fictional mid-to-large regulated enterprise. In ITSM vocabulary, this is the **Service Desk** — the system that captures every IT-related issue or request, tracks it through resolution, and produces the operational data leadership needs to manage and improve the service.

I framed the design around **ITIL 4**, the international standard for IT Service Management. ITIL is the working vocabulary of mature IT operations, and aligning to it makes the design defensible against industry practice rather than something invented from scratch.

---

## Incident vs. Service Request

ITIL distinguishes two types of work the Service Desk handles, and the distinction shapes the entire design:

| | Incident | Service Request |
|---|---|---|
| Definition | An unplanned interruption to a service | A pre-defined user request |
| Example | "Email is down" | "Please grant me access to the finance drive" |
| Trigger | Something broke | Someone needs something |
| Workflow | Diagnose → restore service | Approve (where needed) → fulfil |

Both types are tickets in the system, but they follow different lifecycles, carry different SLAs, and produce different reports. My design supports both.

---

## TechCare in ITIL Terms

TechCare currently has IT staff who do support work, but no Service Desk function. They have no formal SLAs, no centralised intake, no audit trail, and no service data. The system I'm designing gives them the operational foundation that's missing — a single source of truth for IT demand, with the discipline a regulated organisation needs.

---

## Phase 1 Scope

**In scope:**
- Incident Management
- Service Request Management
- SLA management with Urgency × Impact priority calculation
- Multi-level service categorisation
- Resolution and root cause capture
- Role-based access control
- Reporting and dashboards
- Audit trail

**Out of scope (deferred to Phase 2):**
- Formal Problem Management (linking incidents to problem records)
- Change Management
- Configuration Management Database (CMDB)
- Service Catalog with approval workflows
- AI-driven triage and chatbot self-service
- Knowledge Base with publishing workflow

The Phase 1 work establishes the foundation; Phase 2 layers on the maturity once there's operational data to drive it.

---

➡️ **Next:** [Section 2 — Business Scenario](../02-Business-Scenario)
