# 02 — Supply Chain Mapping: Transitive Trust in AI Systems
 
The EU AI Act creates a chain of accountability across the AI supply chain. Understanding that chain — and the trust that flows through it — is the starting point for any governance programme.
 
---
 
## The transitive trust problem
 
When a bank deploys a fraud detection model, it rarely builds it from scratch. The typical architecture looks like this:
 
```
Bank (Deployer)
    │
    └── Third-Party Model Provider (e.g. specialist fraud AI vendor)
            │
            └── Foundation Model / API Provider (e.g. AWS Bedrock, Azure OpenAI)
                    │
                    └── Training Data Vendor (e.g. data broker, web scrape aggregator)
```
 
At each layer, trust is transferred but not verified. The bank trusts the vendor. The vendor trusts the foundation model provider. The foundation model provider trusts the training data source.
 
If the training data contains biased samples — over-representing certain customer demographics as fraudulent — that bias propagates through every layer. The bank's fraud model discriminates. The bank is liable under the EU AI Act. But the root cause is four layers removed from the bank's direct control.
 
This is transitive trust risk. Article 25 and Article 28 of the EU AI Act attempt to address it by imposing supply chain obligations — but the practical compliance work falls on the bank's risk and governance teams.
 
---
 
## Supply chain mapping methodology
 
### Step 1 — Identify all AI components
 
List every component of the fraud detection system that involves an AI or ML model, including:
- The primary fraud scoring model
- Any pre-processing models (e.g. entity resolution, transaction enrichment)
- Any post-processing models (e.g. explainability layers, alert ranking)
- Any foundation model APIs called at inference time
### Step 2 — Map the provider chain
 
For each component, identify:
 
| Layer | Entity | Role under EU AI Act | Contractual relationship |
|-------|--------|---------------------|--------------------------|
| 1 | Bank | Deployer (Article 3(4)) | Internal |
| 2 | Fraud AI vendor | Provider (Article 3(3)) or Distributor (Article 3(7)) | Direct contract |
| 3 | Foundation model provider | GPAI model provider (Article 51) | Vendor's contract (indirect) |
| 4 | Training data vendor | Outside EU AI Act scope — but GDPR Article 28 applies | Unknown to bank |
 
### Step 3 — Assess trust at each layer
 
For each provider relationship, assess:
 
**Contractual controls**
- Does the contract include AI-specific obligations (accuracy, bias testing, incident notification)?
- Does the contract permit audit rights over the AI component?
- Is there a data processing agreement covering training data?
**Technical controls**
- Can the bank inspect the model's behaviour (explainability, feature importance)?
- Is the model versioned and change-controlled?
- Is the model's training data documented (data card, model card)?
**Governance controls**
- Does the provider hold an EU AI Act conformity certificate or equivalent?
- Is the provider subject to a SOC 2 Type II, ISO 42001, or equivalent audit?
- Who has privileged access to the model weights, APIs, and inference infrastructure?
### Step 4 — Identify trust gaps
 
A trust gap exists where:
- A contractual control is absent (e.g. no audit rights over a sub-processor)
- A technical control is unavailable (e.g. foundation model is a black box with no explainability API)
- A governance control is unverified (e.g. provider claims ISO 42001 compliance but no certificate exists)
---
 
## CyberArk and access governance in the AI supply chain
 
Privileged access to AI systems is a critical and frequently overlooked control. The following access vectors require governance:
 
| Access vector | Risk | Control |
|---------------|------|---------|
| Model weights / parameters | Insider threat; model poisoning | CyberArk PAM; MFA; session recording |
| Training data pipeline | Data poisoning; bias injection | Access provisioning review (Veza/SailPoint); segregation of duties |
| Inference API keys | Unauthorised queries; data exfiltration | API key rotation; rate limiting; audit logging |
| Model monitoring dashboards | Suppression of adverse performance signals | Role-based access; read-only for business users |
| Retraining pipeline | Model drift manipulation | Change management via ServiceNow; dual approval |
 
The PAM controls for AI systems should follow the same framework as CyberArk ITGC controls — privileged users, session recording, rotation schedules — but applied to AI-specific access vectors rather than traditional server infrastructure.
 
---
 
## ServiceNow: model change management
 
Every material change to a fraud detection model must be treated as a change management event, equivalent to a production code change. This includes:
 
- Retraining on new data (even if model architecture is unchanged)
- Updating hyperparameters or decision thresholds
- Changing input features
- Switching foundation model versions (e.g. upgrading from GPT-4 to GPT-4o)
- Changing a third-party provider
**ServiceNow change record requirements for AI model changes:**
 
| Field | Requirement |
|-------|-------------|
| Change type | Standard / Normal / Emergency |
| Description | Model version, change type, expected impact on fraud detection rate |
| Risk assessment | Fairness impact, performance degradation risk, regulatory notification trigger |
| Approvers | Model Risk (second line), Business Owner, CISO (for security-material changes) |
| Testing evidence | Pre/post performance metrics, bias test results, A/B test output |
| Rollback plan | Previous model version; rollback trigger conditions |
| Post-implementation review | 30-day performance monitoring; anomaly thresholds |
 
A model retrain that is not logged as a change event is an ITGC exception — the same as a code deployment without change approval.
 
---
 
## Supply chain trust register template
 
| Provider | Layer | EU AI Act role | Contract reviewed | Audit rights | Model card / data card | Last assessed | Trust gap identified | Gap owner |
|----------|-------|----------------|-------------------|--------------|------------------------|---------------|----------------------|-----------|
| [Vendor A] | 2 | Provider | Yes / No | Yes / No | Yes / No | [Date] | Yes / No | [Name] |
| [Vendor B] | 3 | GPAI provider | Yes / No | Yes / No | Yes / No | [Date] | Yes / No | [Name] |
| [Data broker] | 4 | Outside scope | Yes / No | Yes / No | N/A | [Date] | Yes / No | [Name] |
 
---
 
*Part of the A-GRC: AI Governance & Risk Controller framework*
*Author: Layla Bhatti — github.com/lbhatti-risk*
