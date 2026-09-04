# Fair-use Implementation Guidelines For AA
This repository contains the Fair Use Implementation Guidelines for Account Aggregators (AAs). It outlines the necessary steps to ensure that all Consent requests and FI/requests comply with the upper bounds set in the Fair Use Template Library
# Fair Use Implementation Guidelines for AAs

AAs must ensure that all **consent requests** and **FI requests** comply with the **Fair Use Policy**. To ensure the same following guidelines have been issued in v2.0:

AAs - Consent Request Validation Rules [https://github.com/Sahamati/fair-use-implementation-guidelines-for-aa/blob/v2.0/AAs%20-%20Consent%20Request%20Rules%20and%20Rule%20Matching%20Guidelines.md] 

AAs - FI Request Validation Rules [https://github.com/Sahamati/fair-use-implementation-guidelines-for-aa/blob/v2.0/AAs%20-%20FI-Request%20Rules%20and%20Rule%20Matching%20guidelines.md]

### Auditing and Reporting
 
**1.** AAs should log and report Fair Use validation failures with clear error codes and messages indicating:
 
- **1.1.** Template ID
- **1.2.** Version
- **1.3.** Attribute(s) in violation

**2.** AAs may use the template reference for reporting, analytics, and ecosystem-level monitoring.


## Monthly Fair Use Reporting by AAs – Guidelines on Data Collation

To support ecosystem-wide transparency and encourage collaborative adoption of Fair Use Templates, AAs are expected to submit **monthly reports** summarizing their implementation status.

Below are the recommended data points along with guidance on how to collate and report each metric:

| Field Name                                                  | Format                                     | Guidelines on Data Collection                                                                                                                                         |
|-------------------------------------------------------------|--------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Actions Taken for Compliance                                | Text                                       | AAs are expected to maintain internal records of outreach and operational activities related to Fair Use implementation. Examples include: one-on-one calls with FIUs, email campaigns, identifying and flagging deviations, providing support on template alignment, enabling real-time detection mechanisms, etc. Multiple actions may be listed as a comma-separated string. |
| % of FIUs Confirmed Adherence to Fair Use Templates         | Percent                                    | Estimate the percentage of integrated FIUs who have confirmed that Fair Use Templates are being followed, based on request patterns and implementation observations.   |
| Is Detection of Fair Use Template Compliance Automated?     | Fully Automated / Partially Automated / Yet to be Automated | Indicate the state of automation for detecting Fair Use Template compliance within your systems as of the end of the reporting month.                                 |
| If Above is not 'Fully Automated', Estimated Implementation Date | DD-MM-YYYY                               | If compliance detection is not fully automated, provide a realistic date by which automation is expected to be completed.                                              |
| % of Consents Raised as per Fair Use Templates              | Percent                                    | Collate details of consent requests received during the reporting month and determine the percentage that align with known Fair Use Templates using internal matching logic. |

