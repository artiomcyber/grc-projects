# 🔐 CIA Triad — Practical Assessment
### GRC Mastery Course | Exercise 01

![GRC](https://img.shields.io/badge/GRC-Mastery%20Course-2E86AB?style=for-the-badge)
![Topic](https://img.shields.io/badge/Topic-CIA%20Triad-4B8BBE?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge)

---

## 📖 What is the CIA Triad?

The CIA Triad is the foundation of information security. Every security control, policy, risk assessment and audit ultimately connects back to these three principles.

| Principle | Definition | The question it answers |
|-----------|-----------|------------------------|
| **Confidentiality** | Information is only accessible to those authorised to see it | *Is only the right people seeing this?* |
| **Integrity** | Information is accurate, complete and has not been altered without authorisation | *Can we trust this data hasn't been changed?* |
| **Availability** | Information and systems are accessible when needed by authorised users | *Can we access this when we need it?* |

---

## ⚡ Key Concepts to Know

**Confidentiality controls:**
- Encryption — scrambles data so only authorised parties can read it
- Access control — restricts who can view or interact with data (RBAC, least privilege)
- Data classification — labelling data by sensitivity (Public, Internal, Confidential, Highly Confidential)
- DLP (Data Loss Prevention) — tools that detect and block unauthorised data transfers
- MFA — adds a second layer of verification beyond a password

**Integrity controls:**
- Version control — tracks every change to a document or system
- Hashing — generates a unique fingerprint of data; any modification changes the hash
- Audit logs — records who accessed or changed data and when
- Change management — formal process for approving and tracking changes to systems
- Backups — regular copies of data that can be used to restore a known-good state

**Availability controls:**
- Redundancy — duplicate systems so if one fails, another takes over
- Backups and disaster recovery — tested recovery procedures for data loss or system failure
- High availability architecture — systems designed to minimise downtime (e.g. load balancing, failover)
- BCP/DRP — Business Continuity Plan and Disaster Recovery Plan

---

## ⚠️ The CIA Tension

The three principles constantly push against each other. Good GRC work is about finding the right balance:

- **More availability** (synced everywhere) → **reduced confidentiality** (more places it could leak)
- **Strict confidentiality** (very limited access) → **reduced availability** (what if the one person with access is unavailable?)
- **Strong integrity controls** (read-only) → **reduced availability** (what if someone urgently needs to update it?)

The right balance depends on **how sensitive the asset is** and **what the organisation can tolerate**.

---

## 🏢 Practical Assessment — Oscorp

**Company:** Oscorp
**Asset:** Microsoft Word document containing the full ingredient list for a highly confidential experimental drug
**Lead:** Chief Scientist Harry Osborn
**Situation:** Document just created — no security controls in place yet

---

### 🔒 Confidentiality Assessment

A Word document with no access controls is one accidental share away from being leaked. No encryption, no access restrictions, no controls on copying or forwarding.

**Questions to ask:**
- Who currently has access to this document?
- How do you ensure only authorised individuals can access it?
- Is the file encrypted or password protected — and if yes, who holds the password?
- Are there controls preventing it from being copied to a USB drive?
- Are there controls preventing it from being sent as an email attachment or uploaded externally?

**Recommendations:**
- Store in an access-controlled, encrypted location — SharePoint with named-user permissions as a minimum
- Apply a **Highly Confidential** sensitivity label using Microsoft Information Protection or equivalent
- Enforce DLP policies to block unauthorised transfers

---

### 🛡️ Integrity Assessment

No version control or change tracking confirmed. If the ingredient list is modified — deliberately or accidentally — there is no way to detect it or revert to the correct version.

**Questions to ask:**
- Do you have regular backups of this file — and have you tested those backups?
- Are there controls in place to prevent unauthorised modification?
- Is there a version control system tracking all changes made to the document?

**Recommendations:**
- Enable document versioning in SharePoint so every change is tracked and reversible
- Enable change tracking within the Word document itself
- Store in a system that logs who accessed and modified the file with timestamps

---

### ✅ Availability Assessment

A document on a single device or unprotected share is one hardware failure away from being permanently lost — which could set the entire research project back significantly.

**Questions to ask:**
- Is this document stored on a highly available system?
- Has the storage system undergone disaster recovery testing?
- Do you have accurate backups in case the file is lost or corrupted?

**Recommendations:**
- Move to a cloud platform with built-in redundancy (e.g. SharePoint, OneDrive for Business)
- Confirm automated backups are running and recovery has been tested
- Assign a backup owner for the document in case Harry is unavailable

---

## 🎯 Priority Decision

Given this is **highly confidential pharmaceutical IP** at an early stage of development, the priority order is:

**Confidentiality → Integrity → Availability**

The biggest immediate risk is unauthorised access or leakage. Integrity and availability can be addressed in parallel but confidentiality must be locked down first.

---

## 🚀 About Me

**Artsiom** | Aspiring Cybersecurity Professional

I am an aspiring cybersecurity professional holding SC-900 (Microsoft Security, Compliance & Identity Fundamentals) and TryHackMe SEC0 certifications, actively expanding my hands-on experience through industry simulations, labs, and real-world projects. My focus areas include Governance, Risk & Compliance (GRC) and Security Operations (SOC) — working towards a career where I can help organizations build resilient security programs and respond effectively to evolving cyber threats.

- 🐙 GitHub: [@artiomcyber](https://github.com/artiomcyber)
- 🏅 Certifications: SC-900 | SEC0
- 🎯 Target Roles: SOC Analyst | GRC Analyst | Security Awareness | Threat Analyst

---

*⚠️ Oscorp and all scenario details are fictional and used for educational purposes only.*
