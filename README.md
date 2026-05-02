# A-GRC: AI Governance & Risk Controller
 
**A structured readiness assessment framework for high-risk AI systems in financial services.**
 
Focused on AI/ML fraud detection in retail banking, mapped against the EU AI Act, NIST AI RMF, and ISO/IEC 42001. Built with a transitive trust / AI supply chain risk lens.
 
> All content is synthetic and methodology-based. Nothing in this repository originates from a live client engagement or proprietary system.
> *The views expressed are my own and do not represent my employer.*
 
---
 
## Why this exists
 
Almost every retail bank now uses a third-party AI or ML model for fraud detection. The model flags a transaction. The bank acts on it. The customer is affected.
 
The EU AI Act classifies fraud detection systems in banking as **high-risk AI** under Annex III. That means they are subject to mandatory conformity assessments, transparency obligations, human oversight requirements, and supply chain accountability — before deployment, not after.
 
Most GRC teams are not ready for this. The challenge isn't understanding the regulation. It's translating it into a control framework that an auditor can test, a risk manager can own, and an engineer can implement.
 
That's what A-GRC is for.
 
---
 
## The transitive trust problem
 
Modern fraud detection models are rarely built in-house. A bank typically:
 
1. Calls an API from a third-party model provider (e.g. AWS Bedrock, Azure OpenAI, a specialist fintech)
2. That provider may use a foundation model trained by a fourth party (e.g. Anthropic, OpenAI, Meta)
3. That foundation model was trained on data from a fifth party (web scrapes, licensed datasets, third-party data vendors)
When the bank says "we trust our fraud detection model," what they're actually saying is: *we trust the vendor, who trusts the foundation model provider, who trusts the training data source.*
 
This is **transitive trust** — and it's the primary governance gap in AI supply chains right now. The EU AI Act's supply chain provisions (Articles 25, 28, 55) are attempting to address this. Most banks haven't worked out how.
 
A-GRC makes transitive trust auditable.
 
---
 
## Repository structure
 
```
a-grc/
├── README.md                          ← This file
├── framework/
│   ├── 01-system-classification.md   ← EU AI Act risk classification
│   ├── 02-supply-chain-mapping.md    ← Transitive trust & TPRM
│   ├── 03-control-requirements.md    ← Control domains & requirements
│   ├── 04-conformity-assessment.md   ← Pre-deployment checklist
│   └── 05-ongoing-monitoring.md      ← Post-deployment controls
├── schemas/
│   ├── assessment-schema.yaml        ← Assessment-as-Code schema
│   ├── control-register.yaml         ← Control register schema
│   └── supply-chain-map.json         ← Supply chain trust map schema
├── templates/
│   ├── risk-assessment-template.md   ← Completed example (synthetic)
│   └── supply-chain-register.md      ← Vendor trust register example
└── mappings/
    └── eu-ai-act-nist-iso42001-crosswalk.md ← Framework crosswalk
```
 
---
 
## Framework scope
 
| Dimension | Scope |
|-----------|-------|
| AI use case | Fraud detection and transaction monitoring in retail banking |
| Regulatory trigger | EU AI Act Annex III — high-risk AI system |
| Primary frameworks | EU AI Act, NIST AI RMF (Govern/Map/Measure/Manage), ISO/IEC 42001 |
| Supply chain | Third-party model providers, foundation model vendors, training data sources |
| Control domains | Data governance, model governance, access control, change management, human oversight, incident response |
| Tools referenced | CyberArk (model access), ServiceNow (model change management), Veza (identity governance) |
 
---
 
## Who this is for
 
- **Risk and audit teams** building readiness assessments for AI systems ahead of EU AI Act enforcement
- **GRC analysts** designing control frameworks for AI governance programmes
- **Internal auditors** scoping AI model audits under the Three Lines Model
- **Regulators and compliance teams** assessing third-party AI providers against supply chain obligations
---
 
## Author
 
Layla Bhatti — Digital Audit & IT Risk | [linkedin.com/in/layla-b-3470a31b8](https://linkedin.com/in/layla-b-3470a31b8) | [github.com/lbhatti-risk](https://github.com/lbhatti-risk)
