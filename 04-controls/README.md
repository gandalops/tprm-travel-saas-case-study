# Stage 4: Control requirements and questionnaire

> **Fictional case study.** Example Bank and Vendor X are placeholders. Legal and standard references are indicative and must be checked against the official texts. 
>
> **Builds on:** Stages 1 to 3 (scope and data, vendor claims and fourth parties, flows and observations X1 to X12).

## 1. Purpose and method

Turn what we learned in Stages 1 to 3 into **control requirements**, then map each requirement to the frameworks and to questions the vendor must answer. The order matters: **controls come from risks, and the frameworks come second.**

The chain used throughout:

**Flow or observation, then risk, then control requirement, then framework reference, then question, then vendor answer, finding and decision (Stage 5).**

Worked example:

| Link | Content |
|---|---|
| Flow | FA: the vendor-operated connector pulls the employee roster from the HR system every night |
| Observation | X2: the connector holds credentials for several bank systems in one place |
| Risk | A stolen credential allows bulk reading of employee data |
| Control requirement | CR-03: credentials are held in a vault, readable only by named roles, with access logged |
| Frameworks | DORA Art 9, GDPR Art 32, ISO 27001 A.5.17 and A.8.24 |
| Questions | E3, O3 (vendor-questionnaire-and-control-map.xlsx, Questionnaire sheet, column A) |
| Vendor answer and finding | Stage 5 |

## 2. Inputs

| Stage | What it provides | IDs used |
|---|---|---|
| 1 | Scope, data types, inherent risk, Tier 1, regulations | S1 to S12, D1 to D16, F1 to F9, R1 to R10, A1 to A11 |
| 2 | Vendor claims and fourth parties | V1 to V13, FP1 to FP10, A12 |
| 3 | Flows, boundaries, exposures | FS, FA, F1 to F12, FG, FN, FL, FH, FV, FW1 to FW3, X1 to X12, A13 to A16 |

## 3. Control requirements (28)

| ID | Control requirement | Risk addressed | Derived from | Questions |
|---|---|---|---|---|
| CR-01 | **Network.** The vendor connects to the bank only from a fixed, documented set of source addresses, announced before any change, and the bank allows only those. | An unauthorised party reaches the bank's HR, expense or finance endpoints | X1; FA, F3, F6, F11, F7 | H1, O1 |
| CR-02 | **Connection authentication.** Every connection from the vendor into the bank uses mutual TLS or equivalent strong client authentication, with short-lived tokens. | A stolen or replayed credential works from anywhere | X1; V7 | H2, H3, O2 |
| CR-03 | **Credential storage.** Credentials the bank gives the vendor (HR, HR portal, expense and ERP accounts) are held in a vault, never in plain text, readable only by named roles, with access logged. | Compromise of one place exposes four bank systems | X2; V7 | E3, O3 |
| CR-04 | **Credential rotation.** Credentials are rotated at least every 90 days and after staff or incident triggers, and the bank can revoke them immediately. (90 days is a proposed default.) | A leaked credential stays valid for months | X2; V7 | O4 |
| CR-05 | **Connector isolation.** The connector is a dedicated instance for the bank, patched and monitored, with read-only access and only the agreed fields. | Over-broad access allows bulk reading of employee data | X1, X2; FA, F3 | E1, O5, O6 |
| CR-06 | **Connector exit.** At contract end the connector is shut down, credentials are revoked and deleted, and the bank receives evidence. | Residual access after the relationship ends | X2; Tier 1 | M3, O7 |
| CR-07 | **SSO and MFA.** Users sign in only through the bank IdP with MFA. Local passwords are disabled, including for admins, except vaulted break-glass accounts. | Account takeover or unmanaged accounts | X4; FS, FG, F10 | B1, B2, B3, B4 |
| CR-08 | **Joiners, movers, leavers.** Accounts follow the HR record: leavers lose access within an agreed time, movers get new roles, seats are reclaimed and access is reviewed. | Former employees keep access to travel data and booking rights | FA; FS | C1, C2, C3, C4, C5 |
| CR-09 | **Privileged and support access.** Vendor admin and support access to production data is just-in-time, approved, logged and restricted by region. | Misuse or compromise of support accounts exposes passport and executive data | X5; V8; FV | D1, D2, D4 |
| CR-10 | **VIP protection.** Executive and VIP itineraries have restricted visibility and masked trip purposes, including for vendor staff. | Leak of senior management movements | Stage 1 F5; S2 | D5 |
| CR-11 | **Invoice and finance integrity.** Invoices are authenticated and tamper-evident, duplicates and alterations are detected, and changes of bank details are verified with the bank. | A fraudulent or altered invoice reaches the ERP | X3; F7, F8 | G1, G2, G3, G4, G5 |
| CR-12 | **Data minimisation and lifecycle.** Only required fields are sent, retention periods are set and deletion is evidenced, test environments hold no real data, and guest data is deleted after the trip. | Over-collection and long retention of passport and personal data | X10; V10; D2, D3, D10 | A2, E1, I3, I4, I5, I7 |
| CR-13 | **Encryption.** Data is encrypted in transit (TLS 1.2 or higher) and at rest, with defined key management and a customer-managed key option where available. | Data exposed if storage or traffic is intercepted | V11 | H2, I1 |
| CR-14 | **Cross-border transfers and regional rules.** Every country that can access or receive personal data is listed with a transfer mechanism, regional residency needs are met, and local regulator requests can be supported. | Unlawful transfer or breach of local data laws | X5, X6; V6; R9 | I2, T1, T2, T3 |
| CR-15 | **Logging and monitoring.** Security events are logged immutably, exportable to the bank's SIEM, free of personal and card data and monitored for anomalies. Failed syncs raise alerts. | Incidents go undetected, or logs leak personal data | X6; FL | E4, I6, J1, J2, J3 |
| CR-16 | **Fourth-party transparency.** The vendor lists each fourth party, the data it receives and its role, gives advance notice of changes with a right to object, and ensures deletion after use. | Data spreads to suppliers the bank cannot see or control | X7, X12; V9; FP1 to FP10 | K1, K2, K3, K4, K5 |
| CR-17 | **Insurer hand-off.** Data sent to the group insurer is accurate and minimal, health information is protected, and a failed interface is detected. | Wrong or excessive data reaches the insurer, or there is no cover during a trip | X8; F9 | U1, U2, U3 |
| CR-18 | **Allowance integrity.** Only authorised Finance roles change the rate table, changes are approved and logged, and calculation errors are detected before payment. | Wrong or fraudulent allowance payments | X9; F10, F11 | D3, Q1, Q2 |
| CR-19 | **Gifts and loyalty.** Gift orders follow value limits and recipient rules with an audit trail. Loyalty data and discount codes are protected from misuse. | Improper gifts and loyalty fraud | S9, S11; F5d | Q3, Q4, Q5 |
| CR-20 | **Virtual cards.** Card numbers are held only where PCI DSS applies and is attested, cards are single-use with limits, and transactions are reconciled. | Card misuse or card data exposure | X11; V3; F12 | P1, P2, P3, P4 |
| CR-21 | **Guest booking control.** Only authorised bookers create guest bookings with sponsor approval, and guest data is minimal and short-lived. | Unauthorised bookings and uncontrolled guest data | X10; S5; FG | F4, I7 |
| CR-22 | **Approval integrity.** Approval messages are authenticated and cannot be forged or replayed, policy rules are version-controlled, and requesters cannot approve their own trips. | Unapproved trips or spend | F3, F6 | F1, F2, F3 |
| CR-23 | **Assurance evidence.** The vendor provides current independent assurance that covers all modules and sites: SOC 2 with a bridge letter, ISO 27001 scope, penetration test and PCI attestation. | Reliance on claims or outdated reports | V1 to V4 | L1, L2, L3 |
| CR-24 | **Resilience and incident support.** Recovery targets are met and tested, incidents are notified to the bank within an agreed time, and the vendor assists at no extra cost or a set cost. | A long outage or a late breach notice | V5; Tier 1 | M1, M2, N4 |
| CR-25 | **Contract terms.** The contract contains the DORA Art 30(2) terms and, because the service is Tier 1, the Art 30(3) terms, including audit rights and exit. | No legal basis to enforce the controls | R1; Tier 1 | N1, N2, N3, N4, N5, N6, N7 |
| CR-26 | **Tenant isolation.** Customer tenants are logically separated, tested and prevented from accessing each other's data. | One client sees another client's data | V12; F4 | I8 |
| CR-27 | **Architecture transparency.** The vendor documents its edition, interfaces and data flows, keeps them current, and tells the bank about changes. | The bank assesses a picture that no longer matches reality | Stage 3; all flows | A1, A3, E2 |
| CR-28 | **AI and automation.** AI features and model providers are disclosed, bank data is not used for model training unless agreed, and automated actions stay under human control. | Bank data leaks into models, or automated actions go unchecked | AI note; V13 | W1, W2, W3 |

## 4. Framework mapping

References are at article or control level. DORA is Regulation (EU) 2022/2554. GDPR is Regulation (EU) 2016/679. ISO is ISO/IEC 27001:2022 Annex A. The Other column uses the Stage 1 regulation IDs.

| ID | Tier | DORA | GDPR | ISO 27001:2022 Annex A | Other |
|---|---|---|---|---|---|
| CR-01 | All tiers | Art 9 | Art 32 | A.8.20; A.8.22 | none |
| CR-02 | All tiers | Art 9 | Art 32 | A.8.5; A.8.24 | none |
| CR-03 | All tiers | Art 9 | Art 32 | A.5.17; A.8.24 | none |
| CR-04 | All tiers | Art 9 | Art 32 | A.5.17 | none |
| CR-05 | All tiers | Art 9 | Art 5(1)(c); Art 32 | A.8.22; A.8.8; A.5.15 | none |
| CR-06 | Tier 1 | Art 28(8); Art 30(2)(d) | Art 28(3)(g) | A.5.18; A.5.20 | none |
| CR-07 | All tiers | Art 9 | Art 32 | A.5.16; A.5.17; A.8.5 | none |
| CR-08 | All tiers | Art 9 | Art 32 | A.5.16; A.5.18; A.6.5 | none |
| CR-09 | All tiers | Art 9 | Art 28(3)(b); Art 32 | A.8.2; A.8.15 | none |
| CR-10 | All tiers | Art 9 | Art 32 | A.8.3; A.5.15 | none |
| CR-11 | All tiers | Art 9 | n/a | A.8.26; A.8.32 | none |
| CR-12 | All tiers | Art 30(2)(c); Art 30(2)(d) | Art 5(1)(c); Art 5(1)(e); Art 32 | A.5.34; A.8.10; A.8.33 | none |
| CR-13 | All tiers | Art 9 | Art 32(1)(a) | A.8.24 | none |
| CR-14 | All tiers | Art 30(2)(b) | Arts 44 to 49 | A.5.34; A.5.23 | Regional rules (R9) |
| CR-15 | All tiers | Art 10 | Art 32; Art 33(2) | A.8.15; A.8.16; A.8.11 | none |
| CR-16 | Tier 1 (deeper) | Art 28(3); Art 28(4); Art 30(2)(a) | Art 28(2); Art 28(4) | A.5.19; A.5.21; A.5.22 | none |
| CR-17 | All tiers | Art 9; Art 11 | Art 5(1)(d); Art 9; Art 32 | A.8.26; A.5.34; A.5.30 | none |
| CR-18 | All tiers | Art 9 | n/a | A.8.32; A.5.3 | Allowance tax rules (R10) |
| CR-19 | All tiers | Art 9 | Art 32 | A.5.3; A.5.15 | Anti-bribery and gifts policy (R5) |
| CR-20 | All tiers | Art 9; Art 28(4) | n/a | A.5.22; A.8.24 | PCI DSS (R7) |
| CR-21 | All tiers | Art 9 | Art 5(1)(c); Art 5(1)(e) | A.5.3; A.5.15 | none |
| CR-22 | All tiers | Art 9 | n/a | A.8.26; A.5.3 | none |
| CR-23 | Tier 1 (deeper) | Art 28(4); Art 30(3)(d) | Art 28(1); Art 32(1)(d) | A.5.22; A.8.8; A.8.29 | ISO 27001 and SOC 2 (R8) |
| CR-24 | Tier 1 (deeper) | Art 11; Art 12; Art 17; Art 30(2)(e); Art 30(2)(f); Art 30(3)(a) | Art 32(1)(b); Art 32(1)(c); Art 33(2) | A.5.24; A.5.26; A.5.30; A.8.13; A.8.14 | none |
| CR-25 | Tier 1 | Art 30(2); Art 30(3); Art 28(7) | Art 28(3) | A.5.20 | none |
| CR-26 | All tiers | Art 9 | Art 32 | A.8.3; A.8.22 | none |
| CR-27 | All tiers | Art 8; Art 28(3); Art 30(2)(a) | Art 30 | A.5.9; A.8.20 | none |
| CR-28 | All tiers | Art 28(3); Art 30(2)(a) | Art 5(1)(b); Art 28(2) | A.5.19; A.5.21; A.8.26 | ISO/IEC 42001, EU AI Act (to check) |

**Note on NIS2:** Directive (EU) 2022/2555 may apply to the vendor as a service provider, while DORA is the specific rule for the bank. NIS2 is not mapped question by question here, and its applicability should be verified.

## 5. Coverage checks

**Observations from Stage 3**

| Observation | Control requirements |
|---|---|
| X1 Four openings into the bank | CR-01, CR-02, CR-05 |
| X2 Connector holds several credentials | CR-03, CR-04, CR-05, CR-06 |
| X3 Invoice path bypasses the connector | CR-11 |
| X4 SSO runs through the browser | CR-07 |
| X5 Support access from India | CR-09, CR-14 |
| X6 US providers FP9 and FP10 | CR-14, CR-15 |
| X7 Suppliers outside the bank's contract | CR-16 |
| X8 Insurer reached through the vendor | CR-17 |
| X9 Allowance rate table in the vendor console | CR-18 |
| X10 Guest data typed in by hand | CR-12, CR-21 |
| X11 Virtual card flow | CR-20 |
| X12 FW3 not controlled by the bank | CR-16 |

**Vendor claims from Stage 2**

| Claim | Control requirements |
|---|---|
| V1, V2 ISO 27001 and SOC 2 | CR-23 |
| V3 PCI DSS | CR-20, CR-23 |
| V4 Penetration test | CR-23 |
| V5 Recovery targets | CR-24 |
| V6 Data stored only in the EU | CR-14 |
| V7 Connector secrets | CR-02, CR-03, CR-04 |
| V8 Support access logged | CR-09 |
| V9 Subprocessor changes | CR-16 |
| V10 No real data in test | CR-12 |
| V11 Encryption | CR-13 |
| V12 Tenant separation | CR-26 |
| V13 AI features | CR-28 |

Every question is linked to at least one control requirement, and every flow in the Stage 3 table appears in at least one question. Both checks were run when the workbook was built.

## 6. Evidence strength and rating rules (used in Stage 5)

| Evidence strength | Examples | Supports |
|---|---|---|
| Strong | Independent report (SOC 2 Type II, ISO certificate with scope, penetration test summary). System export or configuration evidence dated within 90 days. An observed test, for example a leaver test | Satisfactory |
| Medium | A dated screenshot without an export. A policy with a small sample of records | Satisfactory for lower-risk controls, otherwise Partial |
| Weak | A policy without proof, a vendor statement, undated or marketing material | Partial at best |

| Rating | Meaning |
|---|---|
| Satisfactory | Control described and supported by suitable evidence |
| Partial | Described, but evidence is weak or coverage is incomplete |
| Gap | Absent, or contradicted by evidence |
| Not applicable | Does not apply to this service |

**Severity of a gap or partial (proposed):**

| Severity | Test |
|---|---|
| High | Could expose bulk personal data, allow fraudulent payment, give unauthorised access into the bank, or leave a mandatory contract term for a critical service unmet |
| Medium | Weakens a control, but another control compensates |
| Low | Documentation or minor |

The decision rules built on these ratings are set in Stage 5.

## 7. What is deeper because the service is Tier 1

| Area | Control requirements | Questions |
|---|---|---|
| Audit and inspection rights | CR-25 | N7 |
| Exit plan and termination | CR-06, CR-24, CR-25 | M3, N3, O7 |
| Resilience and recovery testing evidence | CR-24 | M1 |
| Fourth-party chain and advance notice | CR-16 | K1 to K5 |
| Security testing, including cooperation with threat-led testing where the authority requires it | CR-23 | L2 |
| Register of information and supervisor notification | Compliance action for the bank, not a vendor question | none |

## 8. ISO 27001 view

The workbook has an **ISO 27001 view** sheet. It lists the 39 Annex A controls that this assessment tests (18 organizational, 2 people, 19 technological), the control requirements and questions that test each one, and the evidence expected.

It shows how a vendor assessment draws on the same controls an ISMS implementer works with. It is **not a Statement of Applicability** for the bank, and it is not an ISMS implementation.

## 9. Workbook: vendor-questionnaire-and-control-map.xlsx

| Sheet | Content |
|---|---|
| Read me | How to use it, legend, rating and evidence rules |
| Control requirements | 28 requirements with sources, risk and mappings |
| Questionnaire | 87 questions in 20 domains, with flow IDs, control IDs, evidence to request and columns for the vendor response, evidence status, rating and notes |
| Regulatory map | DORA, GDPR, ISO and other references for every question |
| ISO 27001 view | Annex A controls tested |
| Summary | Counts by domain, calculated by formula |

Question IDs are a domain letter plus a number (for example H1). In the traceability matrix they carry the prefix Q-, because D, F, R and S are also used for data, factors, regulations and scope.

**ID keys added in this stage:** CR for control requirements, W for the AI questions, and the Q- prefix for questions in the matrix.
