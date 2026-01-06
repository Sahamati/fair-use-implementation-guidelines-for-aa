## Fair Use Implementation Guidelines for FIUs

As part of the participatory governance initiative, FIUs are expected to implement the Fair Use templates as agreed upon by the ecosystem for their respective use cases. The parameters of the individual Fair Use templates in the Fair Use Template Library represent upper bounds for the respective use cases, as decided by the relevant User Councils.

The parameters in the Fair Use templates should be treated by participants as outer limits and not be construed as legal advice in any manner. Participants are encouraged to review their use case(s) and ensure compliance with applicable laws, including the RBI Master Directions on NBFC-AA and the DPDP Act.

Sahamati will publish additional Fair Use templates as the AA ecosystem evolves, based on discussions in the relevant Use Case Councils and the Fair Use Committee. Existing Fair Use templates may also be revised based on statutory and regulatory guidance, including the DPDP Act and the Rules issued thereunder.

### Guidelines on the Attributes of Fair Use Templates

- **Use Case Description**  
  This describes the specific financial need or context for which the data is being accessed. FIUs must align their consent purpose with this use case and avoid using the template for unrelated use cases.

- **Purpose Text**  
  FIUs must display the exact purpose text as provided in the template to ensure uniform customer communication across the ecosystem. No customization is allowed, as this text is designed to build trust and clarity.

- **Purpose Code**  
  This maps to the ReBIT-specified purpose codes and is used for backend classification of consent and rule setting at AA and FIPs. FIUs must use the purpose code as-is from the template.

- **Consent Type**  
  This defines the components of the data packet to be accessed – Profile, Summary / Holdings, and/or Transactions. FIUs must restrict data requests to only the consent types mentioned in the template. Requesting more components than specified would be flagged as a deviation.

- **Fetch Type**  
  This specifies how the data is accessed – One-time or Periodic. FIUs must configure their consent and FI request logic accordingly. A template that supports only one-time fetch must not be used for recurring access and vice versa.

- **Frequency**  
  This indicates the maximum allowed number of data pulls during the validity period, based on the unit of time (day, month, or year) decided by the Fair Use Councils.

  FIUs must ensure that data fetches across the validity period do not exceed the defined ceiling for the specified unit as prescribed in the template. FIUs are advised to use calendar-based intervals only (e.g., calendar day/month/year), not rolling or dynamic intervals.

  **Example**:  
  A template with frequency set as “45 per month” must not be interpreted as “1.5 per day.” The FIU must ensure that the number of data pulls in any calendar month does not exceed 45.

- **Validity Period**  
  This indicates how long the consent is valid (e.g., 6 months, 1 year). As per ReBIT specifications, FIUs must display both Consent Start Date and Expiry Date to the user. Fair Use Councils expect the FIUs to ensure the validity duration does not exceed the maximum allowed in the template.

- **Maximum FI Data Range**  
  This defines the maximum span of historical data that can be requested in a single FI request.

  FIUs must:  
  - Display to the user a consent window that does not exceed `consent start - FI data range` to `consent expiry`. *(Consent Request API)*  
  - Limit the data request window to this range. *(FI/Request API)*

  **Example**:  
  - Consent Start Date: 7th June 2024  
  - Consent Expiry Date: 7th June 2025  
  - Maximum FI Data Range as per Template: 6 months  

  In this case, the FIU can fetch up to 6 months of data at once in a FI Data Request. On 15th June 2024, it can pull statements from 15th December 2023 to 15th June 2024.  
  FI Data Range in Consent Request: 7th December 2023 to 7th June 2025

- **Data Life**  
  This is defined in ReBIT as “for how long the FIU/AA Client stores the data”. FIUs must not confuse this with data storage — that requires data to be archived as per the storage requirements under their regulations.

  This is the time period available for the FIU to process the data for the consented purpose, post which it is archived and not available for processing again. FIUs are expected to “delete” or “purge” the data after the Data Life time-window expires.

---

The same is available in Google Document here: https://docs.google.com/document/d/12meAAjUhc7DrCUXDiZ9rsSu7ssTjuhgD8OJJQ_iv5Wk/edit?
