# ⚖️ Risk Assessment — Practical Exercise
### GRC Mastery Course | Exercise 02

![GRC](https://img.shields.io/badge/GRC-Mastery%20Course-2E86AB?style=for-the-badge)
![Topic](https://img.shields.io/badge/Topic-Risk%20Assessment-4B8BBE?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge)

---

## 📖 What is a Risk Assessment?

A risk assessment is a structured process for identifying what could go wrong, how likely it is, how bad it would be, and what to do about it. It is one of the most fundamental activities in GRC — you cannot protect something if you do not know what threatens it or how serious that threat is.

### Risk Score Formula

> **Risk Score = Likelihood × Impact**

Every risk gets two scores, multiplied together to produce a final rating.

---

## 📊 Risk Matrix

| | **Impact: Low (1)** | **Impact: Medium (2)** | **Impact: High (3)** |
|---|---|---|---|
| **Likelihood: Likely (3)** | 3 — LOW | 6 — HIGH | 9 — HIGH |
| **Likelihood: Possible (2)** | 2 — LOW | 4 — MEDIUM | 6 — HIGH |
| **Likelihood: Unlikely (1)** | 1 — LOW | 2 — LOW | 3 — LOW |

### Scale Definitions

**Likelihood:**
| Score | Rating | Meaning |
|-------|--------|---------|
| 3 | Likely | High chance of occurrence — has already happened |
| 2 | Possible | Moderate chance — may happen |
| 1 | Unlikely | Very rare — unlikely to occur |

**Impact:**
| Score | Rating | Meaning |
|-------|--------|---------|
| 3 | High | Significant financial loss — over $500K |
| 2 | Medium | Moderate financial loss — $100K to $499K |
| 1 | Low | Minor loss — under $100K |

**Risk Level:**
| Score | Level | Action Required |
|-------|-------|----------------|
| 6 – 9 | 🔴 HIGH | Unacceptable — immediate treatment required |
| 4 – 5 | 🟡 MEDIUM | Needs mitigation or justification |
| 1 – 3 | 🟢 LOW | Acceptable — monitor and review |

---

## 🔑 Risk Treatment Options

Once a risk is scored, the organisation must decide what to do with it:

| Option | Meaning | When to use |
|--------|---------|-------------|
| **Mitigate** | Implement controls to reduce likelihood or impact | Most common — HIGH and MEDIUM risks |
| **Accept** | Acknowledge the risk and do nothing | LOW risks within tolerance |
| **Transfer** | Shift the risk to a third party (e.g. insurance) | When cost of mitigation exceeds potential loss |
| **Avoid** | Stop the activity that creates the risk entirely | When risk is unacceptable and cannot be reduced |

---

## 🏢 Practical Assessment — Wayne Enterprises

**Company:** Wayne Enterprises
**Incident:** An employee deliberately leaked confidential financial data — including employee salaries — to a competitor
**Estimated Financial Loss:** $700,000

---

## 📋 Risk Register

| # | Risk | Likelihood | Impact | Score | Level | Treatment |
|---|------|-----------|--------|-------|-------|-----------|
| 1 | Employee deliberately leaked salary data to a competitor | Likely (3) | High (3) | **9** | 🔴 HIGH | Forensic investigation, revoke access, notify legal and HR immediately |
| 2 | No DLP controls — a second leak could happen undetected | Likely (3) | High (3) | **9** | 🔴 HIGH | Deploy DLP solution, block transfers to USB, personal email and cloud storage |
| 3 | Legal and regulatory exposure from the salary data breach | Likely (3) | High (3) | **9** | 🔴 HIGH | Engage legal counsel, notify affected employees, review data protection compliance |
| 4 | Competitor uses salary data to recruit key staff | Likely (3) | High (3) | **9** | 🔴 HIGH | Brief leadership, review compensation packages, monitor resignation patterns |
| 5 | Residual risk after compensating control reduces likelihood to 1 | Unlikely (1) | High (3) | **3** | 🟢 LOW | Maintain controls, monitor annually |

📎 [Download Full Risk Assessment (Excel)](https://github.com/artiomcyber/grc-projects/blob/main/02-risk-assessment-wayne-enterprises/Wayne_Enterprises_Risk_Assessment.xlsx?raw=true)

---

## ✅ Quiz Results

**Q1 — What is the risk score? (Assuming it has already occurred)**
- Likelihood: Likely (3) × Impact: High (3) = **9 → HIGH** ✅

**Q2 — Based on the risk score, Wayne Enterprises should:**
- **Propose immediate risk treatment** — score of 9 is HIGH, which means unacceptable and requires immediate action ✅

**Q3 — After a compensating control reduces Likelihood to 1, the risk becomes:**
- New score: 1 × 3 = **3 → LOW → Acceptable** ✅
- This demonstrates how a single well-implemented control can move a risk from unacceptable to acceptable

---

## 🧠 Key Takeaways

- A risk score alone does not tell you what to do — you need to match it to a risk appetite and decide on treatment
- Residual risk matters as much as inherent risk — controls only help if they actually reduce likelihood or impact
- An insider threat is particularly dangerous because the attacker already has legitimate access — detection and response matter as much as prevention
- $700,000 in financial loss classifies as High impact (over $500K) — which combined with a Likely likelihood produces the maximum score of 9

---

## 🚀 About Me

**Artsiom** | Aspiring Cybersecurity Professional

I am an aspiring cybersecurity professional holding SC-900 (Microsoft Security, Compliance & Identity Fundamentals) and TryHackMe SEC0 certifications, actively expanding my hands-on experience through industry simulations, labs, and real-world projects. My focus areas include Governance, Risk & Compliance (GRC) and Security Operations (SOC) — working towards a career where I can help organizations build resilient security programs and respond effectively to evolving cyber threats.

- 🐙 GitHub: [@artiomcyber](https://github.com/artiomcyber)
- 🏅 Certifications: SC-900 | SEC0
- 🎯 Target Roles: SOC Analyst | GRC Analyst | Security Awareness | Threat Analyst

---

*⚠️ Wayne Enterprises and all scenario details are fictional and used for educational purposes only.*
