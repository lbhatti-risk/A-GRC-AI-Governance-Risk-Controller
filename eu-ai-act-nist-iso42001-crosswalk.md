# Framework Crosswalk: EU AI Act × NIST AI RMF × ISO/IEC 42001
 
This crosswalk maps the key obligations for high-risk AI systems (fraud detection, retail banking) across three frameworks. It is designed to help GRC teams avoid duplicating work across compliance programmes.
 
All three frameworks are relevant for UK/EU financial services firms deploying AI in 2025–2026.
 
---
 
## Framework overview
 
| Framework | Issuer | Scope | Legal status |
|-----------|--------|-------|--------------|
| EU AI Act | European Union | AI systems placed on EU market or affecting EU persons | Binding regulation — phased enforcement 2024–2027 |
| NIST AI RMF 1.0 | NIST (US) | Voluntary framework for managing AI risk | Voluntary — but referenced by FCA, PRA in AI guidance |
| ISO/IEC 42001:2023 | ISO | AI management system standard | Voluntary — certification available; referenced in EU AI Act conformity |
 
---
 
## Crosswalk table — high-risk AI (fraud detection)
 
| Control domain | EU AI Act obligation | NIST AI RMF function | ISO 42001 clause |
|----------------|---------------------|----------------------|------------------|
| **Risk classification** | Annex III classification; Article 6 | MAP 1.1 — Context established | Clause 4.1 — Understanding context |
| **Quality management system** | Article 17 — QMS required for providers | GOVERN 1.1 — Policies established | Clause 4.4 — AI MS and its processes |
| **Training data governance** | Article 10 — Data and data governance | MAP 2.1 — Scientific theory examined | Clause 8.4 — AI system development |
| **Training data bias** | Article 10(5) — Data examined for bias | MAP 5.1 — Likelihood of risks examined | Clause 8.4 — AI system development |
| **Technical documentation** | Article 11 + Annex IV | GOVERN 1.2 — Accountability established | Clause 7.5 — Documented information |
| **Transparency to deployers** | Article 13 — Transparency obligations | GOVERN 4.1 — Organisational teams committed | Clause 7.4 — Communication |
| **Human oversight — design** | Article 14 — Human oversight by design | MANAGE 4.1 — Response plans in place | Clause 8.6 — AI system operation |
| **Human oversight — training** | Article 26(6) — Deployer training obligation | GOVERN 5.1 — Organisational teams committed | Clause 7.2 — Competence |
| **Accuracy and robustness** | Article 15 — Accuracy, robustness, cybersecurity | MEASURE 2.2 — AI systems evaluated | Clause 8.5 — AI system verification |
| **Post-market monitoring** | Article 72 — Post-market monitoring | MEASURE 2.7 — AI system performance monitored | Clause 9.1 — Monitoring and measurement |
| **Incident reporting** | Article 73 — Serious incident reporting | MANAGE 2.4 — Incidents and errors responded to | Clause 10.1 — Nonconformity and corrective action |
| **Fundamental rights assessment** | Article 27 — FRIA for certain deployers | MAP 5.2 — Practices for AI risk management | Clause 6.1 — Actions to address risks |
| **Supply chain obligations** | Articles 25, 28 — Third-party obligations | GOVERN 6.1 — Policies for AI risk management | Clause 8.4 — AI system development |
| **Conformity assessment** | Article 43 — Conformity assessment | GOVERN 1.7 — Processes documented | Clause 9.2 — Internal audit |
| **Registration** | Article 49 — Registration in EU database | GOVERN 1.2 — Accountability established | Clause 4.4 |
| **Access control / PAM** | Article 15(5) — Cybersecurity measures | GOVERN 6.2 — Policies for AI risk extended | ISO 27001 A.5.15 (referenced) |
| **Change management** | Article 9(5) — Risk management ongoing | GOVERN 6.1 — Policies for AI risk management | Clause 8.3 — AI system design |
 
---
 
## Key differences between frameworks
 
**EU AI Act** is obligations-based and legally binding. It tells you *what* must be in place (conformity assessment, QMS, human oversight) but largely leaves the *how* to the organisation. Non-compliance carries fines up to €30m or 6% of global annual turnover.
 
**NIST AI RMF** is outcomes-based and voluntary. It tells you *how* to think about AI risk management across four functions (Govern, Map, Measure, Manage) without prescribing specific controls. It is the closest thing the industry has to a universal AI risk management methodology.
 
**ISO/IEC 42001** is process-based and auditable. It provides a management system structure (similar to ISO 27001) that organisations can certify against. An ISO 42001 certificate is likely to become an accepted conformity evidence mechanism under the EU AI Act for some use cases.
 
---
 
## Using this crosswalk
 
**For GRC teams building an AI governance programme:**
Start with NIST AI RMF to establish the conceptual structure. Map your existing controls against the EU AI Act obligations. Use ISO 42001 as the audit and evidence management layer.
 
**For auditors scoping an AI model audit:**
Use the EU AI Act column as the legal baseline. Use the NIST column to frame the risk assessment. Use ISO 42001 clauses to identify what documented evidence should exist.
 
**For third-party risk assessments:**
Assess AI vendors against their obligations under Articles 25 and 28 of the EU AI Act. Ask for ISO 42001 certification or SOC 2 Type II as evidence of control effectiveness.
 
---
 
*Part of the A-GRC: AI Governance & Risk Controller framework*
*Author: Layla Bhatti — github.com/lbhatti-risk*
