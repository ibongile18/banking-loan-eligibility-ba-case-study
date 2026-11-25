# 02. Functional Requirements & Agile User Stories

## 1. Functional Requirements (FR)
* **FR-01 (Affordability Calculation):** The system must calculate the applicant's Debt-to-Income (DTI) ratio using gross monthly income, existing monthly debt obligations, and estimated new loan repayment.
* **FR-02 (Automated Risk Tiering):** The system must classify applicants into `LOW_RISK`, `MEDIUM_RISK`, or `HIGH_RISK` based on credit score, DTI ratio, and employment tenure.
* **FR-03 (Decision Routing):**
  * `APPROVED`: Credit score ≥ 680 AND DTI ≤ 35% AND employment tenure ≥ 6 months.
  * `MANUAL_REVIEW`: Credit score 600–679 OR DTI between 35.01% and 45%.
  * `DECLINED`: Credit score < 600 OR DTI > 45% (aligned with National Credit Act reckless lending prevention).
* **FR-04 (Audit Logging):** Every automated decision must record the exact rules triggered and timestamp for compliance auditing.

## 2. Non-Functional Requirements (NFR)
* **NFR-01 (Performance):** Automated eligibility scoring must complete in under **2 seconds** per application.
* **NFR-02 (Auditability & Explainability):** Decline reasons must be human-readable so customer support and credit analysts can explain outcomes clearly.
* **NFR-03 (Data Integrity):** Financial figures must prevent floating-point rounding errors in repayment calculations.

## 3. Agile User Stories & Acceptance Criteria

### Story 1: Instant Pre-Approval for Qualifying Applicants
> **As a** retail banking applicant,  
> **I want** to receive an instant pre-approval decision after submitting my financial details,  
> **So that** I know immediately whether I qualify without waiting days for manual review.

* **Acceptance Criteria (Gherkin):**
  * **Given** an applicant has a credit score of `710`, a DTI of `28%`, and `14 months` of employment,
  * **When** the scoring engine evaluates the application,
  * **Then** the decision status is set to `APPROVED` and the risk tier is `LOW_RISK`.

### Story 2: Borderline Risk Flagging for Credit Analysts
> **As a** Credit Risk Analyst,  
> **I want** borderline applications automatically flagged with specific risk reasons,  
> **So that** I only spend manual review time on complex cases that require human judgment.

* **Acceptance Criteria (Gherkin):**
  * **Given** an applicant has a credit score of `645` and a DTI of `39%`,
  * **When** the scoring engine evaluates the application,
  * **Then** the decision status is set to `MANUAL_REVIEW` and the system outputs the flag `"Moderate credit score & elevated DTI ratio"`.
