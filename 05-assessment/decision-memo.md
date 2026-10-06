# Decision memo: onboarding Vendor X travel platform

> **Fictional case study.** Example Bank and Vendor X are placeholders, and the assessment results are simulated. 
>
> **Date:** 4 Oct 2026

## 1. Management summary

| Item | Result |
|---|---|
| Service | Corporate travel management platform (SaaS), HR, finance and insurance integrations, for staff in the EU and other regions |
| Classification | Critical or important function, Tier 1, and treated as outsourcing as well as an ICT service |
| Inherent risk | Very high (25 of 27) |
| Assessment | 64 of 87 questions assessed: 24 Satisfactory, 32 Partial, 8 Gap |
| Findings | 22: 5 High, 16 Medium, 1 Low |
| Current risk | 2 Very high (support access from India, undisclosed AI provider), 4 High, 11 Medium |
| Risk after remediation | No risk above Medium |
| **Recommendation** | **Conditional approval. Go-live only after the pre-go-live conditions are verified. Not approved today** |
| Target go-live | 1 Feb 2027, if conditions are verified by 15 Jan 2027 |

**Why not approve now.** Five High findings remain open. The vendor's staff can read the bank's connector credentials, and those credentials rotate once a year. Support staff in India have standing access to production data without a transfer assessment. An AI provider in the US receives data without being disclosed. The audit rights in the contract do not meet what is expected for a critical service.

**Why not reject.** The vendor's basic security is sound (fixed source addresses, a dedicated connector, SSO with MFA, tested tenant separation, a recent penetration test), and every High finding has a clear, achievable fix.

## 2. Decision and risk treatment

| Treatment | What we do | Risks |
|---|---|---|
| **Mitigate** | Close 8 pre-go-live actions and 11 actions within 90 days, then verify them | RR-01, RR-02, RR-04, RR-05, RR-07, RR-09, RR-10, RR-12, RR-13, RR-14, RR-16 |
| **Avoid** | Keep the AI assistant off for the bank until REM-04 is verified. Keep virtual cards off until the attestation is verified. Roll out in the EU first | RR-03, RR-06, RR-15 |
| **Transfer** | Put audit rights, 24-hour incident notice, an assistance rate card, an insolvency clause and liability terms in the contract. Verify the vendor's EUR 10 million cyber insurance cover | RR-08, RR-11 |
| **Accept** | Minor loyalty, discount code and booker reporting gaps, which are tracked. The missing mutual TLS is accepted only with a written Bank IT security sign-off | RR-17 and part of RR-01 |

Transfer does not remove the bank's own responsibility. Contracts and insurance reduce the cost and the likelihood, but the bank remains accountable to its supervisor.

## 3. Conditions

**Before go-live (due 15 Jan 2027, verified by Bank TPRM)**

| Action | Condition |
|---|---|
| REM-01 | Secret read access limited to named roles, with approval and logging |
| REM-02 | Credentials rotate at least every 90 days, and the bank can revoke them itself |
| REM-03 | Just-in-time approval for production access, masked data offshore, transfer assessment done |
| REM-05 | Contract gives unrestricted access, inspection and audit rights |
| REM-08 | SOC 2 bridge letter provided |
| REM-12 | Contract: notice and a right to object for every subprocessor change |
| REM-15 | Contract: insolvency and data-return clause, credential revocation within 24 hours of the end |
| REM-16 | Contract: incident notice within 24 hours and an assistance rate card |

**Feature gates (the feature stays off until verified)**

| Action | Feature |
|---|---|
| REM-04 | AI assistant, until the provider is contracted, listed, and prompts exclude personal data |
| REM-06 | Virtual cards, until the vendor's attestation or an accepted scoping statement is received (target 31 Mar 2027) |

**After go-live**

| When | Actions |
|---|---|
| By 30 Apr 2027 | REM-07, 09, 10, 11, 13, 14, 17, 18, 19, 20, 21 |
| By 30 Jun 2027 | Exit plan test (part of REM-15) |
| By 31 Jul 2027 | REM-22 |
| By 31 Dec 2027 | SOC 2 and ISO scope extended (part of REM-08) |

## 4. Escalation

- A pre-go-live condition not verified by 15 Jan 2027 means go-live is postponed.
- A High finding still open at the new date goes to the risk committee, which decides between a further extension and avoiding the vendor.
- A 90-day action more than 30 days overdue is escalated to the business owner and the risk committee.

## 5. Actions for the bank

| Action | Owner |
|---|---|
| Add the service to the register of information, with the criticality classification | Compliance |
| Confirm whether the supervisor must be informed before signing (DORA Art 28(3)) | Compliance |
| Decide on a data protection impact assessment, given large-scale processing and possible special-category data | DPO |
| Negotiate the contract amendments | Legal and Procurement |
| Complete the transfer assessment for India | DPO |
| Add a call-back check for vendor bank-detail changes | Finance |

## 6. Monitoring and reassessment

Thirteen key risk indicators are reviewed monthly or quarterly (for example days since credential rotation, open High findings, hours to notify an incident, availability). The service is reassessed in full every year, with a mid-year review, and also on a trigger such as an incident, a change of ownership, a new fourth party or a new module. Details are in the Monitoring sheet of the assessment workbook.

## 7. Sign-off (pending)

| Role | Name | Decision | Date |
|---|---|---|---|
| Business owner (Head of HR) | | Pending | |
| IT security lead | | Pending | |
| Data protection officer | | Pending | |
| Compliance | | Pending | |
| Head of Finance | | Pending | |
| Legal and Procurement | | Pending | |
| Third-party risk analyst | | Recommends conditional approval | 4 Oct 2026 |
| Risk committee (final approval) | | Pending | |

## 8. Where to find the detail

Findings, risks, actions and monitoring: `assessment-workbook.xlsx`. The full thread from flow to decision: `traceability-matrix.xlsx` in the repository root.
