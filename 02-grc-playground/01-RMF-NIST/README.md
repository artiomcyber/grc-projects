# CivicTrack Analytics — NIST RMF Implementation: Full Risk Management Lifecycle

## Overview

| Field | Details |
|---|---|
| **Scenario** | CivicTrack Analytics — AWS-hosted internal analytics platform |
| **Role** | GRC Engineer |
| **Framework** | NIST Risk Management Framework (RMF) |
| **Completed** | June 2026 |

Applied the full NIST RMF lifecycle for CivicTrack Analytics — prepare, categorize, select, implement, assess, authorize, and monitor. Each step produced structured artifacts: YAML configs, boundary maps, control mappings, assessment findings, and authorization decisions.

---

## What Is RMF and Why Does It Exist?

The **Risk Management Framework (RMF)** is a structured, repeatable process developed by NIST to manage security and privacy risk throughout the life of a system. It was originally built for US federal agencies but is now widely adopted across regulated industries, defense contractors, healthcare, and financial services.

**Why it exists:** Most security failures don't happen because organizations don't know security matters. They happen because security decisions are made reactively — build first, bolt on security later, scramble for evidence during audits.
**RMF is the process of making security decisions on purpose instead of by accident.**

**NIST references:**
- NIST SP 800-37 Rev. 2 — the core RMF document
- NIST SP 800-53 Rev. 5 — the security control catalogue
- NIST SP 800-53A Rev. 5 — how to assess controls
- NIST SP 800-53B — control baselines (Low / Moderate / High)
- NIST SP 800-60 Vol. 1 Rev. 1 — how to categorize information types
- NIST SP 800-137 — continuous monitoring
- NIST SP 800-160 — systems security engineering

---

## The Scenario: CivicTrack Analytics

CivicTrack Analytics is a cloud-hosted internal analytics platform used by government operations staff to manage incident case data, generate reports, and export analysis.

**System profile:**

| Attribute | Details |
|---|---|
| **Hosting** | AWS (cloud infrastructure) |
| **Users** | Internal staff only |
| **Functions** | Collect, store, report, export operational data |
| **Data handled** | Incident case notes, auth logs, uploaded data files, internal reports, exported analysis |

**Full system architecture:**

| Component | Type | Description |
|---|---|---|
| CivicTrack Web Application | In boundary | The interface users interact with |
| Application Server | In boundary | Processes user requests |
| Database | In boundary | Stores operational data |
| Object Storage | In boundary | Holds reports and uploaded files |
| Admin Access Node | In boundary | Privileged management path |
| Identity Provider (SSO) | Inherited service | Enterprise authentication — managed by another team |
| Logging Platform | Inherited service | Centralized log collection — managed by another team |
| External Reporting Tool | External system | Outside the boundary and outside direct system ownership |

---

## Step 1 — Prepare

**What this step does:** Set the foundation before doing anything else. Identify system owner, security lead, engineering contacts, hosting model, and dependencies. If skip this, every decision that follows lacks context.

**What I established for CivicTrack:**

- System owner and security lead identified
- Hosting model: AWS cloud
- User base: internal staff only
- Data types to be categorized: incident case notes, auth logs, uploaded files, internal reports, exported analysis
- Dependencies: inherited SSO and logging services

**Why this matters (NIST perspective):** NIST SP 800-37 Rev. 2 emphasizes that preparation is the most undervalued step. Organizations that skip it produce weak system security plans, inconsistent categorization, and control selections that don't match the actual risk. Preparation creates the shared understanding that makes every subsequent step coherent.

**Key artifact produced:**

```yaml
system_profile:
  system_name: CivicTrack Analytics
  hosting: AWS
  users: internal_staff
  owner: GRC Engineering
  data_types:
    - incident_case_notes
    - user_authentication_logs
    - uploaded_data_files
    - internal_operational_reports
    - exported_analysis_reports
```

---

## Step 2 — Categorize

**What this step does:** Determine the impact level of every information type the system handles, then assign the system an overall security categorization. This drives everything that comes next — wrong categorization means wrong controls.

**The CIA Triad — what you're actually scoring:**

| Pillar | Question | Example failure |
|---|---|---|
| **Confidentiality** | Can unauthorized people read this? | Case notes leaked to unauthorized users |
| **Integrity** | Can this data be changed without authorization? | Incident records altered without a trace |
| **Availability** | Can the system be reached when needed? | CivicTrack offline during an incident response |

**Impact levels (FIPS 199):**

| Level | What it means | Examples |
|---|---|---|
| **Low** | Limited adverse effects | Public info, low-sensitivity tools |
| **Moderate** | Serious operational disruption | Internal workflows, sensitive records |
| **High** | Severe mission or safety damage | Critical infrastructure, highly sensitive systems |

**CivicTrack data type analysis:**

| Data Type | Confidentiality | Integrity | Availability | Primary Concern |
|---|---|---|---|---|
| Incident case notes | **HIGH** | Moderate | Moderate | Unauthorized access exposes sensitive details and response patterns |
| User authentication logs | Moderate | Moderate | Low | Missing or altered logs reduce detection capability |
| Internal operational reports | Low | Moderate | Moderate | Tampering could mislead decisions |
| Uploaded data files | Low | Moderate | Low | Corruption or malicious files impact results |
| Exported analysis reports | Moderate | Low | Low | Unauthorized disclosure exposes operational context |

**High-water mark rule:** The system's overall categorization is set by the highest score across all data types and all three pillars. One HIGH score anywhere = the system is categorized HIGH for that pillar.

**CivicTrack overall categorization: MODERATE**

Incident case notes drive a HIGH confidentiality concern — but taken across all data types together, the system overall lands at **Moderate**, which determines the control baseline.

**Why this matters (NIST perspective):** NIST SP 800-60 provides a full mapping of information types to impact levels. Over-categorizing wastes resources on controls that aren't needed (drag). Under-categorizing leaves critical systems exposed (exposure). Getting it right is the foundation of proportionate security.

**Key artifact produced:**

```yaml
system_categorization:
  system_name: CivicTrack Analytics
  information_types:
    - type: incident_case_notes
      confidentiality: high
      integrity: moderate
      availability: moderate
    - type: user_authentication_logs
      confidentiality: moderate
      integrity: moderate
      availability: low
    - type: internal_operational_reports
      confidentiality: low
      integrity: moderate
      availability: moderate
    - type: uploaded_data_files
      confidentiality: low
      integrity: moderate
      availability: low
    - type: exported_analysis_reports
      confidentiality: moderate
      integrity: low
      availability: low
  overall_categorization: moderate
  high_water_mark_driver: incident_case_notes_confidentiality
```

---

## Step 3 — Define System Boundary

**What this step does:** Decide exactly what is inside your security and compliance responsibility, what is shared (inherited), and what is outside. Poorly defined boundaries are one of the most common reasons security assessments fail.

**Three categories:**

| Category | Meaning |
|---|---|
| **In System Boundary** | You directly own and secure it — must be documented, controlled, and assessed |
| **Inherited Service** | Shared service managed by another team — you use their controls but don't own them |
| **External System** | Connected but outside your boundary entirely — you have no control ownership |

**CivicTrack boundary classification:**

| Component | Classification | Reason |
|---|---|---|
| CivicTrack Web Application | In boundary | Core system component, directly managed |
| Application Server | In boundary | Core infrastructure, directly managed |
| Database | In boundary | Stores sensitive operational data, directly managed |
| Object Storage | In boundary | Holds reports and uploads, directly managed |
| Admin Access Node | In boundary | Privileged access path, must be secured and assessed |
| Identity Provider (SSO) | Inherited service | Enterprise identity — another team manages it |
| Logging Platform | Inherited service | Centralized logging — another team manages it |
| External Reporting Tool | External system | Outside the boundary and ownership chain |

**Why this matters (NIST perspective):** NIST SP 800-37 explicitly warns that boundary errors leave critical components unprotected, blur control ownership, and make audits chaotic. A logging service may sit outside the application code but still inside the system boundary — this is one of the most commonly missed components.

**Key artifact produced:**

```yaml
system_boundary:
  system_name: CivicTrack Analytics
  in_scope:
    - web_app
    - application_server
    - database
    - object_storage
    - admin_access_node
  inherited_services:
    - enterprise_sso
    - centralized_logging
  external_systems:
    - external_reporting_tool
```

---

## Step 4 — Select Security Controls

**What this step does:** Choose the right controls from the NIST SP 800-53 catalogue based on the system's categorization level. Then tailor them — keep, modify, or remove specific controls to fit the actual system context.

**Control types:**

| Type | What it is | Example |
|---|---|---|
| **Technical controls** | Built into systems and software | Multi-factor authentication |
| **Operational controls** | People and process-based | Incident response procedures |
| **Management controls** | Governance and policy | Security policy, risk assessments |

**The NIST SP 800-53 control families (key ones for CivicTrack):**

| Family | Code | What it covers |
|---|---|---|
| Access Control | AC | Who can access what resources |
| Identification & Authentication | IA | Proving identity, MFA enforcement |
| Audit & Accountability | AU | Logging, audit events, traceability |
| Configuration Management | CM | Secure settings, drift prevention |
| Incident Response | IR | What to do when something goes wrong |
| System & Communications Protection | SC | Encryption, network boundaries |

**Why these six for CivicTrack:**

- Incident case notes require **AC** and **IA** — strict access control and strong authentication
- Authentication logs require **AU** — logs must be captured, intact, and protected
- Configuration drift risks require **CM** — settings must be locked and monitored
- Vulnerability response needs **IR** — defined playbooks for coordinated action
- Data in transit and at rest needs **SC** — encryption throughout

**Baseline selected: Moderate**
The Moderate baseline from NIST SP 800-53B provides stronger protection + monitoring requirements. Higher than Low (basic safeguards), lower than High (extensive safeguards + strict ops).

**Control mapping artifact:**

```yaml
control_mapping:
  - risk: unauthorized_access
    control_family: IA
    control_example: IA-2 (Identification and Authentication)
  - risk: lack_of_audit_traceability
    control_family: AU
    control_example: AU-2 (Audit Events)
  - risk: insecure_baseline_drift
    control_family: CM
    control_example: CM-2 (Baseline Configuration)
  - risk: uncoordinated_vulnerability_response
    control_family: IR
    control_example: IR-4 (Incident Handling)
```

**What the course didn't show, but extra from NIST:**

NIST SP 800-53B specifies that for Moderate systems, the baseline isn't just a checklist — you're expected to **tailor** it. Tailoring means:
- **Scoping** — removing controls that don't apply (e.g. physical controls for a fully cloud system)
- **Compensating** — substituting a control with an equivalent when direct implementation isn't feasible
- **Supplementing** — adding controls beyond the baseline when the risk profile demands it

CivicTrack on AWS would likely scope out some physical protection controls (PE family) since AWS handles physical security, and rely on AWS's inherited controls for those.

---

## Step 5 — Implement Security Controls

**What this step does:** Actually turn the selected controls on in the real environment. A control that only exists on paper protects nothing.

**CivicTrack controls in the real system:**

| Control | How it's implemented | Evidence location |
|---|---|---|
| MFA (IA-2) | Identity provider enforces MFA at sign-in for all users | Identity provider configuration |
| Logging (AU-2) | Application forwards audit events to centralized logging platform | Logging platform records |
| Access Restriction (AC-2) | RBAC limits admin functions to specific roles | Role configuration / access control lists |
| Encryption (SC-28) | Data encrypted at rest in object storage and database | Infrastructure configuration |

**The config that matters:**

```yaml
security:
  mfa_required: true
  enforce_all_users: true
  allowed_methods:
    - password
    - otp
  rbac:
    admin_roles:
      - security_admin
      - platform_admin
  logging:
    destination: centralized-log-platform
    retention_days: 365
  data_protection:
    encryption_at_rest: true
```

**What evidence looks like:**
Evidence is proof that a control exists and operates. Assessors need real artifacts — not just a word for it:
- Configuration screenshots
- System logs and audit records
- Policies and procedures
- Pipeline outputs and test artifacts

**Why this matters (NIST perspective):** NIST SP 800-53A emphasizes that implemented controls must produce **verifiable evidence**. Claiming a control exists is not proof. The evidence chain — configuration → logs → screenshots → policy — is what gets verified during assessment.

---

## Step 6 — Assess Security Controls

**What this step does:** Verify that implemented controls actually work as intended. Controls can fail due to misconfiguration, drift, or process breakdown. Assessment checks reality, not documentation.

**Three assessment methods (NIST SP 800-53A):**

| Method | What it involves |
|---|---|
| **Examine** | Review configs, docs, and artifacts |
| **Interview** | Ask personnel how processes work in reality |
| **Test** | Validate with technical and procedural checks |

**The MFA gap exercise — what actually happened:**

The identity config file showed:
```yaml
authentication:
  mfa_required: true
  enforce_all_users: false   ← THIS IS THE PROBLEM
  allowed_methods:
    - password
    - otp
```

MFA was enabled in principle (`mfa_required: true`) but `enforce_all_users: false` meant any user could bypass it. This is exactly the kind of gap that only shows up when we read the actual config — not when we read the policy document.

**The fix:**
```yaml
authentication:
  mfa_required: true
  enforce_all_users: true    ← FIXED
  allowed_methods:
    - password
    - otp
  privileged_roles:
    - admin
    - security_admin
```

**Evidence matched to controls:**

| Control | Evidence Location |
|---|---|
| MFA enforced | Identity provider configuration |
| System logs captured | Logging platform records |
| Access privileges restricted | Role configuration / access control lists |

**What the course didn't show — extra from NIST:**

NIST SP 800-53A introduces the concept of **assessment objectives** — for each control, there are specific things an assessor must confirm. For IA-2 (MFA), the objectives include:
1. MFA is implemented for privileged accounts
2. MFA is implemented for non-privileged accounts accessing sensitive data
3. Replay-resistant authentication mechanisms are used
4. The system enforces MFA — not just offers it

The gap found in the exercise (enforce vs. offer) directly maps to objective #4. This is why assessors read configs, not just policies.

---

## Step 7 — Implement (Operational Controls)

**What operational controls look like:**

Some controls live in workflows and people, not just technology:

**Incident Response workflow:**
```
Detect event → Triage → Assign owner → Respond → Document lessons learned
```

**Continuous monitoring pipeline:**
```
System / Pipeline / Scanner / Logs → Telemetry → Monitoring Review → Action
```

---

## Step 8 — Authorize the System

**What this step does:** A responsible person — the Authorizing Official (AO) — reviews the full security package and formally accepts (or rejects) the residual risk. This is accountability in writing.

**The three authorization decisions:**

| Decision | When it's used |
|---|---|
| **Authorization to Operate (ATO)** | Controls implemented, risk acceptable, no critical vulnerabilities |
| **Authorization with Conditions** | Moderate findings exist, system can operate, but must fix issues on a defined timeline |
| **Denial of Authorization** | Critical controls missing, severe vulnerabilities, architecture unsafe |

**The authorization package (what the AO reviews):**

| Document | What it contains |
|---|---|
| **SSP** (System Security Plan) | System description and all implemented controls |
| **SAR** (Security Assessment Report) | Assessment findings and control effectiveness |
| **POA&M** (Plan of Action & Milestones) | Known weaknesses and remediation tracking |

**CivicTrack authorization decision:**

```yaml
authorization_decision:
  system: CivicTrack Analytics
  recommendation: ATO with Conditions
  residual_risk: Moderate
  required_actions:
    - Complete CM process hardening
    - Track findings in POA&M
  reviewer: Authorizing Official
```

Assessment showed authentication and logging are operational. Configuration management is still maturing. Two moderate findings remain open. Decision: **ATO with Conditions** — operate, fix the two open items on a defined timeline.

**Why this matters (NIST perspective):** Authorization does not mean zero risk. It means leadership has reviewed the risk, understands it, and formally accepts it. The signature creates personal accountability — if something goes wrong, someone owned that decision. This is what separates proper risk governance from just hoping nothing bad happens.

---

## Step 9 — Monitor the System

**What this step does:** Keep watching the system after authorization because systems change. A software update might break a setting. A role might change. A new vulnerability might appear. Monitoring catches these before they become incidents.

**What teams monitor continuously:**

| Area | What to watch |
|---|---|
| **Configuration State** | MFA still required? Privileged roles changed? |
| **Vulnerabilities** | New critical findings from scanners? |
| **Logging and Telemetry** | Audit events still flowing? |
| **Access and Identity** | Inactive privileged accounts removed? |
| **Infrastructure Changes** | Storage public exposure or firewall drift? |
| **Operational Processes** | Reviews and incident workflows still happening? |

**The regression exercise — what actually happened:**

After authorization, an identity settings update weakened MFA enforcement. The monitoring review caught it:

```yaml
# BEFORE (after the update broke it)
authentication:
  mfa_required: true
  enforce_all_users: false   ← regression introduced

# AFTER (fix applied)
authentication:
  mfa_required: true
  enforce_all_users: true    ← restored
```

A security regression is when a security control that was working correctly stops working due to a change. Continuous monitoring exists to detect these before attackers find them first.

**The monitoring pipeline:**
```
Observe → Detect changes → Evaluate impact → Respond → Continue monitoring
```

**Why this matters (NIST perspective):** NIST SP 800-137 defines continuous monitoring as an information security continuous monitoring (ISCM) strategy. The key insight is that authorization is a point-in-time decision about a system that will change. Without monitoring, approved systems quietly become insecure. Modern teams automate evidence collection through logs, scanners, CI/CD policy checks, and configuration drift detection — so monitoring is ongoing, not periodic.

---

## Full RMF Lifecycle Summary for CivicTrack

| Step | What Was Done | Key Output |
|---|---|---|
| **1. Prepare** | Identified system, users, data types, hosting model, dependencies | System profile artifact |
| **2. Categorize** | Scored all data types across CIA — system = Moderate | Categorization artifact |
| **3. Boundary** | Classified all components as in-scope, inherited, or external | Boundary artifact |
| **4. Select** | Chose Moderate baseline controls: AC, IA, AU, CM, IR, SC | Control mapping artifact |
| **5. Implement** | Turned controls on — MFA, logging, RBAC, encryption | Config artifacts + evidence |
| **6. Assess** | Found MFA bypass gap (`enforce_all_users: false`), fixed it | Assessment findings |
| **7. Authorize** | ATO with Conditions — 2 moderate findings tracked in POA&M | Authorization decision |
| **8. Monitor** | Caught MFA regression after identity update, restored compliance | Monitoring alert + fix |

---

## Key Findings

**1. RMF is a lifecycle, not a checklist.**
The goal is not to finish RMF. The goal is to manage risk throughout the life of the system. Authorization is not the end — it's the handoff to continuous monitoring.

**2. Categorization drives everything downstream.**
Wrong categorization = wrong baseline = wrong controls = wrong protection level. Getting this step right is the most important decision in the whole process. NIST SP 800-60 exists specifically to help make this consistent and defensible.

**3. Boundaries are where security programs silently fail.**
The most commonly forgotten components are logging services, admin jump boxes, and shared infrastructure. If it's not in the boundary, it doesn't get controlled, assessed, or evidenced. Boundary gaps show up during audits as control ownership failures.

**4. A control that only exists on paper protects nothing.**
Implementation means the control is running, configured correctly, and producing evidence. The MFA exercise proved this — `mfa_required: true` meant nothing while `enforce_all_users: false` sat underneath it. Assessors read configs, not policies.

**5. Authorization creates accountability, not certainty.**
The AO doesn't approve because the system is perfect. They approve because they understand the risk and are willing to accept it on behalf of the organization. That personal accountability is what makes the decision meaningful.

**6. Monitoring is the step most organizations skip.**
After the ATO is signed, attention moves to the next project. But systems change constantly — updates, new users, config drift, new vulnerabilities. NIST SP 800-137 treats continuous monitoring as a core program, not an afterthought. The regression exercise showed exactly how quickly a working control can silently break.

---

## NIST References — Beyond the Course

These are the actual documents behind everything covered in this mission:

| Document | What it covers | Why it matters here |
|---|---|---|
| **NIST SP 800-37 Rev. 2** | The full RMF process | Core framework — all 7 steps |
| **NIST SP 800-53 Rev. 5** | Security control catalogue | Where all controls come from |
| **NIST SP 800-53A Rev. 5** | Assessment procedures for each control | How assessors verify controls |
| **NIST SP 800-53B** | Control baselines (Low/Moderate/High) | What baseline to start from |
| **NIST SP 800-60 Vol. 1 Rev. 1** | Information type categorization | How to assign FIPS 199 impact levels |
| **FIPS 199** | Standards for security categorization | The official scoring standard |
| **FIPS 200** | Minimum security requirements | Minimum standards per categorization |
| **NIST SP 800-137** | Continuous monitoring | The ISCM strategy framework |
| **NIST SP 800-160** | Systems security engineering | Building security in from the start |

---

## What This Taught Me

Working through every step of RMF for a single system changed how I think about security work.

RMF is not a framework you learn — it's a discipline you apply. The difference shows in the details: why boundaries must be defined before controls are selected, why categorization drives every downstream decision, why an assessor reads the config file instead of the policy document.

The MFA exercise was the sharpest lesson. The policy said MFA was required, `mfa_required: true` was in the file — but `enforce_all_users: false` sat underneath it, giving every user a bypass path. That gap doesn't appear in a document review. It only surfaces when you inspect the actual configuration. That's the point of assessment.

The monitoring step reframed something I'd underestimated. Authorization is not the finish line — it's the handoff to continuous oversight. The regression exercise showed how fast a working control silently breaks after a routine update. Security posture decays. Monitoring is what keeps it honest.

---

*CivicTrack Analytics — NIST RMF Implementation | June 2026*

---

## About Me

**Artsiom** | Aspiring Cybersecurity Professional
I am an aspiring cybersecurity professional holding SC-900 (Microsoft Security, Compliance & Identity Fundamentals) and TryHackMe SEC0 certifications, actively expanding my hands-on experience through industry simulations, labs, and real-world projects. My focus areas include Governance, Risk & Compliance (GRC) and Security Operations (SOC) — working towards a career where I can help organizations build resilient security programs and respond effectively to evolving cyber threats.
- GitHub: [@artiomcyber](https://github.com/artiomcyber)
- Certifications: SC-900 | SEC0
- Target Roles: SOC Analyst | GRC Analyst | Security Awareness | Threat Analyst
