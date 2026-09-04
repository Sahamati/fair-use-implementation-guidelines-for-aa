## Fair Use Implementation Guidelines for FIPs (on Fair Use Enforcement)

Being the custodians of customer data integrity and security, **FIPs** have reserved the right to act as *second checkers* of incoming **Consent Requests** and **FI/Request**.

While **Account Aggregators (AAs)** serve as the **primary enforcers** of Fair Use compliance, FIPs may deploy their own validation as given below. In case FIPs wish to do so, under v2.0, they no longer need to infer the template. They receive the explicit Fair Use Registry XML link from the AA as part of the consent artefact.
 
### Guidelines to FIPs for Consent Validation for Fair Use Templates
 
**1. Acknowledgement of Consent Artefact:** Upon receiving the signed consent artefact copy shared by the AA via the Consent Notification API, the FIP must acknowledge it, except where the FIP identifies a Fair Use deviation. The FIP must not withhold acknowledgement for any reason unrelated to a Fair Use deviation.
 
**2. Template Validation (Recommended):** Where a FIP chooses to validate the consent artefact, it should extract the templateId from the refUri in the Purpose block and validate the consent artefact's parameters against the corresponding Fair Use Template, in the manner prescribed in AAs - Consent Request Rules - https://github.com/Sahamati/fair-use-implementation-guidelines-for-aa/blob/v2.0/AAs%20-%20Consent%20Request%20Rules%20and%20Rule%20Matching%20Guidelines.md
 
**3. Deviation Handling:** Where the FIP identifies a deviation from the Fair Use Template's prescribed limits, it may decline to acknowledge the consent artefact, citing the relevant deviation.
 
**4. Error Codes:** Where a FIP declines to acknowledge a consent artefact under this section, it must use the error codes prescribed in AAs - FI-Request Rules - https://github.com/Sahamati/fair-use-implementation-guidelines-for-aa/blob/v2.0/AAs%20-%20FI-Request%20Rules%20and%20Rule%20Matching%20guidelines.md
 
### Guidelines to FIPs for FI Request Validation for Fair Use Templates
 
**1. Consents Created Under Fair Use Limits:** Where a FIP chooses to validate FI Requests received from the AA, it should do so against the parameters of the applicable Fair Use Template, as set out in Table 3.
 
**2. Consents Created before Fair Use Adoption:** The FIP must not reject an FI Request received from the AA for a consent created prior to Fair Use adoption, provided the request conforms to the outer limits prescribed in Table for the applicable purpose code under https://github.com/Sahamati/fair-use-implementation-guidelines-for-aa/blob/v2.0/AAs%20-%20FI-Request%20Rules%20and%20Rule%20Matching%20guidelines.md
 
**3. Error Codes:** FIPs must provide deterministic rejection responses when validation fails, clearly indicating the error, using the error codes prescribed as under:
##### Error Responses
 
<table>
<thead>
<tr>
<th>Scenario</th>
<th>Response Code</th>
<th>Error Code</th>
<th>Error Message</th>
</tr>
</thead>
<tbody>
<tr>
<td>Missing, incomplete or invalid template link in refUri field</td>
<td>412</td>
<td>PreconditionFailed</td>
<td>Consent request rejected: Fair Use XML link in refUri is incorrect.</td>
</tr>
<tr>
<td>Any deviation in attributes in consent request/artefact</td>
<td>412</td>
<td>PreconditionFailed</td>
<td>Consent parameters are not as per fair use policy {Attribute name} is invalid.</td>
</tr>
<tr>
<td>Any deviation in attributes in consent request/artefact</td>
<td>412</td>
<td>PreconditionFailed</td>
<td>FI data range is not as per fair use policy.</td>
</tr>
</tbody>
</table>


 
---
