### Background and Context for Fair Use Implementation Rules
 
The Fair Use implementation rules have played a critical role in sensitising FIUs to the use of fair use templates and enabling consistent enforcement across the Account Aggregator (AA) ecosystem. Data shared by AAs indicates that Fair Use templates were adopted across FIUs, reflecting ecosystem-wide alignment and operational stability. However, as adoption has scaled and more use cases have become prevalent, certain structural limitations have emerged in the current implementation model, particularly where multiple Fair Use templates exist under the same Purpose Code.
 
Based on the AA Council and Fair Use Committee, it is recommended that FIUs explicitly include the Fair Use Template ID in the consent initiation request, using the `refUri` field. Consequently, this document covers Fair Use Implementation Rules v2.0, including an explicit mechanism to identify the Fair Use Template used by the FIU, with the reference provided in the `refUri` field of the consent request. This approach aligns with ReBIT expectations, which allow FIUs to provide a URL to additional information explaining the purpose or use case. The purpose refURI will indicate which Fair Use Template is being implemented by FIUs, allowing AAs and FIPs to validate against the declared template.
 
**These rules are intended to supersede and deprecate the existing Version 1x of Fair Use Implementation Rules.**
 
### Scope of the Document
 
This document sets out the **Adoption Guidelines for Fair Use Implementation Rules v2.0**, including scope and entity-specific obligations for FIUs, AAs, and FIPs. Compared to v1.0, where Fair Use Guidelines were published as separate documents for FIUs, AAs, and FIPs, v2.0 consolidates them into a single unified document that provides an end-to-end view while clearly identifying the responsibilities of each participant role.
 
Fair Use Implementation Rules v2.0 introduce explicit identification of the use case with a combination of Purpose Code and Fair Use Template via the refUri field, enabling deterministic validation and removing ambiguity arising from multiple templates under a single Purpose Code.
 
<table>
<thead>
<tr>
<th>Aspect</th>
<th>v1.0 (Previous)</th>
<th>v2.0 (This Document)</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>Document Structure</strong></td>
<td>Separate documents per role plus separate rule-set files</td>
<td>Single unified document covering all three roles, with appendices</td>
</tr>
<tr>
<td><strong>Template Identification</strong></td>
<td>Inferred by AA via Purpose Code + wildcard matching; Template ID not shared with FIPs</td>
<td>FIU declares explicit Registry XML link in consent request; AA forwards to FIP as-is</td>
</tr>
<tr>
<td><strong>Validation Method</strong></td>
<td>AA maintains internal rule database; FIPs replicate AA logic independently</td>
<td>AA and FIP both validate directly against the XML from the Fair Use Registry</td>
</tr>
<tr>
<td><strong>FI Data Range by FI Category</strong></td>
<td>Separate rule tables for SEBI vs non-SEBI FI Types per Purpose Code</td>
<td>SEBI and NON-SEBI FI categories with their FI Data Range are embedded directly in each XML template</td>
</tr>
<tr>
<td><strong>Purpose Text</strong></td>
<td>Recommended but not strictly enforced at validation layer</td>
<td>Expected to be present for all templates</td>
</tr>
<tr>
<td><strong>Template Discovery</strong></td>
<td>Templates available on website but no machine-readable links</td>
<td>Fair Use Registry introduced at library.sahamati.org.in; XML and JSON Link columns added to the Library table</td>
</tr>
</tbody>
</table>
These guidelines are issued to ensure uniform adoption, orderly transition, and predictable enforcement across the AA ecosystem.

## Fair Use Template Library and Registry - Discovery and Access
 
### Fair Use Template Library Web Page
 
**1. Access:** All published Fair Use Templates are listed in the Fair Use Template Library on the Sahamati website at: https://sahamati.org.in/aa-fair-use-template-library/. This page contains the master table listing every Fair Use Template finalised by the User Councils and Fair Use Committee. The Library table now includes two new columns, XML Link and JSON Link, pointing to the corresponding entries in the Fair Use Registry at library.sahamati.org.in. FIUs, AAs, and FIPs can directly copy the correct Registry URL for their use case from this table.
 
**2. How to Discover the Correct Template URL:**
 
**2.1.** **Visit** the Fair Use Template Library: Navigate to https://sahamati.org.in/aa-fair-use-template-library/
**2.2.** **Identify Your Use Case:** Locate the row matching your Purpose Code and use case description. For Purpose Codes with multiple templates (e.g., 104 with Loan Monitoring and Loan Monitoring for Collections), select the correct one.
**2.3.** **Copy the XML Link:** Use the XML link from the corresponding column. Place it in the refUri field of the consent request. It must be XML and not JSON.
**2.4.** **Optionally Use JSON:** If your internal systems prefer JSON for rule-engine integration, use the JSON link for programmatic access (but not inside the purpose block).

**3. Programmatic Access to the Fair Use Registry**
 
**3.1.** FIUs, AAs, and FIPs should not pull the Fair Use Registry URLs more than once per 24-hour period. Templates change only when the Fair Use Committee finalises revisions. Excessive pulling creates unnecessary traffic and may result in rate-limiting.
**3.2.** Cache XMLs / JSONs locally in your validation engine for the next 24 hours.
**3.3.** Use the cached version for all real-time consent request validations during the day. On the next pull, compare with the cached version. If changed (version incremented, parameters updated), update the cache and log for audit.
**3.4.** Do NOT fetch the XML/JSON on every incoming consent request. This is unnecessary and generates excessive traffic.

**4. Availability and Support:** The Fair Use Registry XML and JSON endpoints at library.sahamati.org.in are designed to be available 24 hours a day, 7 days a week. In the event of unavailability:

**4.1.** Use cached version: If you followed the daily-pull approach, validate against the cached copy until the endpoint is restored.

**4.2.** Do not reject due to outage: Consent requests should not be rejected because of a temporary Registry outage if a cached copy is available.

**4.3.** Report the issue: If the Registry endpoints are unreachable or returning errors, contact Sahamati promptly at techsupport [at] sahamati.org.in, cc'ing fairuse [at] sahamati.org.in, include: the exact URL that failed, the HTTP status code or error received, the timestamp, and your entity ID. Sahamati will acknowledge and work to resolve on priority.

PDF Copy of the Guidelines is available on Sahamati website: https://sahamati.org.in/aa-fair-use-template-library/
