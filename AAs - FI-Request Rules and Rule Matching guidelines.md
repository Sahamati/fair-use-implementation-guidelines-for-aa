### Guidelines to AAs for FI Request Validation for fair use templates
 
For every FI Request (data fetch), the AA must validate:
 
**1. Frequency:** Calendar-based time intervals only, e.g., if a "45 per month" consent is raised on 15th July, the 45 limit applies to the entire calendar month, and the counter resets to 0 at the start of each new month. Similarly, for "1 per day," the counter cannot start before the consent start date; only 1 data pull is allowed that day. This applies to all consents irrespective of the frequency given in the consent artefact.
 
**2. FI Data Range against FI Category:** The FI Data Range in the FI Request must not exceed the FIDataRange > max for the applicable FICategory in the template XML.
 
- **2.1.** If the request includes SEBI FI Types, the SEBI category's limit applies. If it includes NON-SEBI FI Types, the NON-SEBI category's limit applies.
- **2.2.** If a single FI Request includes both SEBI and NON-SEBI FI Types, the AA should apply the stricter (lower) of the two FI Data Range limits.
- **2.3.** If an FI Request exceeds the fair use data range it must be rejected

**3. Consents Created Under Fair Use Limits:** AAs validate the data request strictly as per the parameters of the consent artefact post roll out of v2.0 and ensure the data requests are well within the Fair Use limits.
 
**4. Consents Created Prior to Fair Use Adoption:** Where the FI Request is made under a consent that was created prior to v2.0 roll out or not in accordance with Fair Use Template upper limits, the AA must validate the request against the outer limits prescribed in for the applicable purpose code:

##### Maximum data request fair use limits by purpose codes
 
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

 
- **4.1.** The FI Request must not be made under a consent whose remaining validity extends beyond the earlier of (a) its own original expiry, or (b) the Maximum Consent Validity in Table 2, calculated from the date of v2.0 rollout.
- **4.2.** The frequency of data pulls must not exceed the Maximum Frequency in Table 2.
- **4.3.** The FI Data Range must not exceed the Maximum FI Range in Table 2.
- **4.4.** Any FI Request that does not conform to these limits given in the Table must be rejected.
