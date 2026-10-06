# Stage 3: Architecture and data flows

> **Fictional case study.** Example Bank, Vendor X and all flows are simulated. Protocols and ports are assumptions (typical defaults) and must be checked against a real integration specification.
>
> **Builds on:** Stage 1 (scope, data, process steps) and Stage 2 (vendor claims, fourth parties, and decision A12: the vendor operates the connector).

## 1. Purpose of this stage

Show how the two parties connect in practice, so that the questions in Stage 4 come from the architecture and not from a generic checklist. For every flow we record who opens the connection, which boundary it crosses, which data moves, and what could go wrong.

## 2. Trust zones and boundaries

| ID | Zone or boundary | Who controls it | Note |
|---|---|---|---|
| Z1 | Bank internal network | Bank | HR system, HR portal, IdP, expense or payroll system, ERP |
| Z2 | Internet | Nobody | Untrusted, encrypted in transit only |
| Z3 | Vendor X cloud | Vendor | Connector, login service, roster, platform, invoicing, support tools |
| Z4 | Suppliers and insurer | Fourth parties | FP1 to FP10, including the bank's own group insurer (FP5) |
| FW1 | Bank edge firewall | Bank | The bank decides what may come in. **Every inbound opening is a decision the bank owns** |
| FW2 | Vendor edge firewall | Vendor | Controls access to the vendor cloud. The bank can only check evidence |
| FW3 | Vendor to suppliers | Vendor | **The bank cannot enforce or audit this boundary.** Only the contract and the subprocessor list cover it |

## 3. The diagram

![Network architecture with trust boundaries](network-architecture.png)

How to read it:

- An arrow points **from the system that opens the connection to the system that receives it**. This is the direction you need when writing firewall rules.
- The dashed line (FS) is single sign-on. It runs through the user's browser, not between servers.
- The connector sits in the **vendor** zone (decision A12). It calls into the bank, so the bank must open FW1 for it.
- The invoicing path (F7, F8) goes straight between the vendor and the ERP and **does not use the connector**.

An editable vector version is in `network-architecture.svg`.

## 4. Data-flow table

All connections are assumed to use HTTPS (TLS) with token-based authentication unless stated.

| ID | Step | From to | Data | Protocol (assumed) | Opened by | Boundaries crossed | Main exposure |
|---|---|---|---|---|---|---|---|
| FS | S8 | User's browser to vendor login, redirected to bank IdP | D1, D7 | HTTPS, SAML or OIDC | User's browser | FW1 out, FW2 in | Local logins left enabled, weak MFA, hijacked session |
| FA | A | Connector to HR system | D1, nightly, agreed fields only | HTTPS REST (SFTP as alternative) | Connector | FW2 out, FW1 in | Opening into the bank. A stolen credential allows bulk reading of employee data |
| F1, F2 | 1, 2 | Employee and manager to HR portal | D1, D4 | Internal | Employee | None | Inside the bank. Shown for completeness |
| F3 | 3 | Connector to HR portal, then to the platform | D1, D4. D2, D3, D8, D9, D11 only when the booking needs them | HTTPS REST | Connector | FW2 out, FW1 in | Passport data pulled at booking time. Forged or replayed approval |
| F4 | 4 | Platform to roster database | D1, D4, D16 | Vendor internal | Platform | None | Tenant separation, support staff access |
| F5a | 5 | Platform to airlines and GDS (FP2) | D1, D2, D3, D4, D9, D13 | HTTPS, GDS or airline APIs | Platform | FW3 | Passport data goes to independent controllers with no bank contract |
| F5b | 5 | Platform to hotels and ground transport (FP3) | D1, D4, D9, D13 | HTTPS | Platform | FW3 | Name and dates shared widely |
| F5c | 5 | Platform to visa agency (FP4) | D2, D3, D8, D11 | HTTPS or secure upload | Platform | FW3 | Passport copy and photo leave to agencies in destination countries |
| F5d | 5, S9 | Platform to gifts marketplace (FP7) | D12 | HTTPS | Platform | FW3 | Third-party recipient data |
| F6 | 6 | Connector to HR portal | D5 | HTTPS REST | Connector | FW2 out, FW1 in | Wrong reference to the wrong employee. Low sensitivity |
| F7 | 7 | Vendor invoicing to ERP | D6, trip reference, cost centre | HTTPS API or SFTP file | Invoicing | FW2 out, FW1 in | **Bypasses the connector.** Tampered or duplicate invoice injected into finance |
| F8 | 8 | ERP to vendor invoicing (remittance advice) | D6 | HTTPS or SFTP | Bank ERP | FW1 out, FW2 in | Payment details. The payment itself uses normal bank channels (A15) |
| F9 | 9 | Platform to group insurer (FP5), certificate returns | D1, D2, D3, D4, D15 | HTTPS API | Platform | FW3 | The bank's own third party is reached through the vendor. Health data in assistance requests |
| F10 | 10 | Finance admin's browser to platform (rate table) | D16 | HTTPS through SSO | Finance admin | FW1 out, FW2 in | Wrong or unauthorised rate change |
| F11 | 11 | Connector to expense or payroll system | D1, D16 | HTTPS REST | Connector | FW2 out, FW1 in | Opening into the bank. Altered allowance amounts reach payment |
| F12 | 12 | Platform to Card Provider Y (FP6) | D14, D6, D1 | HTTPS API | Platform | FW3 | Card data and limits. PCI scope is split between vendor and provider |
| FG | S5 | Booker's browser to platform | D10, D2, D3, D4 | HTTPS through SSO | Booker | FW1 out, FW2 in | Guest data typed in by hand, outside the HR sync |
| FN | none | Platform to email and SMS provider (FP9) | D1, D4, D5 | HTTPS | Platform | FW3 | US-based provider, transfer outside the EU |
| FL | none | Platform to monitoring provider (FP10) | Logs that may contain D1, D4, D5 | HTTPS | Platform | FW3 | US-based provider, personal data in logs |
| FH | none | Platform hosted at cloud provider (FP1) | All data, encrypted | Provider internal | Vendor | FW3 | Hosting dependency, key control, concentration |
| FV | none | Vendor support staff (Ireland, India) to production data | D1 to D16 as needed, including executive itineraries | Admin tool, remote | Vendor staff | EU border (not a bank firewall) | Privileged access from a third country |

## 5. Exposed paths

| Boundary | Flows | What it means |
|---|---|---|
| **FW1 inbound to the bank** | FA to the HR system, F3 and F6 to the HR portal, F11 to the expense or payroll system, F7 to the ERP | **Four openings into the bank, all opened from the vendor cloud.** The bank decides which source addresses and accounts are allowed |
| FW1 outbound from the bank | FS, FG, F10, F8 | Users and the ERP reach the vendor |
| FW2 | The same flows, from the vendor side | The bank can only verify the vendor's controls through evidence |
| FW3 | F5a to F5d, F9, F12, FN, FL, FH | **The bank has no technical control and no contract with most of these parties** |
| Bypass of the connector | F7, F8, FS, FG, F10 | Connector controls (read-only account, token, fixed address) do not cover these. The invoice path needs its own review |
| Crosses the EU border | FV, FN, FL, parts of F5 | Transfer rules apply |

## 6. Where each data type goes

| Data | Bank to vendor | Vendor to fourth parties |
|---|---|---|
| D1 Employee identity | FA, F3, FS | FP2, FP3, FP5, FP6, FP8, FP9, FP10 |
| D2 Passport details | F3, FG | FP2, FP4, FP5, FP8 |
| D3 Date of birth | F3, FG | FP2, FP4, FP5 |
| D4 Trip details | F3, FG | FP2, FP3, FP5, FP8, FP9, FP10 |
| D5 Booking references | none (created by the vendor, F6 to the bank) | FP9 |
| D6 Invoice data | none (created by the vendor, F7 to the bank) | FP6 |
| D7 Credentials and tokens | Used in FA, F3, F6, F11, FS | Held by the vendor |
| D8 Visa data | F3 | FP4 |
| D9 Special requests | F3 | FP2, FP3 |
| D10 Guest data | FG | FP2, FP3, and FP5 if insured |
| D11 Contact and home address | F3 | FP4, FP5, FP8 |
| D12 Gift recipient data | By the booker through FS | FP7 |
| D13 Loyalty numbers | F3 | FP2, FP3 |
| D14 Virtual card data | none (created by FP6) | FP6, then used with FP2 and FP3 |
| D15 Insurance data | Returns from FP5 (F9), FP8 | FP5, FP8 |
| D16 Allowance data | F10 (rate table), F11 returns to the bank | none |

## 7. Observations from the architecture

Each observation feeds a control requirement in Stage 4.

| ID | Observation | Why it matters | Related claim | Existing questions | New question needed |
|---|---|---|---|---|---|
| X1 | Four openings into the bank, all opened from the vendor cloud | A compromised vendor connector reaches the HR system, HR portal, expense system and ERP | V7 | H1, H2, H3, E2 | Fixed vendor source addresses, mutual TLS |
| X2 | The connector holds credentials for three bank systems in one place | Single point of compromise | V7 | E3, D1, D2 | Vault, rotation, who can read secrets |
| X3 | Invoice and remittance bypass the connector | Connector controls do not apply | None | G1, G2, G3, H3 | Invoice authentication, duplicate check, change of bank details |
| X4 | SSO runs through the user's browser | Only as strong as the bank's MFA and the vendor's SSO enforcement | None | B1, B2, B3, B4 | None |
| X5 | Vendor support staff in India can reach production data | Transfer outside the EU and privileged access to executive itineraries | V6, V8 | D2, I2, J1 | Just-in-time access, restriction by region |
| X6 | FP9 and FP10 are US-based | Transfers outside the EU, personal data in logs | V6 | I2, K1, K2 | Log redaction |
| X7 | Suppliers are outside the bank's contract, some are independent controllers | No audit right, onward sharing, passport data to visa agencies | V9 | K1, K2, I2, I3 | Data per supplier, deletion after visa processing |
| X8 | The group insurer receives data through the vendor | The bank's third party is reached through another third party | None | E1, H3 | Accuracy and mapping of the hand-off |
| X9 | The allowance rate table is edited in the vendor console | Financial leakage or fraud | None | D3, F1, F3 | Finance-only role, change approval, audit trail |
| X10 | Guest data is typed in by hand | Outside the HR sync, retention unclear | None | E1, I3, I4 | Guest data retention and deletion |
| X11 | Virtual card flow F12 | Card data, spending limits, split PCI scope | V3 | I1, I4 | Card limits, token instead of card number, attestation for both parties |
| X12 | The bank does not control FW3 | Only the contract and the subprocessor list apply | V9 | K1, K2, N1 | Advance notice and a right to object |

## 8. Worked example: reading flow FA

1. **Flow:** the connector opens an HTTPS connection to the HR system every night and pulls the agreed fields.
2. **Boundaries:** it leaves the vendor cloud through FW2 and enters the bank through FW1.
3. **Exposure:** an inbound opening exists in the bank edge, and a service account with read access to the employee list sits in the vendor's cloud.
4. **Risk:** if that account is stolen, an attacker can read the employee list in bulk.
5. **Questions this triggers:** how the credential is stored and rotated (E3), how long the nightly copy is kept (I3), whether the source addresses are fixed (H1), whether only the agreed fields are pulled (E1), and who at the vendor can read the secret (D1, D2).

The same steps apply to every row in section 4.

## 9. Assumptions made in this stage

| ID | Assumption | Basis |
|---|---|---|
| A13 | Finance admins maintain the allowance rate table in the vendor console (F10) | Assumption |
| A14 | The vendor pushes invoices to an intake endpoint of the ERP (F7) | Assumption |
| A15 | The payment itself uses the bank's normal payment channels, outside the platform. F8 carries only the remittance advice | Assumption |
| A16 | Users reach the vendor by browser with SSO. No VPN or private link is used | Assumption |

Addendum : Two data flow diagrams (level 0 and level 1) show the same flows by process and data store: dfd-level-0.png and dfd-level-1.png

