# Section 8 — Power Platform Components

The components selected here flow from the requirements in Section 5, the roles in Section 3, and the data model in Section 7. Each component is chosen because a specific part of the solution needs it — not because the platform offers it.

---

## Component Map

| Layer | Component | Used By |
|---|---|---|
| Data | Microsoft Dataverse | Foundation for all tables and relationships |
| Application (End Users) | Canvas App | End Users |
| Application (IT Team) | Model-Driven App | Service Desk Analysts, Specialist Technicians, IT Support Manager, IT Service Owner, System Administrator |
| Automation | Power Automate (cloud flows) | Triggered by ticket events; affects all roles |
| Analytics (Operational) | Dataverse charts and dashboards | Service Desk Analysts, Specialist Technicians, IT Support Manager |
| Analytics (Strategic) | Power BI | IT Service Owner, CIO, IT Support Manager |
| Communication | Office 365 Outlook + Microsoft Teams connectors | All roles, via notifications |
| Identity | Microsoft Entra ID | All authenticated users |

---

## Microsoft Dataverse — The Data Foundation

Every entity in Section 7 lives in Dataverse: Ticket, Category, SLA, Ticket Comment, Location, Affected Service, plus the built-in User and Team tables.

**Why Dataverse and not SharePoint or Excel.** The solution needs proper relational data with self-referencing relationships (Category hierarchy), role-based security at table, row, and column level, immutable audit logging, server-side calculations (Priority, SLA due dates), and scalability to enterprise volumes. SharePoint lists fall over on the relational integrity and audit requirements. Excel is not a system of record.

**Requirements served:** FR-01 to FR-50 (every functional requirement requires a data platform), NFR-01 (security), NFR-02 (encryption), NFR-06 (search performance), NFR-07 (scalability), NFR-09 (auditability).

---

## Canvas App — For End Users

A Canvas App is the simplest, most controllable interface for the largest user population. End Users (500–2,000 employees) need a focused experience: submit a ticket, view their tickets, comment on them, reopen if needed. They don't need queues, dashboards, or admin controls.

**What it provides:**
- Submit New Ticket form
- My Tickets list
- Ticket detail view with comment thread
- Mobile and desktop access

**Used by:** End Users (Role 1).

**Why Canvas and not Model-Driven for this audience.** Model-driven apps surface too much data by default. End users would be overwhelmed. Canvas allows pixel-level control, branding, and a streamlined experience tailored to a single task: logging a ticket.

**Requirements served:** FR-01 (multi-channel submission — web portal channel), FR-02 (mandatory classification), FR-05 (attachments), FR-06 (location capture), FR-10 / FR-11 (urgency and impact selection with definitions), FR-26 (reopen), FR-40 (self-service view), NFR-08 (usability and accessibility on desktop and mobile).

---

## Model-Driven App — For the IT Team

A Model-Driven App is generated from the Dataverse schema and is built for data-dense, productivity-focused work. The IT team lives inside the system all day; they need grids, filters, advanced search, dashboards, and bulk operations.

**What it provides:**
- Ticket queues by team and assignment
- Ticket form with full lifecycle controls
- Personal and operational dashboards
- Advanced Find and saved views
- Business Process Flow guiding the ticket lifecycle (New → Assigned → In Progress → Resolved → Closed)

**Used by:** Service Desk Analysts (L1), Specialist Technicians (L2/L3), IT Support Manager, IT Service Owner, System Administrator (Roles 2–6).

**Why Model-Driven for this audience.** The IT team's productivity depends on getting through volume. Model-driven gives the grid views, filters, and bulk actions for free from the data schema. Building this in Canvas would mean reinventing those features by hand.

**Requirements served:** FR-03 (auto-numbering), FR-13 (priority override action — manager-only ribbon control), FR-15 (manual and bulk assignment), FR-17 (escalation actions), FR-19 (visibility restrictions), FR-20 / FR-21 (lifecycle and transitions — via Business Process Flow), FR-22 (status logging), FR-23 / FR-24 (resolution and root cause), FR-30 (Major Incident declaration), FR-31 (comment types), FR-37 / FR-38 (operational dashboards), FR-41 (saved views).

---

## Power Automate — The Automation Engine

Automated work that humans shouldn't have to remember. Cloud flows trigger on ticket events and on a schedule.

**Flows in scope:**

| Flow | Trigger | Purpose |
|---|---|---|
| Ticket Auto-Assignment | On ticket creation | Apply routing rules; assign to matching queue |
| Email-to-Ticket | Email arrives in IT mailbox | Create ticket from email, preserving sender, subject, body, attachments |
| SLA Monitoring | Scheduled (every few minutes) | Detect SLA breaches; flag tickets; notify Manager and Service Owner |
| Requester Notifications | On lifecycle events | Notify requester at submission, assignment, On Hold, resolution, closure, customer-update comments |
| Agent Notifications | On assignment | Notify agent via email and Teams |
| Auto-Closure | Scheduled (daily) | Send pre-closure warnings; close eligible Resolved tickets |
| Major Incident Broadcast | On Major Incident declaration | Broadcast to configured distribution list |
| User Provisioning Sync | Scheduled + event-driven | Sync user changes from Entra ID; revoke access for leavers; reassign tickets of departed agents |

**Used by:** Power Automate runs in the background; affects every role through the notifications and actions it produces.

**Requirements served:** FR-01 (email channel), FR-14 (initial assignment), FR-18 (hierarchical SLA escalation), FR-25 (auto-closure), FR-27 (requester notifications), FR-28 (agent notifications), FR-29 (manager SLA alerts), FR-30 (major incident broadcast), FR-35 (SLA breach flagging), FR-49 (user provisioning).

---

## Dataverse Dashboards — Operational Reporting

Dashboards embedded inside the Model-Driven App, surfaced to each role. Built natively from Dataverse views and charts.

**Used by:** Service Desk Analysts and Specialist Technicians (personal dashboards), IT Support Manager (operational dashboard).

**Why Dataverse dashboards instead of Power BI for this layer.** They live inside the app the agents already use, refresh in near-real-time, and require no separate licensing for the operational team.

**Requirements served:** FR-37 (personal workload dashboard), FR-38 (operational dashboard for manager).

---

## Power BI — Strategic Reporting

For trend analysis, cross-period comparison, and executive reporting. Power BI connects directly to Dataverse, so the data is always fresh.

**What it provides:**
- 12-month trends in ticket volume, MTTA, MTTR, SLA compliance
- Top categories and affected services
- Root cause distribution for resolved P1 / P2 incidents
- Major Incident frequency over time
- Comparative period analysis

**Used by:** IT Service Owner, CIO, Executive Leadership, IT Support Manager (for cross-team analysis).

**Why Power BI and not Dataverse dashboards for this layer.** Strategic reports need historical depth, comparative analysis, and presentation polish that the embedded dashboards aren't designed for.

**Requirements served:** FR-36 (SLA compliance reporting), FR-39 (strategic dashboard), FR-42 (report export).

---

## Office 365 Outlook + Microsoft Teams — Communication

Notifications sent through these connectors from Power Automate flows.

- **Email (Outlook connector):** universal channel for requester confirmations, agent assignments, manager alerts, and Major Incident broadcasts.
- **Teams notifications:** in-platform notifications for agents and managers, where Teams is part of the user's workflow.

**Used by:** Recipients vary by event. Requesters get email. Agents get email and Teams. Managers get email, Teams, and the daily breach digest.

**Requirements served:** FR-27 (requester notifications), FR-28 (agent notifications via email and Teams), FR-29 (manager alerts), FR-30 (major incident broadcast).

---

## Microsoft Entra ID — Identity and Access

The organisational identity provider used for authentication. The system maintains no separate credential store.

**What it provides:**
- Single sign-on for all users
- Multi-factor authentication enforcement (especially for administrative roles)
- Conditional access policies honoured automatically
- User profile attributes available for auto-provisioning

**Used by:** Every authenticated user — End Users, IT team, Manager, Service Owner, System Administrator.

**Requirements served:** FR-47 (identity integration), FR-49 (user provisioning), NFR-01 (authentication and authorisation), NFR-03 (privacy via documented lawful basis and access policies).

---

## Security and Environments — Configuration Layer

Not separate components, but configuration that spans everything above:

- **Six Dataverse Security Roles** mirroring the six roles in Section 3, each granted the minimum permissions needed.
- **Three environments** — Development, Test/UAT, Production — to support proper Application Lifecycle Management.
- **Solution packaging** — all tables, apps, flows, and security roles bundled into a Dataverse solution for versioned deployment between environments.

**Requirements served:** FR-19 (visibility restriction), FR-44 (audit trail visibility and protection), FR-48 (role-based access control), NFR-04 (availability), NFR-12 (disaster recovery), NFR-13 (auditable configuration).

---

## Out of Scope for Phase 1

Two Power Platform capabilities are deliberately deferred:

- **Power Pages** — for external users without Microsoft 365 licences. Not needed in Phase 1; all users are internal employees.
- **AI Builder and Copilot Studio** — for category prediction, root cause suggestions, and chatbot self-service. Both require historical ticket data to be effective. Phase 2 candidates once 3–6 months of operational data exist.

---

## Component Summary

| Component | Role |
|---|---|
| Dataverse | Stores everything; enforces relationships and security |
| Canvas App | End Users submit and track tickets |
| Model-Driven App | IT team works tickets; manager oversees the operation |
| Power Automate | Automates routing, notifications, SLA monitoring, closure, broadcasts |
| Dataverse Dashboards | Operational reporting embedded in the IT team's workspace |
| Power BI | Strategic reporting for leadership |
| Outlook + Teams connectors | Notification channels |
| Entra ID | Authentication and provisioning |
| Security Roles + Environments | Access control and lifecycle management |

Every component traces to specific requirements. Nothing is included for breadth alone.

---

⬅️ **Previous:** [Section 7 — Entity Relationship Diagram](../07-Entity-Relationship-Diagram)
🏠 **Back to Project Overview:** [Main README](../README.md)
