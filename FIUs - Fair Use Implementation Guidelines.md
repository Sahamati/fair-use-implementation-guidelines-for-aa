## Fair Use Implementation Guidelines for FIUs

As part of the participatory governance initiative, FIUs are expected to implement the Fair Use templates as agreed upon by the ecosystem for their respective use cases. The parameters of the individual Fair Use templates in the Fair Use Template Library represent upper bounds for the respective use cases, as decided by the relevant User Councils.

The parameters in the Fair Use templates should be treated by participants as outer limits and not be construed as legal advice in any manner. Participants are encouraged to review their use case(s) and ensure compliance with applicable laws, including the RBI Master Directions on NBFC-AA and the DPDP Act.

Sahamati will publish additional Fair Use templates as the AA ecosystem evolves, based on discussions in the relevant Use Case Councils and the Fair Use Committee. Existing Fair Use templates may also be revised based on statutory and regulatory guidance, including the DPDP Act and the Rules issued thereunder.

## Guidelines to FIUs on Consent Creation as per fair use templates:
 
Guidelines for the adoption of the fair use templates remain unchanged from v1.0, except for the introduction of the purpose refUri field and its usage.
 
**1. General Responsibility for Fitment:** The mere existence or publication of a Fair Use Template in the Registry does not automatically grant an FIU the right to use it. FIUs must ensure alignment between their regulatory charter, the selected use case, and the declared Fair Use Template.
 
**2. Use Case Description:** This describes the specific financial service or context for which the data is being accessed. FIUs must align their consent purpose with this use case and avoid using any template for unrelated use cases.
 
**3. Purpose Text:** FIUs should reference the purpose text in the Fair Use Template to ensure consistent, clear customer communication across the ecosystem. The intent and meaning of the template's purpose text must not be altered. FIUs may enhance the purpose text to provide additional information relevant to their use case (such as product details), provided such enhancements do not change the underlying use case or bundle multiple use cases within a single template.
 
**4. Purpose Code:** FIUs must use the purpose code as is in the template. This should map to the ReBIT-specified purpose codes and is used for backend classification of consent and rule setting at AA and FIPs.
 
**5. Purpose refUri:** FIUs must ensure they pass the Fair Use Template ID in the given canonical URL format (7.1 above), referencing the specific Fair Use Template they are using for the consent request. FIUs must further ensure that all parameters in the consent are strictly aligned with what is published in the referenced template. Any deviation from the published template's parameters, even if the template is correctly referenced, would constitute a fair use deviation.
 
**6. Consent Type:** This defines which components of the data packet are to be accessed – Profile, Summary/Holdings, and/or Transactions. FIUs must restrict data requests to only the consent types mentioned in the template. Requesting more components than specified would be flagged as a deviation.
 
**7. Fetch Type:** This specifies how the data is accessed - Onetime or Periodic. FIUs must configure their consent and FI request logic accordingly. A template that supports only one-time fetch must not be used for recurring access and vice versa.
 
**8. Frequency:** This indicates the maximum allowed number of data pulls during the validity period, based on the unit of time (day, month, or year) decided by the User Councils and the Fair Use Committee. FIUs must ensure that data fetches across the validity period do not exceed the defined ceiling for the specified unit as prescribed in the template, and that their data fetch frequency adheres to the data minimisation principles under the DPDP Act. FIUs are advised to use calendar-based intervals only (e.g., calendar day/month/year), not rolling or dynamic intervals.
 
> *Example: A template with frequency set as "45 per month" must not be interpreted as "1.5 per day." The FIU must ensure that the number of data pulls in any calendar month does not exceed 45.*
 
**8. Validity Period:** This indicates how long the consent is valid (e.g., 6 months, 1 year). As per ReBIT specifications, FIUs must display both Consent Start Date and Expiry Date to the user. FIUs are expected to ensure the validity duration does not exceed the maximum allowed in the template.
 
**9. Maximum FI Data Range:** This defines the maximum span of historical data that can be requested in a single FI request. FIUs must:
 
- **1.** Display a consent window to the user that does not exceed the time from consent start to consent expiry minus the FI data range. (Consent Request API)
- **2.** Limit the data request window to this range. (FI/Request API)
> *Example - Consent Start Date: 7th June 2025, Consent Expiry Date: 7th June 2026, Maximum FI Data Range as per Template: 6 months*
>
> *In this case, the FIU can fetch up to 6 months of data at once in an FI Data Request. On 15th June 2025, it can pull statements from 15th December 2024 to 15th June 2025.*
>
> *FI Data Range in Consent Request: 7th December 2023 to 7th June 2025.*
 
**10. Data Life:** This is defined in ReBIT as "for how long the FIU/AA Client stores the data". FIUs must not confuse this with data storage - that requires data to be archived as per the storage requirements under their regulations. This is the time period available for the FIU to process the data for the consented purpose, post which it is archived or purged, based on regulatory requirements, and not available for processing again. FIUs are expected to "delete" or "purge" the data after the data life window expires unless any applicable law or regulation requires archival thereof.
 
**12. One Active Consent Per Template Per FIU:** An FIU must not seek more than one active consent for the same account information, under the same Purpose Code and Fair Use Template, at the same time (except in the case of CT001, CT003, CT035, which may result from multiple loans granted to the same customer by the same FIU). Where an active consent already exists covering the same accounts under the same Purpose Code, the FIU must not request an additional consent for those accounts. Once the current active consent expires, the FIU may request the customer to provide a fresh consent for continuity of service.
 
### Declaration of Fair Use Template to Customer and All Participants
 
**1.** As mentioned above, the FIU must use the applicable use case in the form of the Fair Use Template ID by including the Fair Use Registry XML link in the refUri field of the Purpose block within the consent request payload.
 
**2.** Template ID will be declared to the AA, and through the AA to the FIP, removing the need for inference-based matching. It is passed through to the FIP, giving the FIP direct visibility into the declared use case and template.
 
**3. Maintaining Consistency in Template Declaration:** To maintain consistency across the ecosystem, FIUs are requested to:
 
- **3.1. Version Pinning:** Reference the exact version of the template in the Registry URL. If Sahamati publishes a revised version, FIUs should migrate within the transition period communicated by Sahamati.
- **3.2. No Tampering:** The FIU should not host, proxy, cache, or modify the XML. The link should always point to the canonical Fair Use Registry at library.sahamati.org.in. Any request pointing to a different domain will be rejected by the AA.
- **3.3. Template Alignment:** The FIU should select the correct Fair Use Template for its use case. Using a template designated for a different use case is a deviation and a ground for rejection.
- **3.4. Declaration of Fair Use Template to Sahamati:** During the onboarding of an entity into Sahamati's central registry, each FIU must declare their use case to Sahamati via the required forms.

###  Guidelines to FIUs on Data requests as per fair use templates:
 
**1. Consents Created Under Fair Use Limits:** FIUs must fetch data strictly as per the parameters of the relevant consent artefact.
 
**2. Consents Created Prior to Fair Use Adoption:**
 
- **2.1.** FIUs must not rely on such consents merely because they remain technically valid.
- **2.2.** FIUs must retire pre-existing consents by the earlier of (a) the consent's own original expiry date, or (b) the Maximum Consent Validity prescribed below for the applicable purpose code, calculated from the date of v2.0 rollout. FIUs must obtain a fresh, Fair-Use-conforming consent to continue servicing the customer beyond this date.
- **2.3.** Data must not be fetched at a frequency exceeding the Maximum Frequency prescribed below, regardless of what the original consent permits.
- **2.4.** Non-conforming requests are liable to rejection. FIPs may independently enforce these limits at their end.

##### Table: Maximum data request fair use limits by purpose codes for Consents Created before fair use:
 
<table>
<thead>
<tr>
<th>Purpose Code</th>
<th>Maximum FI Range</th>
<th>Maximum Consent Validity</th>
<th>Maximum Frequency</th>
</tr>
</thead>
<tbody>
<tr>
<td>101 – Wealth Management</td>
<td>Limits set by FIPs for SEBI FI Types<br>13 months for other FI Types</td>
<td>1 Year</td>
<td>31/month</td>
</tr>
<tr>
<td>102 – Personal Finance Management</td>
<td>Limits set by FIPs for SEBI FI Types<br>13 months for other FI Types</td>
<td>1 Year</td>
<td>45/month</td>
</tr>
<tr>
<td>103 – Loan Underwriting</td>
<td>12 months</td>
<td>45 days</td>
<td>1 (One-time)</td>
</tr>
<tr>
<td>104 – Loan Monitoring</td>
<td>1 day for summary-only consents<br>6 months for summary, profile, transactions</td>
<td>8 years for summary-only consents,<br>5 years for summary, profile, transactions</td>
<td>31/month (Summary only) /<br>25/month (Summary, Profile, Transactions)</td>
</tr>
<tr>
<td>105 – Account Verification / Customer Verification</td>
<td>12 months</td>
<td>1 month</td>
<td>1 (One-time)</td>
</tr>
</tbody>
</table>
---
