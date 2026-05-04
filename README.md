# IT Support Ticketing System — TechCare Solutions

Phase 1 design and specification for an ITIL-aligned IT Support Ticketing System, produced as part of the **Platform Explorers Cohort 2 — Power Platform track (Week 2-3)**.

---

## The Problem

TechCare Solutions, a fictional mid-to-large regulated enterprise, receives 200+ IT support requests weekly through email and phone. There is no centralised system, which leads to missed SLAs, duplicated work, frustrated staff, no audit trail, and no data for service improvement.

Each of these is a symptom of a missing Service Desk function — the foundation of any mature IT operation in ITIL terms.

---

## The Approach

I worked through the design in seven sections, each one feeding into the next:

| # | Section | Focus |
|---|---|---|
| 1 | [Use Case and Domain](./01-Use-Case-and-Domain) | What the system is and the ITIL framing |
| 2 | [Business Scenario](./02-Business-Scenario) | TechCare's pain points and the gaps behind them |
| 3 | [Roles in the Solution](./03-Roles-in-the-Solution) | Six roles aligned to ITIL functions |
| 4 | [Key Stakeholders](./04-Key-Stakeholders) | Internal, governance, and external stakeholders |
| 5 | [Business Requirements](./05-Business-Requirements) | 50 functional + 14 non-functional requirements |
| 6 | [Acceptance Criteria](./06-Acceptance-Criteria) | Acceptance criteria covering every requirement |
| 7 | [Entity Relationship Diagram](./07-Entity-Relationship-Diagram) | The data model and relationships |

---

## Key Design Choices

**ITIL 4 as the framing.** The design is built around ITIL 4 practices — Incident Management and Service Request Management for Phase 1.

**Priority is calculated, not selected.** Users choose Urgency and Impact; the system derives Priority via the ITIL matrix. This avoids the common pattern of every ticket being marked "Critical."

**Three-level category hierarchy.** Category supports Level 1 → Level 2 → Level 3 through a self-referencing table.

**Root Cause for high-priority incidents.** Mandatory for P1 and P2; optional for P3 and P4. Builds the dataset for Phase 2 Problem Management.

**Audit trail and separation of duties.** Reflecting the regulated context — the audit log is immutable and not editable by System Administrators.

**Phase 1 scope.** Problem Management, Change Management, CMDB, Service Catalog, and AI triage are explicitly deferred to Phase 2.

---

## Repository Structure

```
IT-Support-Ticketing-System-TechCare/
│
├── README.md
├── LICENSE
│
├── 01-Use-Case-and-Domain/
├── 02-Business-Scenario/
├── 03-Roles-in-the-Solution/
├── 04-Key-Stakeholders/
├── 05-Business-Requirements/
├── 06-Acceptance-Criteria/
└── 07-Entity-Relationship-Diagram/
```

---

## Project Context

| | |
|---|---|
| **Programme** | Platform Explorers Cohort 2 |
| **Track** | Power Platform |
| **Use Case** | IT Support Ticket System (Week 2-3) |
| **Author** | [Martins Osahon Osimen](https://github.com/martosah) |
| **Phase** | Phase 1 — Design and Specification |

---

## Acknowledgements

Thanks to the Platform Explorers programme and the cohort coaches — Juan Ojochemi Idowu, Mathew Ede, Rachel Irabor, Sarah Anueyiagu, Church Ephraim, Thomas Okuya, and Adewale Yusuf.

---

## License

MIT License — see [LICENSE](./LICENSE).
