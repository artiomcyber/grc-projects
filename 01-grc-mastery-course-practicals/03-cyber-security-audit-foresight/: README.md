# 03 — Cyber Security Audit: Foresight Group Holdings Limited

## About Me

**Artsiom** | Aspiring Cybersecurity Professional  
I am an aspiring cybersecurity professional holding SC-900 (Microsoft Security, Compliance & Identity Fundamentals) and TryHackMe SEC0 certifications, actively expanding my hands-on experience through industry simulations, labs, and real-world projects. My focus areas include Governance, Risk & Compliance (GRC) and Security Operations (SOC) — working towards a career where I can help organizations build resilient security programs and respond effectively to evolving cyber threats.
- GitHub: [@artiomcyber](https://github.com/artiomcyber)
- Certifications: SC-900 | SEC0
- Target Roles: SOC Analyst | GRC Analyst | Security Awareness | Threat Analyst

---

## Overview

| Field | Details |
|---|---|
| **Course** | GRC Mastery |
| **Module** | Cyber Security Audit |
| **Case Study** | Foresight Group Holdings Limited — FY24 Annual Report (Risks Section) |
| **My Role** | Cyber Security Consultant |
| **Completed** | June 2026 |

**Scenario:** I was given a real excerpt from Foresight Group's publicly available FY24 Annual Report and hired as a Cyber Security Consultant to analyze how they manage cyber risk, how the Three Lines of Defence model works inside their organization, and what their biggest risks actually are.

## Files in This Folder

| File | Description |
|---|---|
| `README.md` | This write-up — full analysis, findings, and frameworks |
| [`risk_report_foresight.pdf`](./risk_report_foresight.pdf) | Source material — excerpt from Foresight Group Holdings Limited FY24 Annual Report (publicly available) |

---

## Who Is Foresight Group?

Foresight Group Holdings Limited is a UK investment firm listed on the London Stock Exchange. They manage money on behalf of clients — putting it into things like sustainable forestry, infrastructure, and private equity. They're regulated by the FCA (the UK's main financial watchdog), which means they have to follow strict rules around risk management, data protection, and financial crime.

This is a real company. The risks, frameworks, and governance structures in this case study reflect how a regulated financial organization actually operates — not a made-up scenario.

---

## How They Manage Risk

### The System — Three Lines of Defence (3LOD)

Foresight uses the 3LOD model to make sure risk is owned, monitored, and independently checked at every level of the organization. Each line has a different job:

| Line | Who | What They Actually Do |
|---|---|---|
| **1st Line** | Business units and teams | Own the risks day-to-day — follow policies, implement controls, report incidents, feed data into the risk system |
| **2nd Line** | Risk & Compliance team | Watch over the 1st line — score risks, build the risk register, write policies, monitor controls, report to the Risk Committee monthly |
| **3rd Line** | External assurance / auditors | Independent — verify the whole framework is actually working, challenge the Risk Committee, report to the Board |

Above all three lines sits the governance chain:  
**Board → Executive Committee → Members Board → Firm Risk Committee → Risk & Compliance → Business Units**

The Board is ultimately accountable. The Audit & Risk Committee gets quarterly reports on the full risk profile.

### How They Score Risk — RCSA

They use a process called **Risk and Control Self-Assessment (RCSA)**. Each team assesses their own risks, scores them before and after controls, and feeds the data up to the Risk function. The Risk Committee then reviews everything monthly, tracks incidents and breaches, and decides whether controls need improving.

### Risk Appetite

Foresight has a formal **Risk Appetite Statement** — a written document that says exactly how much risk they're willing to accept in each category. It gets reviewed and approved by the Board every year. They use **Early Warning Indicators (EWIs)** to flag when they're getting close to their limits before something actually goes wrong.

---

## Top 10 Risks

These were assessed as of 31 March 2024. The Risk Committee debates them monthly.

### Principal Risks — Ongoing, Core Business Risks

| Risk | What It Means Simply | Trend | Key Controls |
|---|---|---|---|
| **Cyber / Info Security** | Hackers, phishing, ransomware — could steal client data or cause massive fines | ↑ Increasing | Firewalls, IDS, pen testing, phishing simulations, training, encryption |
| **Macro-Economic Conditions** | Inflation, interest rates, geopolitical instability hurts their investments | → No change | Portfolio diversification, active management, hard/soft risk limits |
| **Third-Party Risk** | A supplier gets hacked or fails — and Foresight gets dragged down with them | → No change | Vendor evaluation, IT security assessments, annual due diligence |
| **Sustainability Risk** | ESG regulations changing fast — greenwashing accusations could destroy reputation | ↑ Increasing | Climate due diligence, sustainability policies, compliance monitoring |
| **Regulatory Compliance** | FCA rules keep changing — non-compliance means fines and reputational damage | → No change | Compliance programmes, regulatory body engagement, legal consultations |
| **Resilience Risk** | Tech failures, disasters, or cyberattacks knock systems offline | ↑ Trending up | Redundancy systems, Business Continuity Plan, Disaster Recovery Plan |

### Emerging Risk — New and Growing

| Risk | What It Means Simply | Trend | Key Controls |
|---|---|---|---|
| **Geopolitical Risk** | Wars, sanctions, political instability in regions where they invest | ↑ Increasing | Geopolitical risk assessment, contingency plans, market diversification |

### Evolving Risks — Changing in Nature

| Risk | Trend | Notes |
|---|---|---|
| **Data & Records Management** | ↓ Decreasing | Improving — governance frameworks and backup systems being strengthened |
| **Conduct & Culture** | → No change | Staff ethics, insider trading risk — managed through code of conduct and regular audits |
| **Human Capital** | → No change | Losing key people, skills gaps — addressed through succession planning |

---

## Cyber Risk — Closer Look

Cyber is ranked **#1** and is a **standing agenda item** at every Risk Committee meeting. That's significant — it means this isn't just an IT problem. It's a business problem that reaches the Board.

### Why It's Particularly Dangerous Right Now

Foresight explicitly called out in their FY24 report that **AI tools are making phishing emails much harder to detect.** Attackers are using AI to write more convincing emails, which means traditional awareness training isn't enough on its own. They responded by running regular **phishing simulation tests** — test emails sent to staff to see who falls for them, with targeted training for those who do.

Supply chain attacks are also flagged as a growing threat. Rather than attacking Foresight directly, hackers compromise a smaller vendor and use that as a bridge in. Foresight's response: every third-party supplier now goes through a full **IT Security Assessment** as part of onboarding, and the results feed into their Third-Party Risk Assessment.

### Controls in Place

| Control | Purpose |
|---|---|
| Firewalls + Intrusion Detection Systems | Perimeter defence and real-time threat detection |
| Access controls + authentication | Limit who can access what, and how |
| Encryption + data protection | Protect data in transit and at rest |
| Security awareness training | Annual training covering the latest phishing and attack techniques |
| Phishing simulation tests | Regular fake phishing emails — those who click get targeted re-training |
| Penetration testing | Simulated cyberattacks on their own systems to find weaknesses first |
| Escalation + incident response programme | Clear process for what happens when an incident occurs |
| IT Security Assessment in vendor onboarding | Cyber evaluated for every third party before engagement |
| Board and Risk Committee oversight | Regular cyber updates reach senior leadership and the Board |

---

## Financial Crime Framework

Foresight manages financial crime risk (money laundering, fraud, sanctions, market abuse) through a framework built on **5 pillars** — all running across the three lines of defence:

| Pillar | What It Does |
|---|---|
| **Governance** | MLRO (Money Laundering Reporting Officer) leads oversight — Compliance meets monthly |
| **Risk Assessment** | Annual risk assessment per regulated entity — inherent and residual risk scored |
| **Due Diligence & KYC** | Know Your Customer checks on all clients and counterparties — enhanced for high-risk cases |
| **Training & Awareness** | Annual financial crime training + e-learning refreshers for all staff |
| **Monitoring & Surveillance** | Suspicious activity reported to MLRO — periodic reviews of FC controls |

Backed by: AML Policy, Anti-Bribery & Corruption Policy, Anti-Market Abuse Policy, Anti-Tax Evasion Policy, Record Keeping Policy.

---

## Frameworks and Regulations

| Framework / Regulation | What It Is | In Force |
|---|---|---|
| **FCA Rules** | UK Financial Conduct Authority — primary regulator | Ongoing |
| **MIFIDPRU / IFPR** | UK Investment Firms Prudential Regime — capital and liquidity requirements | Jan 2022 |
| **ICARA** | Internal Capital Adequacy and Risk Assessment — internal stress testing | Approved Oct 2023 |
| **TCFD** | Task Force on Climate-related Financial Disclosures — sustainability reporting | Ongoing |
| **TNFD** | Nature-related Financial Disclosures — voluntary now, expected to become mandatory | Monitoring |
| **Consumer Duty** | FCA standard raising consumer protection in retail financial services | Jul 2023 |
| **3LOD Model** | Three Lines of Defence — core governance framework | Core framework |
| **RCSA** | Risk and Control Self-Assessment — internal risk scoring process | Ongoing |
| **FSMA 2000 (Part 4A)** | Financial Services and Markets Act — governs FCA authorisation | Ongoing |

---

## Key Findings

**1. Cyber risk is treated as a Board-level issue, not just an IT problem.**  
It sits on the Risk Committee agenda every single month and flows up to the Board with regular updates. That's mature cyber governance — most organizations still treat it as an IT department concern.

**2. The 3LOD model has clear separation of duties.**  
Each line genuinely does something different. The Risk & Compliance function (2nd line) doesn't just write policies — they actively score risks, maintain the risk register, and challenge the 1st line. That only works if accountability is explicit, which it is here.

**3. AI-enhanced phishing is recognized as a real, present threat.**  
Foresight's own FY24 report directly calls out AI's impact on phishing quality. They're not waiting for it to become a problem — they're already responding with simulation testing and an escalation programme.

**4. Supply chain risk is directly connected to cyber.**  
Third-party compromise is identified as a realistic attack vector. IT security due diligence on every vendor is a control they actually enforce, not just document in a policy.

**5. Risk appetite is documented and Board-approved.**  
This isn't just a concept — it's a formal statement reviewed annually. They use Early Warning Indicators to monitor proximity to limits in real time. That's proactive risk management.

**6. Financial crime and cyber risk frameworks are integrated.**  
Both use a risk-based approach, both operate across the 3LOD model, and both require annual assessments. This is integrated risk thinking — not siloed security functions working separately.

---

## What This Taught Me

Working through a real annual report made me to connect the GRC frameworks I've been learning to how they actually look inside a regulated financial services firm.

A few things stood out. The 3LOD model only works if each line genuinely stays in its lane. Here, the Risk & Compliance function doing active risk scoring (not just oversight) is a deliberate design choice that keeps risk management embedded in the business rather than sitting above it.

Risk appetite also stopped being an abstract concept. Seeing it documented formally, approved by the Board, and monitored with specific indicators made it click.

And on cyber specifically: technical controls matter, but governance matters just as much. Pen testing and firewalls are only part of the answer. Making sure the Board gets regular cyber briefings and that the Risk Committee treats it as a standing agenda item — that's what actually makes an organization resilient.

---

*Completed as part of the GRC Mastery Course — Cyber Security Audit module | June 2026*
