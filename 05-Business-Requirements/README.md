
# Section 5 — Business Requirements

The system must satisfy 50 functional requirements and 14 non-functional requirements. Each one is written in "shall" language and traced to its stakeholder need and ITIL alignment.

The functional requirements are organised into nine groups that follow the Incident Management and Service Request Management lifecycles, plus supporting capabilities.

---

## Functional Requirements

### Group A — Ticket Intake and Capture

**FR-01 — Multi-Channel Ticket Submission.** The system shall allow tickets to be submitted through a web-based self-service portal, email-to-ticket conversion, and manual entry by Service Desk Analysts on behalf of users contacting them by phone or in person.

*Trace: End Users / Service Desk — single point of contact.*

**FR-02 — Mandatory Ticket Classification at Submission.** The system shall capture the following at submission: Requester, Ticket Type (Incident or Service Request), Title, Description, Category (with sub-category and third-level category as applicable), Urgency, and Impact.

*Trace: Service Desk / Manager — proper logging and classification.*

**FR-03 — Automated Ticket Reference Generation.** The system shall generate a unique, immutable reference for each ticket, formatted `INC-YYYY-NNNNNN` for Incidents and `SR-YYYY-NNNNNN` for Service Requests.

*Trace: All operational roles — unique incident records.*

**FR-04 — Submission Timestamp Capture.** The system shall capture the date and time of submission automatically, with no possibility of user override.

*Trace: Manager / Compliance — accurate chronology and audit baseline.*

**FR-05 — Attachment Support.** The system shall allow requesters and agents to attach supporting files to tickets, subject to file type and size restrictions.

*Trace: All operational roles — efficient information capture.*

**FR-06 — Branch / Location Capture.** The system shall capture the requester's branch or location at submission, defaulted from profile but editable.

*Trace: Manager / Department Heads — multi-site visibility and reporting.*

**FR-07 — Affected Service Capture.** The system shall capture the IT service affected by the ticket where applicable, selected from a configured service list.

*Trace: Service Owner / Manager — service-level visibility.*

---

### Group B — Categorisation and Prioritisation

**FR-08 — Hierarchical Multi-Level Categorisation.** The system shall support a three-level hierarchical category structure (Category → Sub-Category → Third-Level Category).

*Trace: Service Desk / Manager / Service Owner — proper classification at enterprise depth.*

**FR-09 — Configurable Category Library.** The System Administrator shall be able to add, edit, deactivate, and re-order categories at all three levels without developer intervention.

*Trace: Sys Admin / Manager — adaptable taxonomy.*

**FR-10 — Urgency Selection.** The system shall require selection of an Urgency value from a controlled list (Critical, High, Medium, Low) with definitions visible to the user.

*Trace: End Users / Service Desk — input to priority calculation.*

**FR-11 — Impact Selection.** The system shall require selection of an Impact value from a controlled list (Whole Organisation, Entire Department/Affiliate, Whole Branch/Office, Only Me) with definitions visible.

*Trace: End Users / Service Desk — input to priority calculation.*

**FR-12 — Calculated Priority via ITIL Matrix.** The system shall calculate Priority automatically from Urgency and Impact using the ITIL matrix, and shall not permit users to set Priority directly:

| | Only Me | Whole Branch | Entire Dept | Whole Org |
|---|---|---|---|---|
| **Low Urgency** | P4 | P4 | P3 | P3 |
| **Medium Urgency** | P4 | P3 | P3 | P2 |
| **High Urgency** | P3 | P3 | P2 | P1 |
| **Critical Urgency** | P3 | P2 | P1 | P1 |

*Trace: Manager / Service Owner / All operational — formal priority calculation.*

**FR-13 — Manager Priority Override with Audit.** The IT Support Manager shall be able to override the calculated Priority with a recorded reason, captured in the audit trail.

*Trace: Manager / Compliance — controlled exception handling.*

---

### Group C — Assignment, Routing, and Escalation

**FR-14 — Initial Assignment.** The system shall route every newly submitted ticket to the appropriate Level 1 queue based on its category, using configurable routing rules.

*Trace: Manager / Service Desk — efficient assignment.*

**FR-15 — Manual Assignment by Manager.** The IT Support Manager shall be able to assign or reassign tickets to specific agents, individually or in bulk, across queues and tiers.

*Trace: Manager — workload balancing.*

**FR-16 — Self-Assignment by Agents.** Service Desk Analysts and Specialist Technicians shall be able to claim unassigned tickets from their queue.

*Trace: Service Desk / Specialists — agent autonomy.*

**FR-17 — Tier Escalation (L1 → L2 → L3).** The system shall allow escalation between support tiers, with a mandatory escalation reason captured.

*Trace: Service Desk / Specialists / Manager — formal escalation paths.*

**FR-18 — Hierarchical Escalation on SLA Breach.** The system shall notify the IT Support Manager on SLA breach and escalate to the IT Service Owner if the breach extends beyond a configurable threshold.

*Trace: Manager / Service Owner — proactive breach management.*

**FR-19 — Restriction of Visibility by Assignment.** Service Desk Analysts and Specialist Technicians shall see only tickets in their assigned queues or assigned to them, while the IT Support Manager retains full visibility.

*Trace: All operational / Compliance / InfoSec — least privilege.*

---

### Group D — Ticket Lifecycle and Status Management

**FR-20 — Defined Status Lifecycle.** The system shall enforce the following status lifecycle: New → Assigned → In Progress → On Hold (with sub-states: Awaiting User, Awaiting Vendor, Awaiting Parts, Awaiting Approval) → Resolved → Closed → Reopened.

*Trace: All operational — process discipline.*

**FR-21 — Status Transition Rules.** The system shall enforce permitted status transitions and prevent invalid transitions through the UI and any API.

*Trace: Manager / Compliance — process integrity.*

**FR-22 — Status Change Logging.** The system shall record every status change with timestamp, actor, previous status, and new status, in an immutable log.

*Trace: Compliance / Auditors / InfoSec — forensic traceability.*

**FR-23 — Resolution Notes Mandatory.** The system shall require resolution notes before a ticket's status can change to Resolved.

*Trace: Service Desk / Specialists / Manager — knowledge capture.*

**FR-24 — Root Cause Capture for P1 and P2.** The system shall require Root Cause to be captured before resolution for Priority 1 and Priority 2 tickets, optional for P3 and P4.

*Trace: Specialists / Manager / Service Owner — feeds Phase 2 Problem Management.*

**FR-25 — Auto-Closure of Resolved Tickets.** The system shall automatically close tickets that remain in Resolved status without requester response after a configurable period, with prior notification to the requester.

*Trace: Service Desk / Manager — operational efficiency.*

**FR-26 — Ticket Reopen Capability.** The system shall allow a closed ticket to be reopened within a configurable period after closure.

*Trace: End Users / Service Desk — customer focus.*

---

### Group E — Communication and Notifications

**FR-27 — Requester Notifications on Lifecycle Events.** The system shall notify the requester at submission, assignment, status change to On Hold, resolution, closure, and any agent-authored Customer Update comment.

*Trace: End Users — visibility and communication.*

**FR-28 — Agent Notifications on Assignment.** The system shall notify an agent when a ticket is assigned to them.

*Trace: Service Desk / Specialists — fast acknowledgement.*

**FR-29 — Manager SLA Breach Alerts.** The system shall notify the IT Support Manager when a ticket approaches and when it exceeds its SLA Resolution time.

*Trace: Manager — proactive SLA management.*

**FR-30 — Major Incident Broadcast.** The IT Support Manager shall be able to flag a ticket as a Major Incident, triggering a broadcast notification to a configurable distribution list.

*Trace: Manager / Service Owner / Executive Leadership — coordinated major incident response.*

**FR-31 — Internal vs Customer-Facing Comments.** The system shall distinguish between Internal Notes (visible only to agents and managers) and Customer Updates (visible to the requester).

*Trace: Service Desk / Specialists / End Users — information hygiene.*

---

### Group F — Service Level Agreement Management

**FR-32 — Configurable SLA Framework.** The system shall maintain a configurable SLA framework defining Response Time and Resolution Time for each Priority level.

*Trace: Service Owner / Manager / Sys Admin — Service Level Management.*

**FR-33 — SLA Calculation at Ticket Creation.** The system shall calculate and store Response and Resolution SLA Due Dates at ticket creation, based on Priority and the assigned support team's business hours.

*Trace: All operational — fair and visible SLA from the start.*

**FR-34 — SLA Pause for Customer-Side Wait.** The system shall pause the Resolution SLA timer when a ticket's status is "On Hold — Awaiting User" and resume when the status changes to an active state.

*Trace: Manager / Service Desk — fair measurement.*

**FR-35 — SLA Breach Flagging.** The system shall flag a ticket as SLA-breached when its Response or Resolution SLA Due Date passes without the corresponding event.

*Trace: Manager / Service Desk — visibility for management action.*

**FR-36 — SLA Compliance Reporting.** The system shall report SLA compliance broken down by team, agent, category, priority, and time period.

*Trace: Manager / Service Owner / CIO — Continual Improvement.*

---

### Group G — Reporting, Dashboards, and Analytics

**FR-37 — Personal Workload Dashboard for Agents.** The system shall provide each agent with a dashboard showing assigned tickets, tickets approaching SLA, recently closed tickets, and personal performance metrics.

*Trace: Service Desk / Specialists — self-management.*

**FR-38 — Operational Dashboard for Manager.** The system shall provide the IT Support Manager with a dashboard showing total open tickets, by status, by priority, SLA compliance, by agent, by category, and tickets approaching or breaching SLA.

*Trace: Manager — operational situational awareness.*

**FR-39 — Strategic Dashboard for IT Service Owner / CIO.** The system shall provide a strategic dashboard showing trends over time in volume, MTTA, MTTR, SLA compliance, top categories, top affected services, and root cause patterns for P1 and P2 incidents.

*Trace: Service Owner / CIO / Executive Leadership — Continual Improvement at strategic level.*

**FR-40 — End User Self-Service View.** The system shall provide each end user with a view of their own tickets — open, closed, and historical — with status, last update, and resolution notes.

*Trace: End Users — visibility and self-service.*

**FR-41 — Configurable Filtering and Saved Views.** The system shall allow operational users to filter ticket lists and save commonly used filter combinations as named views.

*Trace: Service Desk / Specialists / Manager — productivity tooling.*

**FR-42 — Report Export.** The system shall allow operational and strategic users to export reports and ticket lists for offline analysis and audit submission.

*Trace: Manager / Service Owner / Auditors / Compliance — external analysis and audit response.*

---

### Group H — Audit, History, and Compliance

**FR-43 — Complete Audit Trail.** The system shall maintain an immutable audit trail of every change to every ticket, capturing field changed, previous value, new value, user, timestamp, and source.

*Trace: Compliance / Auditors / Regulators / InfoSec — regulatory and audit requirement.*

**FR-44 — Audit Trail Visibility.** The system shall make the audit trail viewable by Manager, Compliance Officer, and Internal Auditor, and shall not allow any user — including System Administrators — to modify or delete audit records.

*Trace: Compliance / Auditors / InfoSec — audit integrity.*

**FR-45 — Configuration Change Logging.** The system shall log all configuration changes — categories, SLA policies, security roles, routing rules — including who, when, what, and the previous value.

*Trace: Sys Admin / Auditors / Compliance — change accountability.*

**FR-46 — Data Retention Enforcement.** The system shall retain ticket records and audit trails for a minimum of 7 years (or longer if required by applicable regulation).

*Trace: Compliance / Regulators / Auditors — records management.*

---

### Group I — User and Service Management

**FR-47 — Integration with Organisational Identity.** The system shall use TechCare's organisational identity directory for authentication and shall not maintain a separate user credential store.

*Trace: InfoSec / End Users / Sys Admin — Access Management.*

**FR-48 — Role-Based Access Control.** The system shall enforce role-based access control aligned to the six roles in Section 3, with each role granted only the permissions necessary to perform its function.

*Trace: InfoSec / Compliance / All users — Information Security Management.*

**FR-49 — User Provisioning and Deprovisioning.** The system shall reflect changes in user status from the organisational directory and shall revoke access promptly for departed users.

*Trace: InfoSec / HR / Compliance — Access Management.*

**FR-50 — Out-of-Office Coverage.** The system shall allow agents to designate a covering colleague when out of office, with their assigned tickets visible to and actionable by the cover agent.

*Trace: Service Desk / Specialists / Manager — continuity of service.*

---

## Non-Functional Requirements

**NFR-01 — Authentication and Authorisation.** The system shall enforce multi-factor authentication for administrative roles and shall integrate with the organisation's central identity provider.

*Trace: InfoSec / Compliance.*

**NFR-02 — Data Protection in Transit and at Rest.** The system shall encrypt all data in transit and at rest using industry-standard encryption.

*Trace: InfoSec / Compliance / Regulators.*

**NFR-03 — Privacy and Data Protection.** The system shall comply with applicable data protection regulations, including support for data subject access requests and right to erasure within legal limits.

*Trace: Compliance / DPO / Regulators.*

**NFR-04 — Availability.** The system shall maintain high availability during business hours, with planned maintenance scheduled outside business hours where possible.

*Trace: All operational / Service Owner.*

**NFR-05 — Page Response Performance.** Operational pages shall load within an acceptable time under normal load conditions.

*Trace: All operational.*

**NFR-06 — Search and Filter Performance.** The system shall return search and filter results within an acceptable time under normal load.

*Trace: Service Desk / Specialists / Manager.*

**NFR-07 — Scalability.** The system shall accommodate sustained ticket volumes consistent with TechCare's scale, with capacity to scale as the organisation grows, without architectural redesign.

*Trace: Service Owner / Sys Admin.*

**NFR-08 — Usability and Accessibility.** The system shall provide a usable interface on desktop and mobile devices and shall meet recognised accessibility standards.

*Trace: End Users / Service Desk / Specialists.*

**NFR-09 — Auditability.** The system shall maintain auditable records for the full retention period and shall produce complete audit reports on demand.

*Trace: Compliance / Auditors / Regulators.*

**NFR-10 — Maintainability.** The System Administrator shall be able to perform configuration changes — categories, SLAs, routing rules, security roles — without developer intervention or system downtime.

*Trace: Sys Admin / Manager.*

**NFR-11 — Localisation and Time Zones.** The system shall display timestamps in the user's local time zone while storing all data in a single canonical time zone.

*Trace: End Users / Service Desk.*

**NFR-12 — Disaster Recovery.** The system shall meet defined Recovery Time and Recovery Point Objectives in the event of a major disruption.

*Trace: Service Owner / InfoSec / Regulators.*

**NFR-13 — Auditable Configuration.** The system shall version-control all configuration changes and support rollback to a prior configuration.

*Trace: Sys Admin / Auditors.*

**NFR-14 — Vendor and Platform Independence.** The system shall, where commercially reasonable, store data in formats and structures that support future export and migration.

*Trace: Service Owner / Finance / CIO.*

---

## Summary

| Category | Count |
|---|---|
| Functional Requirements | 50 |
| Non-Functional Requirements | 14 |
| **Total** | **64** |

---

➡️ **Next:** [Section 6 — Acceptance Criteria](../06-Acceptance-Criteria)
⬅️ **Previous:** [Section 4 — Key Stakeholders](../04-Key-Stakeholders)
