# NIST SP 800-63B — Password Security & Authenticator Management

## Overview

| Field | Details |
|---|---|
| **Standard** | NIST SP 800-63B Revision 4 (supersedes Rev. 3, effective August 2025) |
| **Scope** | Memorized secrets, authenticator management, digital identity |
| **Maps to** | NIST SP 800-53 Rev. 5 — IA-5 (Authenticator Management) |
| **Completed** | June 2026 |

## Files

| File | Description |
|---|---|
| `README.md` | Standard breakdown, key changes, requirements, NIST references |
| [`FREE-password-checker-NIST.html`](./FREE-password-checker-NIST.html)  | FREE Interactive password compliance checker — runs in any browser, no install, secure |

---

## What Changed in Rev. 4

The old model was prescriptive — rules for rules' sake. Rev. 4 is risk-based. One sentence: **length and breach screening beat complexity and forced rotation.**

| Area | Rev. 3 | Rev. 4 |
|---|---|---|
| Minimum length | 8 characters | 8 characters floor — **15+ recommended** |
| Maximum length | Not specified | **64 characters** |
| Composition rules | Required (8-4 rule) | **Prohibited** — SHALL NOT impose |
| Password rotation | Every 60–90 days | **Only on suspected compromise** |
| Blocklist screening | Recommended | **Mandatory** |
| Password hints | Discouraged | **Prohibited** |
| Knowledge-based auth | Discouraged | **Prohibited** |
| Synced passkeys | Not addressed | **AAL2** |
| Device-bound passkeys | Not addressed | **AAL3** |

---

## Key Findings

**1. The 8-4 rule is prohibited, not deprecated.**
Rev. 4 - Any policy still enforcing uppercase + lowercase + digit + special character is non-compliant.

**2. Forced rotation is a liability.**
60/90-day cycles produce weaker passwords, not stronger ones. NIST, PCI DSS 4.0.1, and ISO 27002:2022 all agree.

**3. SHA-256 is not a password hash.**
Speed is a feature for hashing and a vulnerability for password storage. Argon2id, bcrypt, or PBKDF2 only.

**4. Native Active Directory is not NIST-compliant for breach screening.**
It needs additional tooling. This is one of the most commonly missed gaps in enterprise password policy.

**5. SMS MFA tier matters more than MFA presence.**
An attacker who SIM-swaps a number bypasses SMS MFA entirely. Hardware keys or passkeys are the correct tier for privileged and externally-facing access.

**6. Passkeys have a formal NIST-backed path.**
Synced passkeys at AAL2, device-bound at AAL3. Organizations evaluating passwordless now have clear standardized guidance.

---

## Core Requirements

### Length
- Verifier minimum: **8 characters**
- NIST recommendation: **15+ characters**
- Maximum: **64 characters**
- Accept all Unicode, including spaces, passphrases are preferred


### No Forced Rotation
Rotate only on suspected or confirmed compromise. Forced 60/90-day cycles produce predictable password variations as attackers know this pattern. PCI DSS 4.0.1, ISO/IEC 27002:2022 (5.17), and SOC 2 have all aligned with this position.

### Mandatory Blocklist Screening
Screen every prospective password against:
- Known-compromised credential databases
- Dictionary words, sequential strings, keyboard walks
- Context-specific terms (company name, username, product name)

Run at registration, on change, and asynchronously against the existing user base. **NIST does not name a specific database**.

### Secure Storage
Store only a salted hash using a slow, memory-hard KDF:
- **Approved:** Argon2id (preferred), bcrypt, PBKDF2
- **Not acceptable:** MD5, SHA-1, standalone SHA-256

SHA-256 is fast by design, but attackers can run billions of guesses per second against stolen hashes. It is only acceptable as a primitive inside an approved KDF (e.g. PBKDF2-HMAC-SHA-256).

### Rate Limiting
Cap consecutive failed attempts. Rev. 4 sets a ceiling of 100. Most organizations enforce lower with progressive delays.

### No Hints or Knowledge-Based Auth
Both prohibited. Security questions and password hints give attackers meaningful clues toward the underlying secret.

---

## Breached Password Databases

NIST mandates breach screening but does not specify which database to use. The right choice depends on context:

| Database | Size | Cost | Use case |
|---|---|---|---|
| **[Have I Been Pwned](https://haveibeenpwned.com/Passwords)** | 847M+ | Free | Individuals, developers, browser tools |
| **[Specops](https://specopssoft.com)** | 5.5B+, updated daily | Paid | Enterprise Active Directory |
| **[Enzoic](https://www.enzoic.com)** | Billions + dark web monitoring | Paid | Enterprise AD / API |
| **Microsoft Entra ID** | Microsoft-curated list | Entra ID P1/P2 | Microsoft cloud only |

**Critical note:** Native Active Directory does not block breached passwords. Entra ID's banned password list is cloud-only and covers weak patterns, not a full breach corpus. On-premises AD requires Specops, Enzoic, or Entra ID P1/P2 licensing for full NIST compliance.

The password checker in this project uses **Have I Been Pwned** via the k-anonymity API — only the first 5 characters of the SHA-1 hash are sent. The password is never transmitted.

---

## MFA Tiers

| Assurance Level | Type | Examples | Phishing-resistant |
|---|---|---|---|
| **AAL3** | Device-bound cryptographic | FIDO2/WebAuthn hardware keys, PIV smart cards | ✅ |
| **AAL2** | Synced passkeys, TOTP apps | Passkeys, authenticator apps | ✅ Passkeys / ⚠️ TOTP |
| **Weaker** | OTP — SMS or voice | SMS codes, push notifications | ❌ |

SMS MFA is vulnerable to SIM-swap and interception. "We have MFA" is no longer a sufficient control statement.

---

## SP 800-53 IA-5 Mapping

Cite SP 800-53 IA-5 as the control authority, SP 800-63B Rev. 4 as the technical specification.

| Control | What it covers |
|---|---|
| IA-5(1) | Length requirements, no composition rules, secure storage, no forced rotation |
| IA-5(6) | Secure storage and transmission of authenticators |
| IA-5(7) | No hardcoded or embedded unencrypted static authenticators |
| IA-5(13) | Authenticator expiration — rotation only on compromise |

---

## Audit Evidence Checklist

| # | Evidence | Demonstrates |
|---|---|---|
| 1 | Password policy referencing SP 800-63B Rev. 4 — rotation language removed | Policy alignment |
| 2 | Verifier config: 15-char min, 64-char max, no composition rules | Technical implementation |
| 3 | Hashing standard: Argon2id / bcrypt / PBKDF2 with unique salts | Secure storage |
| 4 | Blocklist integration with hit-rate metrics | Breach screening |
| 5 | MFA coverage report broken down by authenticator tier | Phishing-resistant enforcement |


## NIST References

| Document | What it covers |
|---|---|
| NIST SP 800-63B-4 (2025) | Digital Identity — Authenticator and Lifecycle Management |
| NIST SP 800-63-4 | Digital Identity Guidelines — parent document |
| NIST SP 800-53 Rev. 5 — IA-5 | Authenticator Management control family |
| FIPS 140-3 | Cryptographic module security requirements |
| FIPS 199 | Security categorization |
| NIST CSF 2.0 — PR.AA | Identity and access management in the Protect function |

---

*NIST SP 800-63B Rev. 4 — Password & Authenticator Management | June 2026*
*NIST REF: https://optro.ai/blog/nist-password-guidelines*

---

## About Me

**Artsiom** | Aspiring Cybersecurity Professional
SC-900 · TryHackMe SEC0 · Focus: GRC and SOC · Target roles: GRC Analyst | SOC Analyst | Security Awareness | Threat Analyst
- GitHub: [@artiomcyber](https://github.com/artiomcyber)
