# Fair-use Implementation Guidelines For AA
This repository contains the Fair Use Implementation Guidelines for Account Aggregators (AAs). It outlines the necessary steps to ensure that all Consent requests and FI/requests comply with the upper bounds set in the Fair Use Template Library
# Fair Use Implementation Guidelines for AAs

AAs must ensure that all **consent requests** and **FI requests** comply with the **Fair Use Policy** by following these steps:

- **Defining Fair Use Rules**: Establish rule sets based on the Fair Use Policy.  
- **FIU and Fair Use Template Mapping**: Maintain an updated database of **Data Consumers (FIU_IDs as per Central Registry)**, Purpose Codes, and **Fair Use Template IDs** for all integrated FIUs.  
- **Consent Request Validation**: Verify that every **consent request** aligns with the approved **fair use parameters** before presenting it to customers for review.  
- **FI Request Validation**: Ensure that **FI requests** adhere to the permitted **FI Data Range** and **fetch frequency** per the Fair Use Policy.  
- **Deviation Monitoring and Reporting**: Generate reports on any **deviations** noted from the Fair Use Policy and work with the respective **FIU(s)** to take corrective actions as needed.

## Defining Fair Use Rules  

### Setting up a Rule Database for Consent Creation  
AAs must create a structured database to store Fair Use Rules for consent creation. This database should include key components such as the FIU_ID, FIP_ID, Fair Use Template ID, Fetch Type, Purpose Code, and FI Types. Fair Use Rules are then codified based on the fair use templates.  

When an incoming consent request is received from an FIU (Financial Information User), the system must follow the Fair Use Rules. The system must use the parameters of FIU_ID, FIP_ID, Sahamati Fair Use Template ID, Fetch Type, Purpose Code, and FI Types to ensure compliance with the predefined rule.  

This Google Sheet provides the details of all the rules:  
[Fair Use Rules Database](https://docs.google.com/document/d/174d79GhuvVGTF8BHsytU4Aklb14jQmYMdDmIfPRBhew)  

## Available on Github here:
[Consent Request Rules and Rule Matching Guidelines](Consent%20Request%20Rules%20and%20Rule%20Matching%20Guidelines.md)

 
## Implementing Rule Matching Logic for Consent Requests  

AAs must build systems that use a rule-based approach to validate consent requests based on the fair use rules. Here's how the matching works:  

### Rule Components  
Each rule contains key parameters:  
- `fiu_id`: Financial Information User identifier  
- `sahamati_template_id`: Fair Use Template ID from Sahamati  
- `purpose_code`: Purpose of the consent (e.g., 101, 102, 103, etc.)  
- `fetch_type`: How data is fetched (ONETIME or PERIODIC)  
- `fi_type`: Types of financial information (DEPOSIT, EQUITIES, etc.)  
- `fair_use_rules`: Detailed constraints on data access  

### Wildcard Matching  
- The `*` symbol acts as a wildcard that matches any value.  
- When a rule contains a wildcard, it applies universally regardless of the specific value in that field.  

### Specific Priority  
- More specific rules (with actual IDs instead of wildcards) take precedence over generic wildcard rules.  

### Multiple FI Types  
- When a consent involves multiple FI types, the system applies the maximum allowed range among all applicable rules.  

## Setting up a Rule Database for FI Requests  

AA must maintain a rule database for FI Requests to ensure compliance with the Fair Use Policy and meet the FIP-wise constraints around the maximum data range allowed in a single request.  

This Google Document provides the list of rules for FI Requests:  
[FI Request Rules Database](https://docs.google.com/document/d/1NXVrhmrKw99BwUxCeAyyepPRkVj3ioPEuvxhQ2xQyh0/edit?tab=t.0)  

Available on Github here:
[FI-Request Rules and Rule Matching Guidelines](FI-Request%20Rules%20and%20Rule%20Matching%20Guidelines.md)


## Implementing Rule Matching Logic for FI Requests  

### Rule Components  
- The system should match each FI Request against predefined rules using Purpose Code, FI Type, and maximum FI Data Range.

### SEBI FI Type Handling  
- For Purpose Codes 101 and 102, ensure that no single FI Request exceeds 2 years for SEBI FI Types, even if the overall limit allows more.

### Multiple FI Types  
- If multiple FIP IDs are in the same request, the system should apply the strictest FI Data Range applicable to SEBI and non-SEBI entities.

### Automatic Adjustments  
- If the requested FI Data Range exceeds the allowed limit, the system should adjust it to the maximum permissible range before forwarding to the FIP.

### Request Rejection  
- If an FI Request cannot be adjusted within the permissible range, it should be rejected to prevent policy violations.

### Consistency with Consent Artefact  
- Validate FI Requests against the original consent artefact issued to the FIP to ensure alignment.

### Wildcard Handling  
- Implement logic for wildcard (`*`) cases, where a rule applies universally to all requests matching certain criteria.

## Mapping FIU and Fair Use Templates  

To ensure compliance with the Fair Use Rules, AAs must maintain a structured mapping of FIUs to approved Fair Use Templates, specifically for purpose codes that have more than one use case mapped against them (example: **104 includes loan monitoring and loan collection**). This mapping enables the validation of consent and FI requests against predefined purpose codes and fair use templates.  

## Real-Time Request Validation  

AAs must implement **real-time validation** to ensure that all consent and FI requests comply with the Fair Use Rules before further processing. Any request exceeding defined limits should be either adjusted or rejected to maintain compliance.  

- The wildcard symbol (`*`) denotes a universal rule. This means that the rule applies to every incoming consent request, irrespective of which FIU (Financial Information User) initiates the request or which FIP (Financial Information Provider) holds the accounts involved in the consent.  
- The wildcard ensures that certain rules are consistently enforced across all consent requests without exception.  

### FIU Consent Request Validation  
For every Consent creation request, the system must:  
1. Retrieve all applicable rules based on request parameters  
2. Validate parameters against rule limits  
3. Reject request if any parameter exceeds limits  

### FIU FI Request Validation  
For every FI Request (for data), the system must:  
1. Validate the request against the copy of the FIP consent artefact  
2. Validate the data range for SEBI FI types, ensuring a maximum of two years of data per request  
3. Either adjust FI Data Range or reject requests as needed  

## Summary  

In summary, the system must ensure that all consent requests and approvals adhere to the established Fair Use Rules, safeguarding customer interests, compliance, and maintaining the integrity of the consent management process.  

For examples, refer to this document:  
[Fair Use Guidelines & Examples](https://docs.google.com/document/d/1NXVrhmrKw99BwUxCeAyyepPRkVj3ioPEuvxhQ2xQyh0/edit?tab=t.0)  

## Error Codes and Messages for Deviant Transactions

AAs must return standardized responses when a Consent or FI request does not conform to the approved Fair Use templates. In such cases, the HTTP status code **412 – Precondition Failed** must be used.

| API            | HTTP Error Code | Response Type        | Error Message Format                                                                 |
|----------------|------------------|-----------------------|----------------------------------------------------------------------------------------|
| Consent Request | 412              | Precondition Failed   | Consent parameters are not as per fair use policy – {Attribute name} is invalid.       |
| FI/Request      | 412              | Precondition Failed   | FI data range is not as per fair use policy.                                           |

> The `{Attribute name}` placeholder may be replaced with the specific non-compliant parameter (e.g., `Purpose`, `Frequency`, `Data Range`) where applicable.  
> AAs may choose whether or not to include specific deviation details in the error message.  
> The level of detail is left to the discretion of the AA, with the intent of assisting FIUs in identifying and correcting non-compliant requests.

---

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

