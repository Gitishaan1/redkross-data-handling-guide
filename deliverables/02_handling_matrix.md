# 02. Handling Matrix: KLP BANKS

**Purpose:** State exactly what staff must and must not do with information at each level, across the six required rule areas: **storage, sharing, access, retention, disposal, incident reporting**.
**Read with:** [Classification register](01_classification_register.md) (which data is at which level).

**Reading guide**

- Every rule is a "must" or "must not" statement that an employee can follow and an auditor can check.
- **◆** marks a value chosen by the author as a design decision (for example a review interval or a deadline). These are *not* legal requirements. A real bank would set them through its own risk assessment.
- Each level **relaxes** the one above it, but never drops the baseline: unique logins, patched and malware-protected devices, and approved tools apply at every level.
- Standards referenced: ISO/IEC 27001:2022 Annex A (5.12, 5.13, 5.14, 8.3, 8.10) and ISO/IEC 27002:2022 guidance, NIST SP 800-88 Rev. 2, India's DPDP Act 2023 and DPDP Rules 2025, CERT-In Directions (28 April 2022), RBI cyber security directions for banks.

---

## A. CONFIDENTIAL

| Rule area | Rule | Threats addressed |
|---|---|---|
| **Storage** | 1. Store only on bank-approved, access-controlled systems, encrypted at rest.<br>2. Never store on personal devices, removable media, personal email or cloud accounts, or unapproved SaaS tools.<br>3. Keep encryption keys in a dedicated key-management system or hardware security module, separate from the data. No single person may hold or use a key alone (dual control). Every key access is logged.<br>4. Keep copies to the minimum needed. Backups are allowed only if encrypted, access-controlled, stored separately and restore-tested ◆.<br>5. Keep paper records in locked cabinets or vaults with a sign-out record. | Key compromise, insider theft, lost or stolen devices, ransomware, stolen backups, unauthorised copies on unapproved tools |
| **Sharing** | 1. Share only with named recipients who have a documented need to know, approved by the data owner.<br>2. Use only bank-approved channels, encrypted in transit. Send the password or key through a separate channel.<br>3. Never use personal email, messaging apps, public links or USB drives.<br>4. External transfers need a signed transfer agreement and a time-limited, access-controlled link ◆.<br>5. Verify the recipient's identity before sending (for example by call-back), and mask or minimise data where the full record is not needed.<br>6. Do not discuss in public areas. Physical documents travel sealed, tracked and signed for.<br>7. Log every transfer. | Misdirected email, interception, data leaving through unapproved tools, impersonation by phishers, third-party leaks |
| **Access** | 1. Grant access by role on a least-privilege, need-to-know basis, with written justification and data-owner approval. Seniority or job title (including managers and IT administrators) never grants access automatically.<br>2. Multi-factor authentication is mandatory.<br>3. Temporary access has an expiry, extra logging and automatic revocation.<br>4. Review all access at least quarterly ◆, and remove it immediately on role change or exit.<br>5. Log all access to Confidential data and alert on unusual activity (bulk downloads, off-hours access).<br>6. Administrators must not be the only reviewers of their own activity logs (segregation of duties). | Insider snooping, a compromised account reaching everything, privilege creep, stolen credentials, administrators covering their tracks |
| **Retention** | 1. The data owner maintains a retention schedule per data type, approved by Compliance and aligned with banking regulations (RBI, KYC and anti-money-laundering record-keeping) and DPDP.<br>2. Keep personal data only as long as its purpose or a legal requirement demands. Where a law requires keeping it, record which rule applies.<br>3. When a retention period ends, disposal must begin within 30 days ◆.<br>4. Keep security and access logs for Confidential data for at least the longest period any applicable rule requires. DPDP Rules: one year. Secondary sources report CERT-In 180 days and a longer RBI period; KLP's design choice is two years ◆ pending verification against the primary texts.<br>5. Review the schedule annually ◆. | **Over-retention:** a larger breach and a DPDP violation. **Under-retention:** no forensic evidence and a failure to meet regulatory duties |
| **Disposal** | 1. Dispose of data using NIST SP 800-88 Rev. 2. For Confidential data, *clear* alone is not enough ◆. Use **purge** (for example cryptographic erase on encrypted drives and cloud storage) or **destroy** (paper shredding, physical destruction of media), depending on the media.<br>2. Apply it to every copy, including backups and replicas.<br>3. The data owner authorises disposal, and a legal hold blocks it.<br>4. Verify afterwards (sample checks) and keep a record: what, when, method, who performed it, who verified it (ISO/IEC 27001 A.8.10 evidence).<br>5. Third parties need a contract requiring confidentiality, a certificate of destruction, audit rights and no retained copies. | Data recovered from discarded or reused media, leftover data in backups, vendors keeping copies |
| **Incident reporting** | 1. Any staff member who notices a suspected or confirmed incident involving Confidential data (loss, unauthorised access, misdirected disclosure, malware, lost device) reports it immediately to the named Security Incident Response contact, within 1 hour ◆.<br>2. Staff must not investigate alone or delete evidence.<br>3. Good-faith reporting is never punished.<br>4. The response team assesses, contains and escalates to the CISO and Compliance, who handle external reporting: **CERT-In within 6 hours** of noticing; **RBI** within its prescribed window (secondary sources report 2 to 6 hours; confirm in the primary text); the **Data Protection Board within 72 hours** of becoming aware, with affected individuals told without delay.<br>5. Record every incident and review it afterwards for lessons. | Delayed containment, continued data theft, regulatory penalties, customers not warned in time |

---

## B. INTERNAL

| Rule area | Rule | Threats addressed |
|---|---|---|
| **Storage** | 1. Store on bank-approved systems behind staff login.<br>2. Laptops and mobiles use full-disk encryption ◆.<br>3. Removable media only if bank-issued and encrypted ◆. No personal cloud or email accounts.<br>4. Standard IT backups apply.<br>5. Paper stays in staff-only areas and is locked away when unattended. | Lost devices, shadow IT, malware introduced by USB drives, visitors seeing documents |
| **Sharing** | 1. Share only with staff and partners under NDA.<br>2. Use approved channels (official email, intranet). No personal email or messaging apps.<br>3. External sharing needs manager approval and an NDA ◆.<br>4. Never post on public forums or social media. | Leaks to competitors or scammers, social-engineering reconnaissance, unofficial channels |
| **Access** | 1. All authenticated staff by default, with unique IDs; MFA for remote access ◆.<br>2. Contractors and partners need a sponsor and a time limit.<br>3. Review access at least annually ◆, and remove it on exit.<br>4. Access is logged; logs are reviewed when investigating an incident. | Unauthorised outsiders, lingering contractor access, privilege creep |
| **Retention** | 1. Keep according to the department's retention schedule, reviewed annually ◆.<br>2. Delete when no longer needed, unless a legal retention rule applies. | Unnecessary accumulation of data, outdated documents misleading staff |
| **Disposal** | 1. NIST **clear** is enough for media that stays under the bank's control ◆.<br>2. Any media leaving the bank's control (resale, repair, return) must be at least **purged** ◆.<br>3. Paper goes into approved shredding bins.<br>4. Keep a record for bulk disposal of devices; deleting a single file needs none. | Data recovered from resold or repaired devices, documents recovered from bins |
| **Incident reporting** | 1. Report suspected loss or leak to the IT security contact within 24 hours ◆, using the normal service channel.<br>2. Security triages and escalates to the Confidential process if Confidential data was involved.<br>3. If the incident is in one of CERT-In's reportable categories, the 6-hour clock applies **whatever the data's level**.<br>4. Good-faith reports are never punished. | Small incidents growing unnoticed, under-reporting, missed regulatory deadlines |

---

## C. PUBLIC

| Rule area | Rule | Threats addressed |
|---|---|---|
| **Storage** | 1. Publish only on approved platforms (the official website and verified social media accounts).<br>2. Keep a master copy of each approved version, version-controlled and backed up.<br>3. The content needs no encryption, but the **publishing system** must be protected against tampering. | Defacement, altered content, loss of the approved original |
| **Sharing** | 1. Free to share once the data owner (for example Communications or Compliance) has approved it.<br>2. Always share the current approved version, with date and source.<br>3. Staff must not release unapproved material or speak for the bank without authorisation. | Accidental release of unapproved material, outdated versions in circulation |
| **Access** | 1. Anyone may read it.<br>2. Only named, authorised staff may **edit or publish**, with MFA, a second-person approval step ◆ and change logging.<br>3. Publishing accounts are treated as sensitive credentials. | Account takeover used to change rates or contact numbers, scam content on genuine channels |
| **Retention** | 1. Keep while still current.<br>2. Remove outdated notices (old rates, expired offers) or clearly mark them as archived ◆.<br>3. Retain mandatory disclosures (such as annual reports) as regulations require. | Customers acting on stale information, fraudsters quoting old offers |
| **Disposal** | 1. Standard deletion is enough for published content.<br>2. Unpublished **drafts** keep the level of their content (often Internal or Confidential) until approved.<br>3. Publishing credentials and backups follow Confidential rules. | Leaked drafts, credentials remaining after staff changes |
| **Incident reporting** | 1. Report defaced pages, altered documents, fake accounts or apps, and phishing that uses the bank's branding to Communications and Security the same business day ◆.<br>2. Escalate immediately if it falls into a CERT-In reportable category (for example a fake mobile app imitating the bank's). | Brand impersonation, customer fraud using the bank's name, missed CERT-In deadline |

---

## D. How the levels scale

| Dimension | Public | Internal | Confidential |
|---|---|---|---|
| **Who may read** | Anyone | Staff and NDA partners | Named roles with need to know |
| **Who may change** | Authorised publishers, with approval | Owners and authorised staff | Authorised staff, with approval and logging |
| **Technical protection** | Protect the publishing system | Device encryption, approved channels | Encryption at rest and in transit, key management, MFA |
| **Proof kept** | Change log, approved master copy | Access logs | Full access logs, transfer logs, disposal certificates |
| **Typical disposal** | Standard delete | Clear (purge if it leaves the bank) | Purge or destroy, with evidence |
| **Staff must report within** | Same business day | 24 hours ◆ | 1 hour ◆ |

## E. Mapping to the standards

| Rule area | Main source |
|---|---|
| Classification and levels | ISO/IEC 27001:2022 A.5.12; FIPS 199 and NIST SP 800-60 (impact-based reasoning) |
| Labelling | ISO/IEC 27001:2022 A.5.13 (note: a "Confidential" label can also tell an attacker where to look, so labels should be paired with access controls) |
| Sharing | ISO/IEC 27001:2022 A.5.14 |
| Access | ISO/IEC 27001:2022 A.5.15 and A.8.3 (least privilege, need to know) |
| Retention and disposal | ISO/IEC 27001:2022 A.8.10; NIST SP 800-88 Rev. 2; DPDP Act 2023 and Rules 2025 |
| Incident reporting | CERT-In Directions (28 April 2022), DPDP Rules 2025, RBI cyber security directions |
| Logs | CWE-532 (sensitive information in log files); CERT-In and DPDP log-retention requirements |
