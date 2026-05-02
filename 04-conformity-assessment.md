# 04 — Conformity Assessment: Pre-Deployment Checklist
 
This checklist provides a structured pre-deployment gate for high-risk AI systems in retail banking. It is designed to be completed by the model risk function (second line) before any new model version enters production.
 
All items must be completed and approved before deployment. Items marked BLOCKING must be resolved — they cannot be accepted as exceptions.
 
---
 
## How to use this checklist
 
1. Complete one checklist per model version being deployed
2. Each item must have a named owner and a status
3. BLOCKING items with status "fail" prevent deployment
4. All items must be retained as part of the technical documentation (Article 11, Annex IV)
5. The completed checklist must be approved by the second-line model risk owner before go-live
---
 
## Section A — Classification and scope
 
| # | Item | Type | Status | Owner | Evidence |
|---|------|------|--------|-------|----------|
| A1 | EU AI Act risk classification confirmed and documented | BLOCKING | | | |
| A2 | Annex III reference recorded | BLOCKING | | | |
| A3 | Intended purpose and deployment scope documented | BLOCKING | | | |
| A4 | Jurisdictions of deployment confirmed | Required | | | |
| A5 | Classification reviewed by second-line owner | BLOCKING | | | |
 
---
 
## Section B — Data governance
 
| # | Item | Type | Status | Owner | Evidence |
|---|------|------|--------|-------|----------|
| B1 | Data card completed for all training datasets | BLOCKING | | | |
| B2 | Data provenance documented (source, collection method, date range) | BLOCKING | | | |
| B3 | Bias assessment completed against defined methodology | BLOCKING | | | |
| B4 | Bias assessment results reviewed by model risk | BLOCKING | | | |
| B5 | Where bias identified: documented decision and mitigation in place | BLOCKING | | | |
| B6 | Data quality rules defined for all material input features | Required | | | |
| B7 | Training data confirmed distinct from test/validation data | BLOCKING | | | |
| B8 | GDPR Article 5 compliance confirmed for personal data in training set | BLOCKING | | | |
 
---
 
## Section C — Model documentation
 
| # | Item | Type | Status | Owner | Evidence |
|---|------|------|--------|-------|----------|
| C1 | Model card completed covering all Annex IV elements | BLOCKING | | | |
| C2 | Model architecture documented | Required | | | |
| C3 | Training methodology documented | Required | | | |
| C4 | Performance metrics documented (accuracy, precision, recall, F1, AUC) | BLOCKING | | | |
| C5 | Known limitations documented | BLOCKING | | | |
| C6 | Explainability approach documented | Required | | | |
| C7 | Version history complete and accurate | Required | | | |
 
---
 
## Section D — Testing and validation
 
| # | Item | Type | Status | Owner | Evidence |
|---|------|------|--------|-------|----------|
| D1 | Pre-deployment test protocol completed | BLOCKING | | | |
| D2 | All performance metrics met defined pass/fail thresholds | BLOCKING | | | |
| D3 | Adversarial robustness test completed | Required | | | |
| D4 | Fairness / demographic parity test completed | BLOCKING | | | |
| D5 | Test dataset confirmed as held-out (not used in training) | BLOCKING | | | |
| D6 | Independent model validation completed (if annual cycle due) | Required | | | |
| D7 | Second-line sign-off on test results obtained | BLOCKING | | | |
 
---
 
## Section E — Supply chain and third-party risk
 
| # | Item | Type | Status | Owner | Evidence |
|---|------|------|--------|-------|----------|
| E1 | Supply chain trust map completed for this model version | BLOCKING | | | |
| E2 | All third-party providers identified and assessed | BLOCKING | | | |
| E3 | Contracts reviewed for AI-specific obligations | Required | | | |
| E4 | Audit rights confirmed for each material provider | Required | | | |
| E5 | Provider conformity evidence obtained (SOC 2 / ISO 42001 / equivalent) | Required | | | |
| E6 | Foundation model version confirmed and documented | Required | | | |
| E7 | Training data vendor obligations assessed under GDPR Article 28 | Required | | | |
| E8 | Open trust gaps assessed and risk-accepted or remediated | BLOCKING | | | |
 
---
 
## Section F — Access control
 
| # | Item | Type | Status | Owner | Evidence |
|---|------|------|--------|-------|----------|
| F1 | Privileged access policy confirmed for this model version | Required | | | |
| F2 | Access provisioning completed for all authorised users | Required | | | |
| F3 | API key inventory updated for new model version | Required | | | |
| F4 | Previous model version access revoked or scoped correctly | Required | | | |
| F5 | SoD confirmed: no individual provisions and reviews their own access | BLOCKING | | | |
| F6 | PAM controls (session recording, MFA, rotation) confirmed active | Required | | | |
 
---
 
## Section G — Human oversight
 
| # | Item | Type | Status | Owner | Evidence |
|---|------|------|--------|-------|----------|
| G1 | Human override mechanism documented and tested | BLOCKING | | | |
| G2 | Explainability output verified for this model version | BLOCKING | | | |
| G3 | Explainability output accessible to reviewing staff without specialist knowledge | Required | | | |
| G4 | Human oversight training updated for this model version | Required | | | |
| G5 | All active reviewers confirmed as trained | BLOCKING | | | |
 
---
 
## Section H — Change management
 
| # | Item | Type | Status | Owner | Evidence |
|---|------|------|--------|-------|----------|
| H1 | Change record raised and approved prior to deployment | BLOCKING | | | |
| H2 | Risk assessment completed within change record | BLOCKING | | | |
| H3 | Rollback plan documented and tested | Required | | | |
| H4 | Post-implementation review scheduled | Required | | | |
| H5 | Deployment window confirmed with operations team | Required | | | |
 
---
 
## Section I — Monitoring and incident response
 
| # | Item | Type | Status | Owner | Evidence |
|---|------|------|--------|-------|----------|
| I1 | Post-deployment monitoring framework active for this model version | BLOCKING | | | |
| I2 | Monitoring thresholds confirmed and appropriate for new version | Required | | | |
| I3 | Alert routing confirmed and tested | Required | | | |
| I4 | Serious incident procedure reviewed and current | Required | | | |
| I5 | Incident log updated to include new model version scope | Required | | | |
 
---
 
## Approval
 
| Role | Name | Date | Signature / approval reference |
|------|------|------|-------------------------------|
| Model Risk Owner (second line) | | | |
| Business Owner | | | |
| CISO / Security representative | | | |
| Compliance / EU AI Act lead | | | |
 
**Deployment approved:** Yes / No
 
**If no — blocking items outstanding:**
 
| Item reference | Description | Owner | Resolution required by |
|----------------|-------------|-------|------------------------|
| | | | |
 
---
 
*Part of the A-GRC: AI Governance & Risk Controller framework*
*Author: Layla Bhatti — github.com/lbhatti-risk*
 
