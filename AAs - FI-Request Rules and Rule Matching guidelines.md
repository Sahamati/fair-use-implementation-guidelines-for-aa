### Guidelines to AAs for FI Request Validation for fair use templates
 
For every FI Request (data fetch), the AA must validate:
 
**1. Frequency:** Calendar-based time intervals only, e.g., if a "45 per month" consent is raised on 15th July, the 45 limit applies to the entire calendar month, and the counter resets to 0 at the start of each new month. Similarly, for "1 per day," the counter cannot start before the consent start date; only 1 data pull is allowed that day. This applies to all consents irrespective of the frequency given in the consent artefact.
 
**2. FI Data Range against FI Category:** The FI Data Range in the FI Request must not exceed the FIDataRange > max for the applicable FICategory in the template XML.
 
- **2.1.** If the request includes SEBI FI Types, the SEBI category's limit applies. If it includes NON-SEBI FI Types, the NON-SEBI category's limit applies.
- **2.2.** If a single FI Request includes both SEBI and NON-SEBI FI Types, the AA should apply the stricter (lower) of the two FI Data Range limits.
- **2.3.** If an FI Request exceeds the fair use data range it must be rejected
**3. Consents Created Under Fair Use Limits:** AAs validate the data request strictly as per the parameters of the consent artefact post roll out of v2.0.
 
**4. Consents Created Prior to Fair Use Adoption:** Where the FI Request is made under a consent that was created prior to v2.0 roll out and not in accordance with Fair Use limits, the AA must validate the request against the outer limits prescribed in [Table 2](#table-2-maximum-data-request-fair-use-limits-by-purpose-codes) for the applicable purpose code:
 
- **4.1.** The FI Request must not be made under a consent whose remaining validity extends beyond the earlier of (a) its own original expiry, or (b) the Maximum Consent Validity in Table 2, calculated from the date of v2.0 rollout.
- **4.2.** The frequency of data pulls must not exceed the Maximum Frequency in Table 2.
- **4.3.** The FI Data Range must not exceed the Maximum FI Range in Table 2.
- **4.4.** Any FI Request that does not conform to these Table 2 limits must be rejected.

### Auditing and Reporting
 
**1.** AAs should log and report Fair Use validation failures with clear error codes and messages indicating:
 
- **1.1.** Template ID
- **1.2.** Version
- **1.3.** Attribute(s) in violation

**2.** AAs may use the template reference for reporting, analytics, and ecosystem-level monitoring.
