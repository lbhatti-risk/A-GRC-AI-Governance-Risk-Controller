# 05 — Ongoing Monitoring: Post-Deployment Controls
 
The EU AI Act does not end its obligations at deployment. Article 72 requires providers and deployers of high-risk AI systems to operate a post-market monitoring system. For retail banking fraud detection, this means continuous, structured oversight of model performance, data quality, access governance, and supply chain integrity.
 
This document defines the ongoing monitoring framework for a deployed fraud detection model.
 
---
 
## Monitoring cadence
 
| Monitoring type | Frequency | Owner | Escalation trigger |
|-----------------|-----------|-------|-------------------|
| Model performance metrics | Daily | Model Operations | Metric outside defined threshold |
| False positive rate by customer segment | Weekly | Model Risk | Demographic disparity above threshold |
| Input data quality | Per inference batch | Automated / Data Engineering | Quality rule failure rate above 1% |
| API access log review | Weekly | Security Operations | Anomalous call volume or access pattern |
| Privileged access review | Quarterly | Identity Governance | User without documented provisioning record |
| Supply chain status check | Quarterly | Third-Party Risk | Provider certification lapsed; contract change |
| Human override rate | Monthly | Model Operations | Rate deviation above ±20% from baseline |
| Incident log review | Monthly | Model Risk | Open incidents beyond SLA |
| Annual model validation | Annual | Independent validation team | Any — triggered by calendar or material change |
| EU AI Act compliance review | Annual | Compliance / GRC | Regulatory change; material model change |
 
---
 
## Section 1 — Model performance monitoring
 
### 1.1 Core performance metrics
 
The following metrics must be tracked on a daily basis and reported weekly to the model risk function:
 
| Metric | Description | Escalation threshold |
|--------|-------------|---------------------|
| Fraud detection rate (recall) | Proportion of actual fraud cases correctly identified | Drop of >5% from baseline |
| False positive rate | Proportion of legitimate transactions incorrectly flagged | Rise of >10% from baseline |
| Precision | Proportion of flagged transactions that are genuine fraud | Drop of >5% from baseline |
| F1 score | Harmonic mean of precision and recall | Drop of >5% from baseline |
| Model confidence score distribution | Distribution of fraud probability scores across population | Material shift in distribution shape |
 
### 1.2 Demographic fairness monitoring
 
Fraud detection models carry an inherent risk of demographic bias — over-flagging transactions from certain customer segments based on patterns in historical training data rather than genuine fraud signals.
 
The following fairness metrics must be tracked weekly:
 
| Fairness metric | Definition | Escalation threshold |
|-----------------|------------|---------------------|
| Demographic parity | False positive rate must not differ materially across defined customer segments | >10 percentage point difference between highest and lowest segment |
| Equalised odds | True positive rate and false positive rate should be approximately equal across segments | >5 percentage point difference in false positive rate across segments |
| False positive disparity | Ratio of false positive rates between the highest and lowest segment | Ratio >1.5 triggers review |
 
Where a threshold breach is identified, the model risk function must be notified within one business day. A root cause analysis must be completed within five business days.
 
### 1.3 Model drift detection
 
Model drift occurs when the relationship between input features and the fraud label changes over time — for example, because fraud patterns evolve faster than the model is retrained. The following drift indicators must be monitored:
 
- **Data drift:** Statistical distribution of input features shifting materially from the training distribution
- **Concept drift:** Model performance degrading without a corresponding change in input feature distribution — suggesting the fraud pattern itself has changed
- **Label drift:** The proportion of transactions labelled as fraud changing materially — which may indicate a genuine change in fraud rate or a labelling error in the feedback loop
A material drift signal must trigger a review within ten business days and may trigger an unscheduled retrain.
 
---
 
## Section 2 — Data quality monitoring
 
Input data quality at inference time must be monitored continuously. The following checks must run automatically before each inference batch:
 
| Check | Description | Action on failure |
|-------|-------------|-------------------|
| Null value rate | Proportion of null values in each input feature | Alert if >defined threshold; suppress model output if critical feature null |
| Value range validation | Input values within expected bounds for each feature | Alert and log; flag transaction for human review |
| Staleness check | Features derived from historical data confirmed within freshness window | Alert if stale; suppress or flag output |
| Schema validation | Input data structure matches expected schema | Halt inference batch; escalate to data engineering |
| Volume anomaly | Inference request volume outside expected range | Alert; investigate for data pipeline failure or unusual transaction activity |
 
---
 
## Section 3 — Access governance monitoring
 
### 3.1 API access log monitoring
 
API access logs must be reviewed weekly for the following anomalies:
 
- Access from an IP address outside the defined allowlist
- Access volume exceeding defined rate limits
- Access at unusual hours without a documented business reason
- Access using a key flagged as due for rotation
- Failed authentication attempts above the defined threshold
Anomalies must be investigated within two business days and documented.
 
### 3.2 Privileged access reviews
 
A quarterly review of all privileged access to model components must be conducted, covering:
- Model weights and parameters
- Training data pipeline
- Inference API keys
- Monitoring dashboards (write access)
- Retraining pipeline
The review must confirm: each user has a current provisioning record; no user's role has changed without access being updated; no orphaned accounts exist; and SoD obligations are met.
 
### 3.3 Leaver and role change process
 
Access must be revoked within one business day of a confirmed leaver or role change notification. A weekly report must confirm no open access revocation actions beyond the one-day SLA.
 
---
 
## Section 4 — Supply chain monitoring
 
The trust map (see `02-supply-chain-mapping.md`) must be maintained as a live document. The following events must trigger an immediate reassessment of affected supply chain layers:
 
| Trigger event | Action |
|---------------|--------|
| Third-party provider changes model version | Update supply chain map; raise change record; reassess trust controls |
| Provider's ISO 42001 / SOC 2 certificate lapses | Escalate to TPRM; obtain updated certificate or initiate remediation |
| Provider announces a data breach or security incident | Immediate assessment of impact on model integrity; consider emergency retrain |
| New sub-processor identified in provider's infrastructure | Add to supply chain map; assess trust controls; update contracts if required |
| Regulatory guidance on AI supply chain obligations updated | Review supply chain map against new requirements |
| Foundation model provider releases a new version | Assess impact; raise change record if version upgrade is adopted |
 
---
 
## Section 5 — Annual model validation
 
An independent model validation must be conducted annually by a function separate from the model development and operations teams. The validation must cover:
 
- Reassessment of the model's intended purpose against its actual deployment context
- Review of model performance against the thresholds defined at deployment
- Reassessment of training data for continued appropriateness
- Review of bias and fairness metrics over the preceding 12 months
- Assessment of whether the model's explainability output remains accurate
- Review of the supply chain trust map for completeness and accuracy
- Assessment of whether the EU AI Act classification remains appropriate
Validation findings must be reported to the model risk governance forum. Material findings must be remediated within a defined SLA. The validation report must be retained as part of the technical documentation.
 
---
 
## Section 6 — Escalation and governance
 
### Escalation path
 
| Severity | Example trigger | Immediate action | Escalation |
|----------|----------------|------------------|-----------|
| Critical | Model producing systematically incorrect outputs; data breach in supply chain | Suspend model output; invoke incident response | CISO, CRO, Compliance within 1 hour |
| High | Performance metric outside threshold; demographic disparity detected | Investigate within 1 business day | Model Risk Owner within 4 hours |
| Medium | Data quality alert; access anomaly detected | Investigate within 5 business days | Model Operations within 1 business day |
| Low | Metric approaching threshold; certificate renewal due | Monitor and schedule action | Document in next weekly report |
 
### Governance forums
 
| Forum | Frequency | Attendees | Scope |
|-------|-----------|-----------|-------|
| Model Performance Review | Monthly | Model Operations, Model Risk, Business Owner | Performance metrics, drift, false positive rates |
| AI Risk Governance Forum | Quarterly | CRO, CISO, Compliance, Model Risk, Business | Supply chain, regulatory developments, material findings |
| Annual Validation Review | Annual | CRO, Model Risk, Compliance, Internal Audit | Annual validation findings, model lifecycle decision |
 
---
 
## Section 7 — Model lifecycle decisions
 
Post-deployment monitoring must feed into model lifecycle decisions. The following triggers require a formal lifecycle review:
 
| Trigger | Likely outcome |
|---------|---------------|
| Sustained performance degradation despite retraining | Model replacement |
| Material bias identified that cannot be mitigated | Deployment suspension pending model rebuild |
| Regulatory change materially affecting permitted use | Reassessment of deployment scope |
| Third-party provider no longer viable (insolvency, sanctions, breach) | Emergency provider transition |
| Foundation model provider discontinues the model version in use | Planned migration to new version |
| Annual validation finds model no longer fit for purpose | Model decommission and replacement |
 
---
 
*Part of the A-GRC: AI Governance & Risk Controller framework*
*Author: Layla Bhatti — github.com/lbhatti-risk*
 
