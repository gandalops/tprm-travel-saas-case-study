# Decision memo: onboarding Vendor X travel platform (after the follow-up assessment)

> **Fictional case study.** Example Bank and Vendor X are placeholders. All vendor replies, evidence, dates and scores are simulated. Legal references are indicative and must be checked against the official texts. Drafted with AI assistance and reviewed by the author.
>
> **Status:** Confirmed by author.

> **Date:** 4 Dec 2026. **Replaces:** the memo of 4 Oct 2026 (kept unchanged in `05-assessment`). **For:** risk committee, 11 Dec 2026.

## 1. Management summary

| Item | Result |
|---|---|
| Service | Corporate travel management platform (SaaS), Tier 1, critical or important function, treated as outsourcing and as an ICT service |
| Inherent risk | Very high (25 of 27) |
| Follow-up | 65 new questions and 23 re-asked, 22 open findings re-examined, the vendor's physical architecture reviewed |
| High findings open | 5 in the initial assessment, now **2**: FND-05 (audit rights) and FND-23 (US backup replication, new) |
| All findings | 33: 11 closed, avoided or accepted; 22 open (2 High, 13 Medium, 7 Low) |
| Risks | The 17 existing risks at High or above fell from 6 to 3. One new risk is Very high (US backups) |
| Go-live conditions | 4 of 10 met or met with residual |
| **Recommendation** | **Conditional approval is kept. Go-live on 1 Feb 2027 is not yet cleared.** The decision gate is 15 Jan 2027 |

**Why not clear go-live now.** The vendor's own diagram shows backups replicated to a US region, which contradicts its EU-only claim, and it has committed to remove them but has not yet shown deletion. The vendor's answer on audit rights does not give the bank and its authorities unrestricted access, which is expected for a critical service.

**Why not reject.** Most findings moved in the right direction with verified evidence: credentials, break-glass access, VIP data, log redaction, recovery testing and PCI scope are closed or reduced, and the AI assistant is off.

## 2. What changed since the initial assessment

| Area | Initial assessment | After the follow-up |
|---|---|---|
| High findings | 5 | 2 (1 closed, 1 avoided, 2 reduced to Medium, 1 new) |
| Findings total | 22 | 33 |
| Risks at High or above (existing 17) | 6 | 3 |
| Conditions | 8 plus 2 feature gates | 10 plus 2 feature gates |
| Decision | Conditional approval | Conditional approval, go-live not yet cleared |

## 3. Go-live conditions (due 15 Jan 2027)

| Action | Condition | Status | Evidence | Residual or next step |
|---|---|---|---|---|
| REM-01 | Secret read access limited to named roles, with approval and logging | Verified | EV-28, EV-26 | None |
| REM-02 | Credentials rotate at least every 90 days and the bank can revoke them | Verified with residual | EV-29, EV-30 | No self-service revoke. Vendor revokes in 4 hours. Reassess Feb 2027 |
| REM-03 | Just-in-time production access, masked data offshore, transfer assessment | Verified with residual | EV-26, EV-27, EV-31 | Masking by 30 Apr 2027 |
| REM-05 | Unrestricted audit, access and inspection rights in the contract | Not met | EV-34 | Vendor counter is not unrestricted. Risk committee decision |
| REM-08 | SOC 2 bridge letter | Verified | EV-36 | Scope extension by 31 Dec 2027 |
| REM-12 | Notice and a right to object for every subprocessor change | In progress | EV-45 | Agreed in the redline, not signed |
| REM-15 | Insolvency and data-return clause, credentials revoked within 24 hours of the end | In progress | EV-45 | Agreed in the redline, not signed. Exit test by 30 Jun 2027 |
| REM-16 | Incident notice within 24 hours and an assistance rate card | Partly met | EV-46 | 48 hours offered. Legal decides |
| REM-23 | No data stored outside the EU (new High) | Not met | EV-47 | Vendor committed to delete by 15 Dec 2026. Evidence pending |
| REM-32 | Liability cap aligned with the potential loss (new) | In progress | EV-61 | Negotiating a higher cap for data breach |

**Feature gates:** the AI assistant stays off for the bank (REM-04, verified) and virtual cards can be enabled (REM-06, verified through the assessor letter).

## 4. Decisions for the risk committee

**FND-05, audit and inspection rights (High).** The vendor offers two on-site audits a year with 10 working days' notice, unrestricted rights for regulators, and pooled audits.

| Option | Effect | View |
|---|---|---|
| A. Accept the vendor's offer | Go-live stays on 1 Feb. The bank's own audit access is limited | Not recommended. A missing mandatory contract term for a critical service counts as High under the decision rules |
| B. Hold for unrestricted rights, with reasonable procedure | Go-live depends on the contract. The vendor may agree with guardrails, for example advance notice except after an incident or an authority request | **Recommended** |
| C. Accept temporarily with a renegotiation in six months | Go-live stays on 1 Feb, with a known gap | Not recommended without a signed exception from the committee |

**FND-23, US backup replication (High).** The vendor committed to stop the replication and delete the US copies by 15 Dec 2026. Condition: a deletion certificate and a new region diagram, checked by the Bank DPO, by 15 Jan 2027. If not delivered, go-live is postponed.

**FND-16, incident notice.** The vendor offers 48 hours, not 24. The vendor's 2024 incident took 52 hours to notify. Recommendation: do not accept 48 hours alone. Ask for a preliminary notice within 24 hours of detection for major incidents, written into the contract, and keep the bank's own detection.

**FND-32, liability cap.** The contract cap (about EUR 0.4 million) is far below the potential loss and the vendor's cyber cover (EUR 10 million). Ask for a separate higher cap for data breach and confidentiality.

## 5. Risk treatment after the follow-up

| Treatment | What | Risks |
|---|---|---|
| Mitigate | Close the remaining actions with verified evidence | RR-01, 02, 04, 05, 07, 09, 10, 12, 18, 19, 20, 21 |
| Avoid | AI assistant off. EU-first rollout | RR-03, RR-15 |
| Transfer | Contract: audit rights, notice, liability cap, exit clauses | RR-08, RR-11 |
| Accept | Compensating controls for mutual TLS, signed by Bank IT security. Minor items tracked | Part of RR-01, RR-17 |

Risks already mitigated with verified evidence: RR-06, RR-13, RR-14, RR-16.

## 6. Residual risk

After follow-up the verified picture is 1 Very high, 3 High, 13 Medium and 4 Low among 21 risks. The target after the remaining actions is no risk above Medium (12 Medium, 9 Low). The three High risks today are support access from India (RR-02), late notice and the liability cap (RR-08), and audit and exit rights (RR-11), and the Very high risk is the US backups (RR-18).

## 7. Next steps

| Step | Owner | When |
|---|---|---|
| Risk committee decision on FND-05 and the notice period | Risk committee | 11 Dec 2026 |
| Verify deletion of the US backups | Bank DPO | By 15 Jan 2027 |
| Sign the contract with the agreed clauses (subprocessor notice, insolvency, revocation) | Bank Legal | By 15 Jan 2027 |
| Go or no-go meeting | Business owner, TPRM, risk committee | 15 Jan 2027 |
| Complete the 90-day actions | Vendor X, bank owners | By 30 Apr 2027 |
| Reassess after the second credential rotation | Bank IT security | Feb 2027 |

## 8. Bank's own actions

Thirteen actions (BA-01 to BA-13) are tracked in the workbook. They include the invoice call-back check, the quarterly review of booker accounts, the weekly review of rate-table changes, the kill-switch runbook for the connector, the register of information entry, the supervisor notification check and the mapping of the 14 SOC 2 customer controls.

## 9. Monitoring

The 13 key risk indicators and the reassessment schedule from the initial assessment continue. After go-live the first checks are the second credential rotation, the support access logs and the arrival of the signed contract.

## 10. Sign-off (pending)

| Role | Name | Decision | Date |
|---|---|---|---|
| Third-party risk (author) | | Recommends conditional approval, go-live not yet cleared | 4 Dec 2026 |
| Business owner (Head of HR) | | Pending | |
| IT security lead | | Pending | |
| Data protection officer | | Pending | |
| Compliance | | Pending | |
| Head of Finance | | Pending | |
| Legal and Procurement | | Pending | |
| Risk committee (final approval) | | Pending | 11 Dec 2026 |

## 11. History

| Assessment | Date | Result |
|---|---|---|
| Initial assessment | 4 Oct 2026 | Conditional approval. 22 findings, 5 High |
| Follow-up assessment | 4 Dec 2026 | 33 findings, 2 High open. Go-live not yet cleared |
