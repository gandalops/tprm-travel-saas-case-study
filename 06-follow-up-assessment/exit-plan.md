# Exit plan: Vendor X travel platform

> **Fictional case study.** Example Bank and Vendor X are placeholders. All vendor replies, evidence, dates and scores are simulated. Legal references are indicative and must be checked against the official texts.
>
> **Builds on:** the follow-up assessment (REM-15, FND-15, RR-11, CR-06, CR-25). **Owner:** Bank TPRM. **Position at:** 4 Dec 2026.

## 1. Why the bank needs this plan

Vendor X supports a critical or important function. If the vendor fails, is sold, or has to be removed, the bank cannot improvise. DORA expects an exit strategy for such services (Art 28(8)) and a termination right with a transition period (Art 28(7) and Art 30(3)(f)). This plan is the bank's side of that strategy. It lists what the bank does, who does it, and what evidence proves it is done.

The plan covers only what the bank controls. What the vendor must still agree or deliver is listed in section 8 as open topics.

## 2. Two kinds of exit

| Type | When | Pace |
|---|---|---|
| **Planned exit** | Contract end, a decision to change vendor, a failed reassessment | Weeks to months, with a transition period |
| **Stressed exit** | Insolvency, serious breach, regulator instruction, a security incident that cannot be contained | Days. Access is cut first, the move comes after |

## 3. Triggers

| ID | Trigger | Type | Who decides |
|---|---|---|---|
| EX-01 | Vendor insolvency or loss of the ability to deliver the service | Stressed | Business owner, TPRM, Legal |
| EX-02 | Material breach of contract or of a security commitment | Stressed or planned | Risk committee |
| EX-03 | Instruction from the bank's supervisor or a competent authority | Stressed | Compliance |
| EX-04 | A High finding still open at the extended date (the escalation rule in the decision memo) | Planned | Risk committee |
| EX-05 | Change of control of the vendor that raises sanctions, ownership or concentration concerns | Planned | TPRM, Compliance |
| EX-06 | Repeated service level breaches or loss of a key certification (ISO 27001, SOC 2) | Planned | Business owner, TPRM |
| EX-07 | A security incident at the vendor that exposes the bank's data and is not contained | Stressed | IT security, Risk committee |

## 4. Alternatives

| Option | Use | Limit |
|---|---|---|
| **Alternative vendor** | Planned exit. Keep a shortlist from the original selection, refreshed yearly | Needs a new assessment, so it cannot replace a stressed exit in days |
| **Temporary manual process** | Stressed exit. Booking by phone agent and direct booking, as in the bank's fallback plan (BA-12) | Does not cover emergency assistance abroad or virtual-card payments. These need a separate interim arrangement with the group insurer and the bank's card arrangements |
| **Bring in-house** | Not realistic for this service | Listed so the committee sees it was considered |

## 5. Exit steps

Owners are teams, not people. Evidence is what Bank TPRM keeps in the exit file.

| ID | Step | Owner | Evidence |
|---|---|---|---|
| EX-10 | **Disable the connector.** Run the kill-switch runbook (BA-06): disable the service accounts for the HR system, HR portal, expense or payroll system and ERP, and revoke the vendor's tokens | IT security, IAM | Account status export, timestamp |
| EX-11 | **Close the inbound openings.** Remove the firewall rules for the vendor's fixed source addresses (the four openings into the bank: FA, F3 and F6, F11, F7) | Network team | Rule change record |
| EX-12 | **Remove single sign-on.** Delete the vendor application in the bank's identity provider and disable any local or break-glass vendor accounts | IAM | IdP configuration export |
| EX-13 | **Stop the invoice path.** Block the intake endpoint (F7) and the remittance path (F8). Hold unpaid invoices for reconciliation | Finance | Endpoint status, invoice list |
| EX-14 | **Inform the insurer.** Tell the group insurer that trip registration through the vendor has ended and agree how new trips are registered | HR benefits and insurance | Written confirmation |
| EX-15 | **Settle virtual cards.** Stop issuing, let open single-use cards expire or settle at month-end, reconcile with Card Provider Y | Finance | Reconciliation report |
| EX-16 | **Secure the executive and traveller position.** List trips in progress and upcoming trips, protect executive itineraries, give travellers abroad a contact for help | Corporate security, HR | Trip list, contact notice |
| EX-20 | **Take the data back.** Export bookings, invoices, allowance records, audit logs and the rate table in an agreed format | Business owner, IT operations | Export file with checksum |
| EX-21 | **Delete at the vendor.** Require deletion of all bank data, including backups and fourth-party copies, with a deletion certificate | DPO, TPRM | Deletion certificate, region confirmation |
| EX-22 | **Check the deletion.** DPO reviews the certificate against the vendor's data inventory and region diagram | DPO | Review note |
| EX-30 | **Update the register of information** and the criticality record (BA-07) | Compliance | Register entry |
| EX-31 | **Inform the supervisor** where the exit is of a critical or important function and notification is required. Compliance confirms | Compliance | Notification record |
| EX-32 | **Close the contract and the invoices.** Final invoice, release of any held payments, contract closure | Procurement, Finance | Closure letter |
| EX-33 | **Lessons learned.** Review what worked, update this plan and the shortlist | TPRM | Review note |

**Timing rules (proposed assumptions, to be fixed in the contract):**

- Access revocation (EX-10 to EX-12) within 24 hours of the exit decision, in line with REM-15.
- Data export (EX-20) within 30 days of the request. Deletion with certificate (EX-21) within 30 days after the export is accepted.
- Transition period for a planned exit: 6 months.

## 6. Roles

| Team | Role in an exit |
|---|---|
| Business owner (HR) | Decides the fallback, owns the data export acceptance |
| TPRM | Runs the plan, keeps the exit file |
| IT security and IAM | Cut access, check accounts |
| Network team | Close the firewall openings |
| IT operations | Receive the export, run the interim process |
| Finance | Invoices, cards, payments |
| DPO | Data return and deletion |
| Compliance | Register of information and supervisor notification |
| Legal and Procurement | Contract rights, notice, closure |
| Business continuity | Fallback and interim arrangements |
| Corporate security | Travellers abroad and executive itineraries |
| Risk committee | Decides on stressed exits and on unresolved High findings |

## 7. Exit test

The exit test is due by 30 Jun 2027 and is part of REM-15. A test proves the plan works before it is needed.

| Part | What is tested | Pass when |
|---|---|---|
| Connector disable drill | The kill-switch runbook (EX-10) is run on a test connector | All accounts disabled within the agreed time, logged |
| Access removal | EX-11 and EX-12 are performed in a test setting | Rules and IdP entries removed and verified |
| Data export | A sample export is requested from the vendor | File received in the agreed format, checksum matches |
| Tabletop | Teams walk through a stressed exit (EX-01) | Every owner confirms their steps and gaps are logged |

## 8. Open topics (depend on the vendor)

| Topic | Why it is open | Linked to |
|---|---|---|
| Signed insolvency and data-return clause | Agreed in the redline, not signed (EV-45) | REM-15, FND-15 |
| Length of the transition period and the data export format | Proposed by the bank, not yet agreed | CR-25 |
| Deletion certificate and proof that the US backups are gone | The vendor committed to delete by 15 Dec 2026. Evidence pending (EV-47) | REM-23, FND-23 |
| Vendor's cooperation in the exit test | Needs a contract commitment | REM-15 |
| Residual risk RR-11 | Stays High until the exit clauses are signed and the test is passed | RR-11 |

## 9. Maintenance

Bank TPRM reviews this plan once a year with the reassessment, and after any trigger such as a change of ownership, a new fourth party or a new module. Changes to the firewall rules, the connector or the identity setup update steps EX-10 to EX-12.
