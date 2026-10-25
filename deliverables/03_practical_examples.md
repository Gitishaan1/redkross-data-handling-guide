# 03. Practical Examples: KLP BANKS

**Purpose:** Show the classification register and handling matrix working on realistic security situations. Each scenario states the data and its level, which rules were broken, the attacker's opportunity, what the right action is, and which control would have prevented the problem.

> All people, systems and numbers below are fictional and written only for training purposes.
> These scenarios were analysed on paper (a desk-based walkthrough against the matrix). No live systems were tested or attacked.

Quick key: **C** = Confidential, **I** = Internal, **P** = Public. Rule references point to [02_handling_matrix.md](02_handling_matrix.md).

---

## Scenario 1: The customer list sent to personal email

**Situation.** A loan officer wants to finish work at home. She exports a spreadsheet of 800 loan applicants (names, phone numbers, PAN, income, loan amounts) and emails it to her personal Gmail account.

| Item | Analysis |
|---|---|
| Data and level | Customer identity and financial records. **C** (register #1) |
| Rules broken | Sharing 2 and 3 (approved channels only; never personal email). Storage 2 (never on personal email or cloud accounts). Sharing 1 (no documented need to know for the export) |
| Attacker's opportunity | If her personal mailbox is compromised (reused password, phishing), the attacker obtains 800 identities ready for fraud and targeted scams. The bank has no logs, no control and no way to delete the copy |
| Correct action | Work through the bank's approved remote-access solution. If an export is truly needed, request owner approval and use an encrypted channel with masked data |
| If it already happened | Report within **1 hour** (Incident reporting 1). The response team assesses whether it is a reportable incident: the DPDP 72-hour Board clock and CERT-In 6-hour rules may apply |
| Preventive controls | Data-loss-prevention rules that block outbound mail with PAN or account patterns; blocking personal webmail on bank devices; remote-work access that never needs local copies |

---

## Scenario 2: A phishing email and a late report

**Situation.** An operations clerk receives an email "from IT" asking him to re-verify his password. He enters his credentials on a lookalike login page. Realising his mistake an hour later, he says nothing because he fears being blamed.

| Item | Analysis |
|---|---|
| Data and level | Staff credentials (**C**, register #6) and everything they can reach |
| Rules broken | Incident reporting 1 and 3 (report immediately; good-faith reports are never punished). The culture problem, fear of blame, is the root cause |
| Attacker's opportunity | The attacker logs in using the stolen password, browses shared folders and reaches customer records. If MFA is not enforced, there is no second barrier |
| What should happen | Report within **1 hour**. Security resets the password, revokes active sessions, reviews logs for the account's activity and decides whether a reportable incident exists. CERT-In's six-hour clock starts when the bank *notices* the incident |
| What would have limited the damage | **MFA** (Access 2), least-privilege access (Access 1) so the clerk's account cannot see customer records it does not need, alerts for unusual access (Access 5), staff training that says plainly *report fast, no blame* |
| Lesson | The delay is more dangerous than the click. Every hour of silence is an hour of attacker access |

---

## Scenario 3: The debug log that records secrets

**Situation.** A developer enables verbose debugging on the mobile-banking API during testing. The application now writes request bodies to a log file, including customer account numbers, session tokens and an API key. The log file sits on a shared server readable by the whole IT department.

| Item | Analysis |
|---|---|
| Data and level | Logs (**C**, register #10) containing credentials (#6) and customer data (#1) |
| Rules broken | The "systems must never write passwords, keys or full customer data into logs" principle (register note 1). Access 1 (the log file is readable by everyone in IT). Storage 1 (unencrypted shared location) |
| Attacker's opportunity | Anyone who reaches the server, whether a malicious insider or an attacker who compromised a developer laptop, can reuse the tokens and the API key. This weakness class is catalogued as CWE-532 (sensitive information written to a log file) |
| Correct action | Stop the verbose logging, rotate the exposed key and invalidate the tokens, restrict and then securely delete the log (Disposal 1 and 2), and report the exposure as an incident |
| Preventive controls | Logging standards that mask sensitive fields; code review and automated scanning for secrets in logs; separate, access-restricted log storage; segregation of duties (Access 6) |
| Lesson | Classifying logs as Confidential is a safety net. The real fix is to stop sensitive data reaching logs at all |

---

## Scenario 4: The retired laptops

**Situation.** KLP replaces 40 branch laptops. A contractor collects them for resale. The IT team deletes the user folders and "empties the recycle bin" but does not sanitise the drives. Some laptops previously held customer documents in the Downloads folder.

| Item | Analysis |
|---|---|
| Data and level | Internal and Confidential data left on storage media |
| Rules broken | Disposal 1 and 4 (use NIST SP 800-88 methods; keep evidence). Disposal 5 (third parties need a contract, a certificate of destruction and no retained copies) |
| Attacker's opportunity | A buyer runs a file-recovery tool and gets the customer documents. Ordinary deletion removes the pointer to a file, not the data itself |
| Correct action | Media leaving the bank's control must be at least **purged** (for encrypted drives, cryptographic erase by destroying the keys, or the manufacturer's secure-erase function) or **destroyed**. Verify, record device serial numbers and methods, and obtain a certificate from the contractor. Drives that cannot be verified as purged are physically destroyed |
| Preventive controls | Full-disk encryption on all laptops from day one (then cryptographic erase is quick and reliable); an asset register that tracks every device until verified disposal; a formal media-sanitisation programme with owners, as NIST SP 800-88 Rev. 2 now emphasises |
| Lesson | "Delete" is not disposal |

---

## Scenario 5: The misdirected statement

**Situation.** A branch employee emails a customer's loan statement to a similarly named customer after picking the wrong autocomplete suggestion. The recipient replies "not mine", and deletes the email.

| Item | Analysis |
|---|---|
| Data and level | Customer financial records. **C** |
| Rules broken | Sharing 5 (verify the recipient's identity before sending). The mistake itself was human error; the failure was that the process allowed unverified sending |
| Attacker's opportunity | The wrong recipient could be a fraudster. Even if honest, the data left the bank's control unencrypted |
| Correct action | Report within 1 hour. Compliance assesses whether this is a personal-data breach under DPDP. If so, the Board report (72 hours from awareness) and notice to the affected customer (without delay) follow. Ask the recipient to confirm deletion in writing, and document what happened |
| Preventive controls | Disable email autocomplete for external addresses; send statements only through the authenticated customer portal; mail gateway warnings for external recipients with attachments; encryption of statements with a separate key |
| Lesson | Even a small mistake can be a legal breach. A no-blame, fast-report culture lets the bank meet its deadlines |

---

## Scenario 6: The altered rate sheet and the fake app

**Situation.** Two events in one week. First, an attacker compromises the credentials of a web-content editor and changes the published fixed-deposit rate and customer-care phone number on the bank's website. Second, a fake "KLP Mobile Banking" app appears on a third-party download site.

| Item | Analysis |
|---|---|
| Data and level | Published rates and contact numbers. **P** |
| Why this matters | Public data has no secrecy requirement, but its **integrity** matters. Customers who call the altered number reach a scammer who asks for OTPs and card details |
| Rules involved | Public access 2 and 3 (only named staff may edit, with MFA and a second-person approval). Public incident reporting 1 and 2 |
| Correct action | Restore the approved master copy (Public storage 2), reset the editor's credentials and sessions, warn customers through verified channels, and report the fake app. Fake apps imitating an organisation's real one can be reportable to CERT-In within six hours even with no proven harm |
| Preventive controls | MFA and approval workflow on publishing; change monitoring on the website with alerts; a brand-monitoring process for lookalike apps and domains |
| Lesson | Public does not mean unprotected. Protect the ability to *change* it |

---

## Scenario 7: The contractor who never left

**Situation.** An external contractor finishes a three-month data-migration project. The project manager forgets to inform IT. Six months later the contractor's account is still active with access to customer-record systems. An attacker obtains the contractor's reused password from an unrelated public breach.

| Item | Analysis |
|---|---|
| Data and level | Customer records. **C** |
| Rules broken | Access 3 (temporary access must expire and auto-revoke) and Access 4 (quarterly review, immediate removal on exit) |
| Attacker's opportunity | The credentials work, MFA is not enforced for contractors, and the account's privileges match the old project, far wider than any current need |
| Correct action | Disable the account, review logs for its activity since the project ended, rotate related secrets, and report if unauthorised access occurred |
| Preventive controls | Sponsor-owned, time-limited contractor accounts that expire automatically; regular access reviews; MFA for everyone; alerts for dormant accounts that suddenly become active |
| Lesson | Access that nobody owns becomes the attacker's easiest way in |

---

## Scenario 8: The old KYC files nobody deleted

**Situation.** A file server at KLP still holds scanned KYC documents for customers who closed their accounts more than a decade ago. Nobody knows who owns the folder. A ransomware group encrypts the server and publishes the stolen data.

| Item | Analysis |
|---|---|
| Data and level | Former customer records. **C** (register #9) |
| Rules broken | Retention 1 to 3 (an owner-run schedule; delete when the purpose ends unless a law requires keeping; start disposal within 30 days after the period ends). Storage 4 (minimise copies) |
| Attacker's opportunity | Data that served no purpose still increased the size of the breach. Former customers are also less likely to notice and act on a warning |
| Correct action | Treat as a serious incident: contain, report within the CERT-In and DPDP windows, and notify affected people. Afterwards, identify an owner and apply the retention schedule. Where a banking law requires keeping certain records for a fixed period, document that rule and keep those records, but delete the rest |
| Preventive controls | Data inventory with named owners; automatic expiry reminders; archive storage that is encrypted and access-restricted; periodic discovery scans for personal data |
| Lesson | Over-retention is a security risk, not just tidiness. The data you do not hold cannot be stolen |

---

## Summary: scenarios against the matrix

| Scenario | Main rule area | Level | Core lesson |
|---|---|---|---|
| 1. Customer list to personal email | Sharing, Storage | C | Approved channels only |
| 2. Phishing and late report | Incident reporting, Access | C | Report fast, no blame |
| 3. Secrets in logs | Access, Storage | C | Fix the source, not just the label |
| 4. Retired laptops | Disposal | I and C | Delete is not disposal |
| 5. Misdirected statement | Sharing, Incident reporting | C | Verify recipients; breaches have clocks |
| 6. Altered rate sheet, fake app | Access, Incident reporting | P | Public data needs integrity |
| 7. Lingering contractor access | Access | C | Access needs an owner and an expiry |
| 8. Old KYC files | Retention | C | Over-retention enlarges breaches |
