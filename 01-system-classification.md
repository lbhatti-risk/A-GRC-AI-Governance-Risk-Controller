# 01 — System Classification: EU AI Act Risk Tier
 
Before any control assessment begins, the AI system must be correctly classified under the EU AI Act. Misclassification is itself a governance failure — it determines the entire compliance obligation.
 
---
 
## Classification decision tree
 
```
Is the system an AI system as defined under Article 3(1)?
│
├── No → EU AI Act does not apply
│
└── Yes
    │
    ├── Does it pose an unacceptable risk? (Article 5)
    │   ├── Yes → PROHIBITED. Do not deploy.
    │   └── No → Continue
    │
    ├── Is it a General Purpose AI (GPAI) model? (Article 51)
    │   ├── Yes → GPAI obligations apply (transparency, copyright, systemic risk)
    │   └── No → Continue
    │
    ├── Does it fall under Annex III high-risk categories?
    │   ├── Yes → HIGH-RISK obligations apply (Articles 9–15, 17, 26, 28)
    │   └── No → Continue
    │
    ├── Does it interact with humans without disclosure? (Article 50)
    │   ├── Yes → LIMITED RISK transparency obligations apply
    │   └── No → MINIMAL RISK — no mandatory requirements
```
 
---
 
## Fraud detection classification rationale
 
**Classification: HIGH-RISK — Annex III, Category 5(b)**
 
Annex III, point 5 covers AI systems used in the area of access to and enjoyment of essential private services. Credit, insurance, and banking services are explicitly listed.
 
A fraud detection model in retail banking falls under this category because:
 
- It makes or materially influences decisions about whether a customer can access their account or complete a transaction
- A false positive (legitimate transaction flagged as fraud) denies the customer access to a private financial service
- A false negative (fraud not detected) causes material harm to the customer and the institution
- The decision is largely automated, with limited human review in real-time transaction contexts
**Consequence of high-risk classification:**
 
The deploying bank becomes a **provider** or **deployer** under the EU AI Act with mandatory obligations including conformity assessment (Article 43), quality management system (Article 17), technical documentation (Article 11), human oversight (Article 14), and accuracy/robustness requirements (Article 15).
 
If the bank uses a third-party model, the third-party provider also carries obligations under Article 25 (obligations of distributors) and Article 28 (third-party providers becoming providers).
 
---
 
## Classification register
 
| Field | Value |
|-------|-------|
| System name | [Fraud Detection Model — synthetic placeholder] |
| System version | [v_X.X] |
| Classification date | [Date] |
| Classification owner | [Role] |
| Risk tier | HIGH-RISK |
| Annex III reference | Category 5(b) — access to private services |
| Review trigger | Model version change, regulatory update, significant performance deviation |
| Next review date | [Date] |
 
---
 
## Classification governance
 
**Who owns this decision?**
 
The classification decision must be owned by a named individual in the second line of defence — typically the Chief Risk Officer, Head of Model Risk, or equivalent. It must not be delegated to the model developer or business line.
 
**What happens if classification changes?**
 
Any change to the model's purpose, scope, or deployment context that could affect its risk tier must trigger a reclassification review. This includes:
- Expanding the model to new customer segments
- Changing the third-party provider
- Adding new input features (especially biometric or behavioural data)
- Deploying in a new jurisdiction
**Audit trail requirement:**
 
The classification decision, rationale, and approver must be documented and retained for the life of the system plus ten years (Article 18).
 
---
 
*Part of the A-GRC: AI Governance & Risk Controller framework*
*Author: Layla Bhatti — github.com/lbhatti-risk*
