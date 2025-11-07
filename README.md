# Belgium Weekly Deposit Compliance Framework
**Ensuring Responsible Gaming and Regulatory Adherence**

---

## 1. Project Overview
This framework was developed to monitor and validate weekly player deposits under Belgium’s gaming regulations.  
It ensures that all reported deposits comply with the **€200 weekly limit** set by the **Belgian Gaming Commission (BGC)**.  
The solution is automated, auditable, and designed to support responsible gaming practices across platforms.

---

## 2. Purpose & Benefits
Belgium’s gaming regulations require licensed operators to enforce deposit limits and submit accurate weekly reports.  
Manual monitoring often leads to:
- Delayed breach detection  
- Inconsistent reporting  
- Limited audit transparency  

This framework helps clients and partners:
- Detect non-compliance early  
- Automate validation and reduce manual effort  
- Improve audit readiness and regulatory confidence  
- Ensure traceable, complete, and compliant reporting  

---

## 3. Integration & Compatibility
| Category | Details |
|-----------|----------|
| **Data Sources** | Gaming platforms, data warehouses |
| **Formats Supported** | CSV + JSON metadata |
| **Delivery Method** | Secure SFTP submission |
| **Validation Configs** | YAML-based, customizable |
| **Audit Logs** | Stored for inspection and traceability |

---

## 4. Report Scope & Submission Standards
| Field | Description |
|--------|-------------|
| **Report Name** | Weekly Player Deposit Limit Report |
| **Regulator** | Belgian Gaming Commission (BGC) |
| **Frequency** | Weekly (Monday–Sunday) |
| **Format** | CSV with JSON metadata |
| **Delivery Method** | Secure SFTP submission |
| **Owner** | Compliance & Risk Management Team |

The report captures weekly deposits per player, ensuring that all reported values adhere to the €200 limit and regulatory completeness standards.

---

## 5. Schema Description
| Field Name | Data Type | Description | Regulatory Requirement |
|-------------|------------|-------------|--------------------------|
| Player_ID | String | Unique player identifier | Mandatory |
| Week_StartDate | Date | Beginning of Reporting | Mandatory |
| Week_EndDate | Date | End of Reporting | Mandatory |
| Total_Deposit_EUR | Decimal | Total deposits in euros | Must ≤ €200 |
| Country_code | String | Player registered country | Must = BE |
| Platform | String | Gaming Platform Source | Required for audit trail |

---

## 6. Framework Overview
The Weekly Deposit Compliance Framework provides an automated, auditable validation pipeline to ensure accuracy and integrity before submission to the **Belgian Gaming Commission (BGC)**.

| Component | Function |
|------------|-----------|
| Data Ingestion | Reads aggregated weekly deposits from gaming systems |
| Schema Validator | Ensures completeness and data type accuracy |
| Business Validator | Checks compliance with €200 deposit limit |
| Regulator Validator | Detects missing player IDs or null entries |
| Reporting Module | Calculates reliability score and readiness |
| Audit Logger | Stores validation metadata for traceability |

---

## 7. Folder Structure
be_weekly_deposit_compliance/
│
├── config/ # YAML rule and threshold definitions
├── ingestion/ # Data reader modules
├── validation/ # Schema and threshold checks
├── reporting/ # Compliance reports and reliability metrics
├── audit_logs/ # Exception and audit evidence
├── tests/ # Unit and functional tests
└── docs/ # Regulatory notes and SOP



---

## 8. Sample Validation Rules
| Rule ID | Rule Type | Description | Priority | Recommendation |
|----------|------------|-------------|-----------|----------------|
| DEP001 | Schema | Ensure all mandatory fields are present | High | Include player_id, country_code, total_deposit_eur |
| DEP002 | Business | Weekly deposits must ≤ €200 | High | Flag players exceeding €200 |
| DEP003 | Regulatory | No missing player IDs | High | Populate all player_id values |
| DEP004 | Regulatory | Player country must equal “BE” | Medium | Remove non-BE records |
| DEP005 | Regulatory | Same player should appear only once per week | Medium | Deduplicate weekly data |

---

## 9. Sample Dataset
| Player_ID | Week_Start | Week_End | Total_Deposit_EUR | Country_Code | Platform |
|------------|-------------|-----------|-------------------|---------------|-----------|
| P001 | 2025-10-13 | 2025-10-19 | 185.00 | BE | Online Casino |
| P002 | 2025-10-13 | 2025-10-19 | 220.00 | BE | Sportsbook |
| P003 | 2025-10-13 | 2025-10-19 | NULL | BE | Poker |
| NULL | 2025-10-13 | 2025-10-19 | 160.00 | BE | Casino |
| P004 | 2025-10-13 | 2025-10-19 | 90.00 | NL | Bingo |
| P005 | 2025-10-13 | 2025-10-19 | 130.00 | BE | Sportsbook |

---

## 10. Issues Found
| Issue | Record | Rule Violated | Priority | Resolution |
|--------|---------|----------------|-----------|-------------|
| Deposit exceeds €200 limit | P002 | DEP002 | High | Notify compliance and request refund/adjustment |
| Missing Player ID | N/A | DEP003 | High | Retrieve player identifier before submission |
| Deposit is NULL | P003 | DEP003 | High | Validate upstream data ingestion process |
| Incorrect country code | P004 | DEP004 | Medium | Exclude from Belgium report |

---

## 11. Validation Results
| Validation Check | Status | Priority | Error Count | Recommendation |
|-------------------|---------|-----------|--------------|----------------|
| Mandatory field check | Passed | High | 0 | - |
| Deposit ≤ €200 | Failed | High | 1 | Review P002 |
| Missing Player ID | Failed | High | 2 | Retrieve IDs |
| Country = BE | Failed | Medium | 1 | Exclude P004 |
| Weekly Duplication | Passed | Medium | 0 | - |

---

## 12. Compliance Summary
| Category | Total Checks | Passed | Failed | Compliance % |
|-----------|---------------|---------|---------|---------------|
| Schema | 3 | 3 | 0 | 100% |
| Business | 2 | 1 | 1 | 90% |
| Regulatory | 3 | 2 | 1 | 88% |
| **Overall** | **8** | **6** | **2** | **87%** |

---

## 13. Reliability Score & Submission Decision
| Metric | Value |
|---------|--------|
| Reliability Score | 87% |
| Threshold for Submission | 90% |
| Submission Status | Action Required – Not Ready for Submission |
| Audit Readiness | Partial |
| Exception Count | 4 |

The validation results indicate the dataset is below submission threshold.  
Breaches include excessive deposits, missing identifiers, and incorrect country codes — all of which must be remediated before the report can be considered compliant.

---

## 14. Operational Workflow
1. Load YAML validation configurations.  
2. Ingest weekly deposit data from the gaming data warehouse.  
3. Apply schema and threshold validations.  
4. Calculate compliance metrics and reliability score.  
5. Generate a validation summary report.  
6. Flag failed validations to compliance officers.  
7. Upon remediation, re-run validation for submission readiness.  

---

## 15. Value Delivered
- Real-Time Compliance Monitoring: Detects breaches before submission  
- Audit Transparency: Logs validation results and metadata for inspection  
- Reusable Framework: Adaptable to other jurisdictions and deposit limits  
- Collaborative Reporting: Enables shared visibility across compliance and data teams  
- Governance Maturity: Quantifiable reliability scoring supports regulatory confidence  

---

**Belgium Weekly Deposit Compliance Framework — Driving Responsible Gaming through Data Integrity and Compliance Automation**
