# 03 — Control Requirements: High-Risk AI in Retail Banking
 
This document defines the minimum control requirements for a high-risk AI system (fraud detection) in a retail banking context, organised by control domain. Each control includes the regulatory basis, design requirement, operating requirement, and audit test approach.
 
All scenarios are synthetic. Nothing in this document originates from a live client engagement.
 
---
 
## Control domain overview
 
| Domain | Controls | Primary regulatory basis |
|--------|----------|--------------------------|
| Data Governance | DG-01 to DG-03 | EU AI Act Article 10; GDPR Article 5 |
| Model Governance | MG-01 to MG-04 | EU AI Act Articles 9, 11, 15, 72 |
| Access Control | AC-01 to AC-03 | EU AI Act Article 15(5); ISO 27001 A.5.15 |
| Human Oversight | HO-01 to HO-03 | EU AI Act Article 14; Article 26 |
| Incident Response | IR-01 to IR-02 | EU AI Act Articles 73, 26(5) |
 
---
 
## Domain 1 — Data Governance
 
### DG-01: Training data documentation
 
**Control objective:** Ensure training data is documented with sufficient detail to assess its suitability, provenance, and known limitations before model training begins.
 
**Design requirement:**
A data card or equivalent document must exist for each training dataset, covering: data source and collection method, date range, geographic scope, known gaps or exclusions, and any pre-processing transformations applied.
 
**Operating requirement:**
The data card must be reviewed and approved by the model risk function before training commences. Version control must be applied — each retrain using a materially different dataset must produce a new or updated data card.
 
**Audit test approach:**
- Obtain the data card for the current model version
- Confirm it covers all required fields
- Cross-reference against the model card (MG-01) to confirm alignment between stated training data and actual data used
- Confirm approval evidence exists from the second-line model risk function
**Common design weakness:** Data card exists but was produced after training, not before. Pre-training approval cannot be evidenced.
 
**Common operating weakness:** Data card not updated following a retrain. Current model version references an outdated data card from a prior version.
 
---
 
### DG-02: Training data bias assessment
 
**Control objective:** Ensure the training dataset has been assessed for demographic bias before deployment, and that known biases are documented with mitigating actions.
 
**Design requirement:**
A bias assessment methodology must be defined, covering which demographic attributes are tested (e.g. age band, geography, transaction type), which fairness metrics are applied (e.g. demographic parity, equalised odds), and what threshold constitutes an acceptable bias level.
 
**Operating requirement:**
The bias assessment must be conducted before each model deployment and before each material retrain. Results must be reviewed by the model risk function. Where bias exceeds the defined threshold, a documented decision to deploy (with mitigating action) or not deploy must be evidenced.
 
**Audit test approach:**
- Obtain the bias assessment methodology document
- Obtain the most recent bias assessment results
- Confirm assessment was conducted before deployment (check timestamp against deployment date)
- Confirm results were reviewed by second-line model risk
- Where bias was identified, confirm a documented decision and mitigation plan exist
**Common design weakness:** No defined threshold for acceptable bias. Assessment is conducted but there is no basis for determining whether the result is acceptable.
 
**Common operating weakness:** Bias assessment conducted at initial deployment but not repeated at retrain. Material bias introduced through new training data goes undetected.
 
---
 
### DG-03: Input data quality at inference time
 
**Control objective:** Ensure that input data fed to the fraud detection model at inference time meets defined quality standards, and that anomalies are detected and escalated before influencing fraud decisions.
 
**Design requirement:**
Data quality rules must be defined for each model input feature, covering: expected data type, permitted value range, null/missing value threshold, and staleness threshold (for features derived from historical data).
 
**Operating requirement:**
Data quality checks must run automatically before each inference call. Failures must trigger an alert to the operations team and, depending on severity, either suppress the model output or flag the decision for human review.
 
**Audit test approach:**
- Obtain the data quality rule set for current model version
- Confirm rules exist for all material input features
- Test whether quality checks run automatically (obtain system log evidence)
- Confirm alert routing and escalation path are documented and tested
- Review alert log for the audit period — confirm alerts were investigated and resolved within SLA
**Common design weakness:** Data quality rules defined at development but not maintained as input features change over time. Rules reference deprecated features or omit new features added in later versions.
 
**Common operating weakness:** Alerts generated but not investigated. Alert log shows recurring failures with no documented resolution.
 
---
 
## Domain 2 — Model Governance
 
### MG-01: Model card and technical documentation
 
**Control objective:** Ensure technical documentation exists for the fraud detection model that satisfies Article 11 and Annex IV of the EU AI Act, and is sufficient for a third party to assess the model's fitness for purpose.
 
**Design requirement:**
Technical documentation must include: intended purpose and scope, model architecture summary, training methodology, performance metrics (accuracy, precision, recall, F1, AUC), known limitations, explainability approach, and version history.
 
**Operating requirement:**
Documentation must be updated with each model version. The current version of the documentation must be accessible to the second-line model risk function and, on request, to regulators.
 
**Audit test approach:**
- Obtain the model card for the current model version
- Confirm it covers all Annex IV-required elements
- Confirm version history is complete and each version change is documented
- Confirm the document is version-controlled and access-restricted appropriately
---
 
### MG-02: Pre-deployment testing
 
**Control objective:** Ensure the fraud detection model is tested for accuracy, robustness, and security before each deployment.
 
**Design requirement:**
A pre-deployment testing protocol must define: the test dataset (held-out, not used in training), the performance metrics and pass/fail thresholds, adversarial robustness tests (e.g. testing model behaviour under data poisoning scenarios), and sign-off requirements before production deployment.
 
**Operating requirement:**
Testing must be completed and results reviewed before each production deployment. A named approver in the model risk function must sign off. Results must be retained.
 
**Audit test approach:**
- Obtain the pre-deployment test results for the current model version
- Confirm test dataset was not used in training (check data lineage documentation)
- Confirm all defined metrics met pass/fail thresholds, or document approved exceptions
- Confirm sign-off evidence exists and is dated before the production deployment date
---
 
### MG-03: Model change management
 
**Control objective:** Ensure all material changes to the fraud detection model are subject to a formal change management process, equivalent to a production code change.
 
**Design requirement:**
A model change policy must define what constitutes a material change (retraining, threshold adjustment, input feature change, provider change, foundation model version upgrade) and require a formal change record for each.
 
**Operating requirement:**
Change records must be raised before implementation, include a risk assessment and rollback plan, require dual approval (model risk + business owner), and be closed with post-implementation review evidence.
 
**Audit test approach:**
- Obtain the model change log for the audit period
- Confirm all material changes have a corresponding change record
- For a sample of change records, confirm: pre-implementation approval, risk assessment, rollback plan, and post-implementation review
- Confirm no deployments occurred outside the change management process (cross-reference deployment logs against change records)
**Key risk — AI-specific:** Foundation model version upgrades by a third-party provider may not trigger an internal change record if the bank's change policy does not explicitly include vendor-side changes. This is a common design gap.
 
---
 
### MG-04: Post-deployment monitoring
 
**Control objective:** Ensure the fraud detection model's performance is continuously monitored after deployment, and that material degradation triggers a defined response.
 
**Design requirement:**
A model monitoring framework must define: the metrics to be monitored (fraud detection rate, false positive rate, demographic parity across customer segments), the monitoring frequency, the thresholds that trigger escalation, and the escalation path.
 
**Operating requirement:**
Monitoring must run on the defined frequency. Results must be reviewed by a named owner. Threshold breaches must be escalated and documented. Annual model validation must be conducted by an independent function.
 
**Audit test approach:**
- Obtain the monitoring framework document
- Confirm all defined metrics are being produced at the required frequency
- Review monitoring reports for the audit period — confirm threshold breaches were escalated and resolved
- Confirm annual model validation was conducted by an independent function and results reviewed by model risk
---
 
## Domain 3 — Access Control
 
### AC-01: Privileged access to model components
 
**Control objective:** Ensure that access to model weights, training pipelines, and inference infrastructure is restricted to authorised personnel and managed through a privileged access management framework.
 
**Design requirement:**
A privileged access policy must define the roles authorised to access each model component, the access provisioning process, the review frequency, and the PAM tooling used.
 
**Operating requirement:**
Access must be provisioned through a formal process with documented approval. A user access review must be conducted at least annually, or following a role change. Access must be revoked within one business day of a leaver or role change notification.
 
**Audit test approach:**
- Obtain the current privileged user list for each model component
- Confirm all users have a documented provisioning record
- Confirm the most recent UAR was conducted within the defined review cycle
- Test a sample of leavers or role changes — confirm access was revoked within SLA
- Confirm SoD: no individual should both provision access and approve their own UAR
---
 
### AC-02: API key governance
 
**Control objective:** Ensure inference API keys are managed, rotated, and monitored to prevent unauthorised access to the fraud detection model.
 
**Design requirement:**
An API key governance policy must define: key naming and ownership conventions, rotation frequency, the process for emergency key revocation, and the logging requirements for API calls.
 
**Operating requirement:**
Keys must be rotated on the defined schedule. Unused or orphaned keys must be identified and revoked. API call logs must be retained and reviewed for anomalies.
 
**Audit test approach:**
- Obtain the API key inventory
- Confirm each key has a named owner and a last-rotation date
- Confirm rotation frequency meets policy requirements
- Identify any keys not rotated within the defined period — confirm explanation
- Review API call logs for anomalous access patterns
---
 
### AC-03: User access review — AI pipeline
 
**Control objective:** Ensure that all users with access to the AI model pipeline (training, inference, monitoring) are reviewed periodically to confirm access remains appropriate.
 
**Design requirement:**
The UAR scope must explicitly include AI pipeline components, not just traditional infrastructure. The review must cover all access vectors: model weights, API keys, monitoring dashboards, retraining pipeline.
 
**Operating requirement:**
UAR must be conducted at least annually. The reviewer must be independent — they must not review their own access. Results must be documented and exceptions remediated within a defined SLA.
 
**Audit test approach:**
- Confirm the UAR scope includes all AI pipeline access vectors
- Obtain UAR completion evidence for the most recent review cycle
- Confirm the reviewer did not review their own access (SoD check)
- Review exception log — confirm all exceptions were remediated within SLA
---
 
## Domain 4 — Human Oversight
 
### HO-01: Human override capability
 
**Control objective:** Ensure a human can override, reverse, or escalate any automated fraud decision, and that the override mechanism is documented, tested, and accessible.
 
**Design requirement:**
The fraud detection system must include a documented override mechanism. The override must be accessible to authorised staff without requiring technical intervention. The override must create an audit trail.
 
**Operating requirement:**
Override decisions must be logged with: the overriding user, the reason, the original model decision, and the outcome. Override rates must be monitored — material deviations from expected rates must trigger a review.
 
**Audit test approach:**
- Obtain the override mechanism documentation
- Confirm the override is accessible without technical intervention
- Obtain the override log for the audit period
- Confirm override decisions include all required fields
- Review override rate trend — confirm material deviations were investigated
---
 
### HO-02: Explainability for human reviewers
 
**Control objective:** Ensure that staff responsible for reviewing AI fraud decisions can access a meaningful explanation of why a transaction was flagged.
 
**Design requirement:**
An explainability mechanism must be defined and documented. The explanation must be accessible to the reviewing staff member without specialist data science knowledge. The explanation must reference the primary features driving the fraud score.
 
**Operating requirement:**
The explainability output must be available for every flagged transaction at the time of human review. The format and content of explanations must be reviewed periodically to confirm they remain accurate as the model evolves.
 
**Audit test approach:**
- Obtain a sample of flagged transactions and retrieve the associated explanation
- Assess whether the explanation references primary model features
- Confirm the explanation was available to the reviewer at the time of review
- Confirm the explainability mechanism has been reviewed following any model version change
---
 
### HO-03: Human oversight training
 
**Control objective:** Ensure staff responsible for reviewing AI fraud decisions are trained on the system's capabilities, limitations, and the circumstances in which human judgement must override the model.
 
**Design requirement:**
A training programme must exist covering: what the model does and does not do, known limitations and bias risks, how to interpret the explainability output, and when and how to invoke the override mechanism.
 
**Operating requirement:**
Training must be completed before a staff member reviews AI-assisted decisions. Refresher training must be completed annually or following a material model change. Completion must be recorded.
 
**Audit test approach:**
- Obtain the training programme content
- Confirm coverage of all required topics
- Obtain the training completion record for all staff with review responsibilities
- Confirm all active reviewers have completed training within the required period
---
 
## Domain 5 — Incident Response
 
### IR-01: Serious incident reporting
 
**Control objective:** Ensure a procedure exists to identify, assess, and report serious incidents involving the fraud detection model to the relevant national competent authority, as required by Article 73 of the EU AI Act.
 
**Design requirement:**
A serious incident procedure must define: what constitutes a serious incident (including reference to Article 3(49)), the escalation path, the reporting timeline, and the responsible owner.
 
**Operating requirement:**
Any event meeting the serious incident threshold must be escalated and assessed within 24 hours. Reportable incidents must be notified to the competent authority within the Article 73 timeline. All incidents and decisions must be documented.
 
**Audit test approach:**
- Obtain the serious incident procedure
- Confirm it references Article 3(49) and Article 73 definitions
- Review the incident log for the audit period
- For any incidents assessed against the serious incident threshold, confirm the assessment was documented and the outcome was appropriate
- Confirm any reportable incidents were notified within the required timeline
---
 
### IR-02: Incident log and root cause analysis
 
**Control objective:** Ensure all AI-related incidents are logged and subject to root cause analysis, with findings used to improve the control environment.
 
**Design requirement:**
An incident log must capture: incident date, description, affected system component, severity, detection method, and root cause. A root cause analysis (RCA) process must be defined with completion SLAs by severity.
 
**Operating requirement:**
All incidents must be logged within one business day of detection. RCA must be completed within the defined SLA. RCA findings must feed into the model's risk register and, where applicable, into the change management process.
 
**Audit test approach:**
- Obtain the incident log for the audit period
- Confirm all incidents have a logged root cause
- For a sample, confirm RCA was completed within the defined SLA
- Confirm RCA findings were reviewed by model risk and, where applicable, triggered a change record
---
 
*Part of the A-GRC: AI Governance & Risk Controller framework*
*Author: Layla Bhatti — github.com/lbhatti-risk*
