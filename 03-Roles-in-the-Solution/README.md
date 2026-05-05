
# Section 3 — Roles in the Solution

The solution supports six roles. Each one represents a distinct function inside the system, with its own scope of access and responsibility. Where a role corresponds to an ITIL-defined function, I noted the alignment.

---

## Role 1 — End User

The largest user population — TechCare employees who submit tickets when they have an IT issue or request.

**In the system:** submits new tickets, views their own tickets, adds comments, confirms or reopens resolutions.
**Cannot:** view other users' tickets, set Priority directly, edit ticket fields after submission, see internal agent notes.
**ITIL alignment:** *User of the IT service.*

---

## Role 2 — Service Desk Analyst (L1)

Frontline IT staff who receive every incoming ticket, perform triage, and resolve the majority of routine issues.

**In the system:** views their queue, claims and resolves tickets, applies known fixes, escalates to L2 when needed, communicates with end users.
**Cannot:** reassign across teams, override priority, modify SLAs.
**ITIL alignment:** *Service Desk Analyst.*

---

## Role 3 — Specialist Technician (L2/L3)

Senior IT staff with domain expertise — network, applications, security, infrastructure. Handle escalations from L1.

**In the system:** takes ownership of escalated tickets, adds technical investigation notes, documents Root Cause for high-priority incidents, resolves and closes.
**Cannot:** modify SLA configurations, reassign to other specialist teams without manager approval.
**ITIL alignment:** *Specialist Technical Support (Tier 2/3).*

---

## Role 4 — IT Support Manager

Supervises the operation. Combines team management with Incident Management process ownership.

**In the system:** views all tickets across the organisation, reassigns and rebalances workload, overrides priority where justified (with audit), declares Major Incidents, monitors SLA compliance, generates reports.
**Cannot:** modify the underlying SLA framework or category structure (that's the System Administrator).
**ITIL alignment:** *Incident Manager combined with Service Desk Manager.*

---

## Role 5 — IT Service Owner

Senior IT leadership — IT Director, CIO, Head of IT Operations. Strategic visibility, not operational ticket work.

**In the system:** accesses executive dashboards (volume, MTTA, MTTR, SLA compliance, trends), drills down to specific tickets when needed, approves major changes to SLA framework or categories.
**Cannot:** edit ticket data, reassign tickets, configure system settings.
**ITIL alignment:** *Service Owner.*

---

## Role 6 — System Administrator

Technical custodian of the platform. Configures and maintains the system itself.

**In the system:** maintains categories, SLAs, routing rules, security roles, and notification templates. Manages user provisioning and integrations.
**Cannot:** view or edit ticket content (separation of duties), modify audit logs.
**ITIL alignment:** *Process Owner combined with Tooling Administrator.*

---

## Roles Summary

| # | Role | ITIL Function | Primary Activity | Population |
|---|---|---|---|---|
| 1 | End User | User of the service | Submits and tracks own tickets | 500–2,000 |
| 2 | Service Desk Analyst | L1 Service Desk | Triage and first-call resolution | 4–8 |
| 3 | Specialist Technician | L2/L3 Specialist | Investigates and resolves escalations | 4–10 |
| 4 | IT Support Manager | Incident Manager + SD Manager | Oversight, escalation, reporting | 1–2 |
| 5 | IT Service Owner | Service Owner | Strategic visibility | 1–3 |
| 6 | System Administrator | Process Owner + Tooling Admin | Configuration and maintenance | 1–2 |

---

➡️ **Next:** [Section 4 — Key Stakeholders](../04-Key-Stakeholders)
⬅️ **Previous:** [Section 2 — Business Scenario](../02-Business-Scenario)
