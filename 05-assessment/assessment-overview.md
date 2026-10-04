# Stage 5: Assessment, findings and risk

> **Fictional case study. Everything Vendor X says, shows or provides in this stage is simulated.** Names, dates, evidence and numbers are invented. Legal references are indicative and must be checked against the official texts. Drafted with AI assistance (Claude), to be reviewed by the author.
>
> **Status:** Confirmed by author.
> **Builds on:** Stage 1 v1.0, Stage 2, Stage 3 v1.0 (frozen) and Stage 4 (controls, questionnaire, mapping).

## 1. What this stage contains

| File | Content |
|---|---|
| `assessment-workbook.xlsx` | Questionnaire with simulated answers, Summary, Findings, Risk register, Remediation plan, Monitoring, Evidence log, plus the Stage 4 sheets |
| `decision-memo.md` | The decision, risk treatment, conditions and a one-page management summary |
| `incident-scenario.md` | A tabletop exercise: a stolen connector credential |
| `../traceability-matrix.xlsx` | One row per thread, from flow to decision |

## 2. How the assessment was run

1. **Priority questions.** 64 of the 87 questions were answered. They cover the controls tied to the Stage 3 observations and the Stage 2 claims. The other 23 are marked "not yet assessed" (lower priority).
2. **Simulated answers and evidence.** Each answer has a vendor response, an evidence item, a status, and a rating. Weaknesses were seeded on purpose from the Stage 2 hypotheses, so that the decision is not trivial.
3. **Rating.** The Stage 4 rules were applied: strong, medium or weak evidence, and Satisfactory, Partial or Gap.
4. **Findings.** Every Partial or Gap was grouped into a finding with a severity.
5. **Risks.** Findings feed a risk register with likelihood and impact before controls (inherent), as assessed (current), and after remediation (target).
6. **Actions and decision.** Each finding has a remediation action, and the decision rules below produce the outcome.

## 3. Results

**Ratings (64 assessed questions)**

| Rating | Count |
|---|---|
| Satisfactory | 24 |
| Partial | 32 |
| Gap | 8 |
| Not yet assessed | 23 |

**Findings (22)**

| Severity | Count |
|---|---|
| High | 5 |
| Medium | 16 |
| Low | 1 |

**The five High findings**

| ID | Finding | Why High |
|---|---|---|
| FND-01 | 11 vendor staff can read the bank's connector credentials, with no approval step | One compromise exposes several bank systems |
| FND-02 | Connector credentials rotate once a year, revocation takes up to 2 business days | A leaked credential stays valid for a long time |
| FND-03 | 22 India-based staff have standing access to production data, with no transfer assessment | Bulk personal data, including passport data |
| FND-04 | An AI model provider in the US is not in the fourth-party list, and keeps prompts for 30 days | Undisclosed fourth party receiving personal data |
| FND-05 | Audit rights are limited to one remote audit a year | A mandatory term for a critical service is unmet |

**Risks by band**

| Band | Inherent | Current | Target after remediation |
|---|---|---|---|
| Very high | 2 | 2 | 0 |
| High | 9 | 4 | 0 |
| Medium | 6 | 11 | 10 |
| Low | 0 | 0 | 7 |

The two Very high risks today are RR-02 (support access from India) and RR-03 (the AI provider). After the agreed remediation, no risk is above Medium.

**What went well:** two fixed source IP addresses, a dedicated connector instance per client, SSO enforced with MFA at the bank's IdP, tokens-only virtual cards, a recent independent penetration test, tenant separation tested, 13 months of immutable logs, and sound basic contract terms (termination, regulator cooperation).

## 4. Change after the freeze: PF-1

Question W1 revealed that the chat assistant uses a third-party model provider in the US. This provider is in neither the Stage 2 fourth-party list nor the Stage 3 diagram. Stage 3 is frozen, so it is **not edited**. The change is recorded here.

| Item | Treatment |
|---|---|
| New fourth party | FP11: AI model provider, US. To be added to Stage 2 by the author as an addendum |
| New flow | **FI:** platform to AI model provider. Data: D1, D4, and free text that may include D9. HTTPS, opened by the platform, crosses FW3 |
| New risk | RR-03 |
| Controls | CR-28 and CR-16 |
| Finding | FND-04 (High) |
| Action | REM-04: the AI assistant is disabled for the bank's tenant until the provider is contracted and listed, personal data is kept out of prompts, and retention is confirmed |

This shows how a frozen baseline handles new information: the baseline stays intact, and the change is traced to a finding and an action.

## 5. Decision rules (Confirmed by author)

| Rule | Effect |
|---|---|
| Any High finding | Must be closed and verified before go-live, or the service is not approved |
| A missing mandatory contract term for a critical service | Counts as High until fixed |
| Medium findings | Need an owner, a date and verification evidence. Pre-go-live where the contract is involved, otherwise within 90 days of go-live |
| Low findings | Tracked |
| Feature gates | A feature with an unresolved High or card-data issue stays off until verified |
| Escalation | A pre-go-live condition not verified by the deadline postpones go-live and goes to the risk committee |

## 6. Assumptions and limits

- Go-live target is 1 Feb 2027. Pre-go-live actions are due by 15 Jan 2027, and the 90-day actions by 30 Apr 2027.
- The 90-day rotation period, the 24-hour notification period and the 90-day guest retention are proposed defaults. The author or the bank's policy can change them.
- Likelihood and impact are scored 1 to 5 by judgement and are not calibrated with data.
- The evidence is invented. Its value is in showing the method, not in the values.

## 7. Handoff

- **Decision memo:** the decision, treatment of each risk, conditions, sign-offs.
- **Incident scenario:** a tabletop of the stolen credential, using the findings.
- **Final README:** the three perspectives (TPRM, ISO 27001, IT risk and GRC), the repository map, and the closing lessons.
