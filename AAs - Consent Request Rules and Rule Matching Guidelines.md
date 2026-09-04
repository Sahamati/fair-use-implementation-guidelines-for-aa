## Fair Use Implementation Rules for AAs
 
AAs are the primary enforcers of Fair Use within the ecosystem. In v2.0, the AA validation model shifts from inference-based rule matching to direct XML-based template validation using the Fair Use Registry. AAs must ensure that all consent requests and FI requests fall within the upper bounds set in the Fair Use Templates.
 
### Guidelines to AAs Consent Request Validation
 
For every consent creation request, the AA must:
 
**1. Extract Template Link:** On receiving a consent request, extract the refUri field from the Purpose block.
 
**2. Validate URL Format:** Verify the URL conforms to the canonical Fair Use Registry pattern at library.sahamati.org.in. Reject any request pointing to a different domain or a malformed URL. (refer to the validation rules table below)
 
**3. Fetch and Parse XML:** Fetch the XML from the Registry (caching is permitted with a maximum TTL of 24 hours). Parse to extract the template attributes and upper-bound parameters.
 
**4. Parameter-by-Parameter Validation:** Compare every consent parameter against the corresponding upper bound in the XML. If any parameter exceeds the bound, reject the request.
 
**5. Purpose Text Validation:** Validate that Purpose Text is populated and non-empty. For finalised templates, the AA should verify that the Purpose Text is semantically consistent with the Purpose Text prescribed in the template, and flag any material deviation for appropriate action.
 
**6. Pass-Through of Purpose refUri:** The AA must not edit or modify the refUri in any way. It is a pass-through attribute, similar to other attributes in the consent request. The FIP must receive the identical Registry URL that the FIU originally provided.
 
**7. Validation Rules for Consent Request received from FIUs:** AAs must validate each attribute in the following manner:
 
##### Table 3: Consent Request and Consent Artefact Validation rules
 
<table>
<thead>
<tr>
<th>Sl. no.</th>
<th>Parameter</th>
<th>Validation Rule</th>
</tr>
</thead>
<tbody>
<tr>
<td>1</td>
<td><strong>Purpose refUri</strong></td>
<td>i) Must be a well-formed URL matching the canonical Fair Use Registry pattern at library.sahamati.org.in.<br>ii) Must resolve to a templateId and version that are actually published and active in the Registry. Requests with a malformed URL, a URL pointing to a different domain, or a reference to a non-existent/deprecated template must be rejected before any further parameter validation is performed.</td>
</tr>
<tr>
<td>2</td>
<td><strong>Purpose Code</strong></td>
<td>Must match the purpose code in the XML URL path and the Purpose &gt; code element in the template.</td>
</tr>
<tr>
<td>3</td>
<td><strong>Purpose Text</strong></td>
<td>i) Must be non-empty.<br>ii) Should be semantically consistent with the template's Purpose Text.<br>iii) Purpose Text can include additional details such as loan product name, etc.; however, the intent cannot be modified.</td>
</tr>
<tr>
<td>4</td>
<td><strong>Fetch Type</strong></td>
<td>Must match the fetchType in the template (ONETIME or PERIODIC).</td>
</tr>
<tr>
<td>5</td>
<td><strong>Consent Expiry</strong></td>
<td>Duration from consentStart to consentExpiry must not exceed consentExpiry &gt; max in the template.</td>
</tr>
<tr>
<td>6</td>
<td><strong>Frequency</strong></td>
<td>i) Must match the unit of frequency as per the template.<br>ii) Value must not exceed the template ceiling.</td>
</tr>
<tr>
<td>7</td>
<td><strong>Data Life</strong></td>
<td>Duration of data life must not exceed the DataLife &gt; max value in the template.</td>
</tr>
<tr>
<td>8</td>
<td><strong>FI Types</strong></td>
<td>All requested FI Types must exist within the FICategory sections of the template.</td>
</tr>
<tr>
<td>9</td>
<td><strong>Consent Types</strong></td>
<td>All requested types (PROFILE, SUMMARY, TRANSACTIONS) must be within the consentTypes in the template.</td>
</tr>
<tr>
<td>10</td>
<td><strong>FI Types</strong></td>
<td>i) Each requested FI Type must exist within one of the fiCategory (SEBI or NON-SEBI) blocks declared in the template.<br>ii) The AA must identify which fiCategory the requested FI Type belongs to as part of this check, this determines the applicable FI Data Range ceiling below.</td>
</tr>
<tr>
<td>11</td>
<td><strong>FI Data Range</strong></td>
<td>i) For each requested FI Type, having identified its applicable fiCategory (SEBI or NON-SEBI) under the FI Types check above, the FI Data Range declared in the consent request (start to end) must not exceed the sum of the consent's validity duration and fiCategory &gt; fiDataRange &gt; max for that category in the template, i.e., the at time of consent creation, FI data range must span from (consent start minus max data range) to consent expiry.<br><br><em>Note: At the time of an actual data pull from FI Request, the data window requested must not itself exceed fiCategory &gt; fiDataRange &gt; max for that category, measured back from the pull date.</em></td>
</tr>
</tbody>
</table>

**8. Error Codes and Messages for Deviant Consent Request received from FIUs:** AAs must return standardised responses when a consent request does not fall within the agreed Fair Use upper bounds. The HTTP status code 412 – Precondition Failed must be used. These error codes are unchanged from v1.0. The {Attribute name} placeholder may be replaced with the specific parameter (e.g., Purpose, Frequency, Data Range). AAs may choose whether or not to include specific deviation details in the error message. The level of detail is left to the discretion of the AA, with the intent of assisting FIUs in identifying and correcting requests that exceed the upper bounds.
 
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

**9. Duplicate Active Consent Check:** The AA must not allow a new consent request where an active consent already exists for the same FIU, Purpose Code, Fair Use Template, and account(s). Such a request must be rejected until the existing active consent expires. (except in the case of CT001, CT003, CT035, which may result from multiple loans granted to the same customer by the same FIU).
