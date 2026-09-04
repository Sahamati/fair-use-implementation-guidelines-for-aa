### Fair Use Registry in XML and JSON Structure
 
Every Fair Use Template published by Sahamati is available as a machine-readable XML document (and an equivalent JSON document) hosted on Sahamati's Library for Fair Use (Fair Use Registry - FUR). The FUR is the machine-readable counterpart to the Fair Use Template Library page on the Sahamati website. While the Library (https://sahamati.org.in/aa-fair-use-template-library/) is the human-readable reference, the Registry hosted at library.sahamati.org.in serves as the single source of truth for automated validation of consent parameters.
 
#### Canonical URL Format
 
To support this, every template in the Registry is addressed using a canonical URL format — a single, predictable path that uniquely identifies a template by its purpose code, template ID, and version, so ecosystem participants and automated systems can resolve the correct document deterministically rather than relying on a lookup or search step.
 
```
https://library.sahamati.org.in/{environment}/fairuse/purpose/{purpose_code}/template/{template_id}/version/{version}.xml
```
 
where,
 
- **environment**: either UAT or PROD to reflect the testing and production environment
- **purpose_code**: The ReBIT-specified Purpose Code (e.g., 101, 102, 103, 104, 105)
- **template_id**: The Sahamati Fair Use Template ID (e.g., CT001, CT003, CT004).
- **version**: The version number of the template (e.g., 1.0, 2.0).
A JSON equivalent is available at the same path with a `.json` extension.
 
#### XML Structure
 
Each Fair Use Registry page XML follows a defined structure. The XML must be used only as a validation reference layer, not a modification of, or substitute for, the ReBIT-defined consent artefact. This structure is modelled on the consent artefact as designed by ReBIT Specifications. Any additional elements appearing in this XML that are not part of the ReBIT consent artefact specification are included solely to enable FIUs, AAs, and FIPs to set validation rules against the attributes of a consent request and the respective Fair Use Template's upper bounds. In no way does Sahamati intend or recommend any change to the consent artefact structure as defined by the ReBIT specification.
 
The key elements are:
 
##### Table 1: Fair Use Template XML Structure
 
<table>
<thead>
<tr>
<th>Attributes</th>
<th>Format</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>fairUseTemplate (root)</strong></td>
<td>element</td>
<td>Root element wrapping the entire template.</td>
</tr>
<tr>
<td>&emsp;<strong>templateId</strong></td>
<td>string</td>
<td>The unique identifier for this Fair Use Template (e.g., CT001, CT003).</td>
</tr>
<tr>
<td>&emsp;<strong>version</strong></td>
<td>decimal</td>
<td>Version number of the template.</td>
</tr>
<tr>
<td>&emsp;<strong>effectiveDate</strong></td>
<td>Date (YYYY-MM-DD)</td>
<td>The date from which this template version is effective and can be referenced in consent requests.</td>
</tr>
<tr>
<td>&emsp;<strong>endDate</strong></td>
<td>Date (YYYY-MM-DD) or Blank</td>
<td>Blank for Active templates. Populated only when the template status is "Soon to be Deprecated" or "Deprecated", indicating the date after which this template should no longer be used.</td>
</tr>
<tr>
<td>&emsp;<strong>templateStatus</strong></td>
<td>enum: ACTIVE, SOON_TO_BE_DEPRECATED, DEPRECATED</td>
<td>One of three values:<br>Active (currently in use),<br>Soon to be Deprecated (will be retired, endDate indicates when), or<br>Deprecated (no longer valid for new consent requests).</td>
</tr>
<tr>
<td>&emsp;<strong>templateName</strong></td>
<td>string</td>
<td>A human-readable name for the use case (e.g., "Loan Underwriting", "Wealth Management Services").</td>
</tr>
<tr>
<td>&emsp;<strong>templateDetail</strong></td>
<td>string</td>
<td>Container for all consent parameters governing this template.</td>
</tr>
<tr>
<td>&emsp;&emsp;<strong>fetchType</strong></td>
<td>Enum: ONETIME, PERIODIC</td>
<td>Defines how data may be fetched under this template.</td>
</tr>
<tr>
<td>&emsp;&emsp;<strong>consentTypes</strong></td>
<td>array of enum: PROFILE, SUMMARY, TRANSACTIONS</td>
<td>The types of FI data the consent covers (e.g., PROFILE, SUMMARY, TRANSACTIONS). A template may list more than one.</td>
</tr>
<tr>
<td>&emsp;&emsp;<strong>purpose</strong></td>
<td>element</td>
<td>Container for the four parameters that make up the Purpose element as defined in ReBIT's consent artefact structure — code, refUri, text, and category.</td>
</tr>
<tr>
<td>&emsp;&emsp;<strong>purpose &gt; code</strong></td>
<td>integer (3-digit)</td>
<td>The ReBIT Purpose Code (e.g., 101, 102, 103, 104, 105).</td>
</tr>
<tr>
<td>&emsp;&emsp;<strong>purpose &gt; text</strong></td>
<td>string</td>
<td>The Purpose Text to be displayed to the customer. This is the agreed ecosystem text for the use case.<br>FIUs must display the exact purpose text as provided in the template to ensure uniform customer communication across the ecosystem. No customisation is allowed, as this text is designed to build trust and clarity.</td>
</tr>
<tr>
<td>&emsp;&emsp;<strong>purpose &gt; refUri<sup>1</sup></strong></td>
<td>string</td>
<td>Reference to the XML page that has further information about the purpose</td>
</tr>
<tr>
<td>&emsp;&emsp;<strong>purpose &gt; category</strong></td>
<td>string</td>
<td>Broad classification of the purpose (e.g., "Financial Reporting", "Personal Finance"), as defined by ReBIT at https://api.rebit.org.in/purpose. Must align with ReBIT classification as per purpose code</td>
</tr>
<tr>
<td>&emsp;&emsp;<strong>fiCategory (SEBI / NON-SEBI)</strong></td>
<td>element, name attribute: SEBI, NON-SEBI</td>
<td>Each template defines FI Types grouped into SEBI and NON-SEBI categories, each with its own FIDataRange upper bound. This replaces the separate FI Request rule tables from v1.0.</td>
</tr>
<tr>
<td>&emsp;&emsp;&emsp;<strong>fiCategory &gt; fiTypes</strong></td>
<td>array of enum:<br>SEBI — SIP, EQUITIES, MUTUAL_FUNDS, ETF, IDR, CIS, AIF, INVIT, REIT<br>NON-SEBI — DEPOSIT, TERM_DEPOSIT, RECURRING_DEPOSIT, INSURANCE_POLICIES, LIFE_INSURANCE, GENERAL_INSURANCE, NPS, GSTR1_3B</td>
<td>The list of specific FI Types permitted within that category.</td>
</tr>
<tr>
<td>&emsp;&emsp;&emsp;<strong>fiCategory &gt; fiDataRange</strong></td>
<td>element</td>
<td>Defines the permissible historical data window for that FI category against each of the SEBI and NON_SEBI FI Types</td>
</tr>
<tr>
<td>&emsp;&emsp;&emsp;<strong>fiCategory &gt; fiDataRange &gt; unit</strong></td>
<td>enum: DAY, MONTH, YEAR</td>
<td>The time unit the FI Data Range is measured in, specific to that FI category.</td>
</tr>
<tr>
<td>&emsp;&emsp;&emsp;<strong>fiCategory &gt; fiDataRange &gt; value</strong></td>
<td>Integer</td>
<td>The maximum FI Data Range allowed for that FI category, in the specified unit.</td>
</tr>
<tr>
<td>&emsp;&emsp;<strong>frequency</strong></td>
<td>element</td>
<td>Defines how often data may be fetched under a PERIODIC consent. Each XML will include this element, even with an empty <code>&lt;frequency/&gt;</code> with no unit/max, when fetchType is ONETIME.</td>
</tr>
<tr>
<td>&emsp;&emsp;&emsp;<strong>frequency &gt; unit</strong></td>
<td>enum: DAY, MONTH, YEAR</td>
<td>The time unit over which fetch frequency is measured, based on calendar timings (calendar day, calendar month, calendar year).</td>
</tr>
<tr>
<td>&emsp;&emsp;&emsp;<strong>frequency &gt; value</strong></td>
<td>integer</td>
<td>The maximum number of times data may be fetched within the specified unit period, applicable to PERIODIC fetch types.</td>
</tr>
<tr>
<td>&emsp;&emsp;<strong>dataLife</strong></td>
<td>element</td>
<td>Maximum data life, the window within which the FIU may process the data for the consented purpose.</td>
</tr>
<tr>
<td>&emsp;&emsp;&emsp;<strong>dataLife &gt; unit</strong></td>
<td>enum: DAY, MONTH, YEAR</td>
<td>The time unit for maximum data life.</td>
</tr>
<tr>
<td>&emsp;&emsp;&emsp;<strong>dataLife &gt; value</strong></td>
<td>integer</td>
<td>Maximum data life, the window within which the FIU may process the data for the consented purpose.</td>
</tr>
<tr>
<td>&emsp;&emsp;<strong>consentExpiry</strong></td>
<td>element</td>
<td>Maximum consent validity duration from consent start to consent expiry.</td>
</tr>
<tr>
<td>&emsp;&emsp;&emsp;<strong>consentExpiry &gt; unit</strong></td>
<td>enum: DAY, MONTH, YEAR</td>
<td>The time unit for consent validity.</td>
</tr>
<tr>
<td>&emsp;&emsp;&emsp;<strong>consentExpiry &gt; value</strong></td>
<td>integer</td>
<td>Maximum consent validity duration from consent start to consent expiry.</td>
</tr>
</tbody>
</table>
> <sup>1</sup> *Note: This refUri (within the FIU's consent request, Purpose block) is distinct from the refUri documented in of the Fair Use Template XML structure, which instead references ReBIT's purpose code definition. Both share the same field name per the ReBIT consent artefact structure, but FIU is expected to pass Canonical URL Format in the consent requests.*
 
An example of the XML structure described above is provided in Appendix 2. The JSON representation follows the same structure and conventions, and a sample JSON is provided in Appendix 3 for reference.
 
### Fair Use Registry URL Links
 
The XML is hosted on the public Fair Use Registry and is accessible to anyone, including customers and the public, ensuring full transparency of the agreed upper bounds for each use case.

##### Table: Fair Use Registry Links as on the date of this release:
 
<table>
<thead>
<tr>
<th>Sl.</th>
<th>Template ID</th>
<th>Version</th>
<th>Purpose Code</th>
<th>Use Case Category</th>
<th>Status</th>
<th>Purpose Text</th>
<th>XML URL</th>
<th>JSON URL</th>
</tr>
</thead>
<tbody>
<tr>
<td>1</td>
<td>CT001</td>
<td>1.0</td>
<td>103</td>
<td>Loan Underwriting</td>
<td>Active</td>
<td>To process borrower's (loan / credit card / credit line) application</td>
<td><a href="https://library.sahamati.org.in/PROD/fairuse/purpose/103/template/CT001/version/1.0.xml">XML</a></td>
<td><a href="https://library.sahamati.org.in/PROD/fairuse/purpose/103/template/CT001/version/1.0.json">JSON</a></td>
</tr>
<tr>
<td>2</td>
<td>CT003</td>
<td>1.1</td>
<td>104</td>
<td>Loan Monitoring</td>
<td>Active</td>
<td>To monitor the borrower's account to verify the repayment capability, subject to activation of (loan / credit card / credit line)</td>
<td><a href="https://library.sahamati.org.in/PROD/fairuse/purpose/104/template/CT003/version/1.1.xml">XML</a></td>
<td><a href="https://library.sahamati.org.in/PROD/fairuse/purpose/104/template/CT003/version/1.1.json">JSON</a></td>
</tr>
<tr>
<td>3</td>
<td>CT004</td>
<td>1.0</td>
<td>101</td>
<td>Wealth Management Services</td>
<td>Active</td>
<td>To provide (Wealth Management) / (Advisory) Services</td>
<td><a href="https://library.sahamati.org.in/PROD/fairuse/purpose/101/template/CT004/version/1.0.xml">XML</a></td>
<td><a href="https://library.sahamati.org.in/PROD/fairuse/purpose/101/template/CT004/version/1.0.json">JSON</a></td>
</tr>
<tr>
<td>4</td>
<td>CT006</td>
<td>1.0</td>
<td>103</td>
<td>Income Verification for Insurance Underwriting</td>
<td>Active</td>
<td>To verify the income as or on behalf of the insurer selected by the customer while underwriting a Life insurance policy</td>
<td><a href="https://library.sahamati.org.in/PROD/fairuse/purpose/103/template/CT006/version/1.0.xml">XML</a></td>
<td><a href="https://library.sahamati.org.in/PROD/fairuse/purpose/103/template/CT006/version/1.0.json">JSON</a></td>
</tr>
<tr>
<td>5</td>
<td>CT008</td>
<td>1.0</td>
<td>102</td>
<td>Personal Finance Management</td>
<td>Active</td>
<td>To generate insights based on your overall finances and provide incidental recommendations, if any</td>
<td><a href="https://library.sahamati.org.in/PROD/fairuse/purpose/102/template/CT008/version/1.0.xml">XML</a></td>
<td><a href="https://library.sahamati.org.in/PROD/fairuse/purpose/102/template/CT008/version/1.0.json">JSON</a></td>
</tr>
<tr>
<td>6</td>
<td>CT010</td>
<td>1.0</td>
<td>105</td>
<td>FNO Services Onboarding</td>
<td>Active</td>
<td>To assess genuineness and financial soundness of the customer for FNO services activation</td>
<td><a href="https://library.sahamati.org.in/PROD/fairuse/purpose/105/template/CT010/version/1.0.xml">XML</a></td>
<td><a href="https://library.sahamati.org.in/PROD/fairuse/purpose/105/template/CT010/version/1.0.json">JSON</a></td>
</tr>
<tr>
<td>7</td>
<td>CT019</td>
<td>1.0</td>
<td>102</td>
<td>Self Use consent on AA Apps</td>
<td>Active</td>
<td>To analyze and generate insights on your financial data for your personal use, presented through an analytics dashboard on the Account Aggregator app</td>
<td><a href="https://library.sahamati.org.in/PROD/fairuse/purpose/102/template/CT019/version/1.0.xml">XML</a></td>
<td><a href="https://library.sahamati.org.in/PROD/fairuse/purpose/102/template/CT019/version/1.0.json">JSON</a></td>
</tr>
<tr>
<td>8</td>
<td>CT035</td>
<td>1.1</td>
<td>104</td>
<td>Loan Monitoring for Collections</td>
<td>Active</td>
<td>To monitor a borrower's accounts for (loan / credit card / credit line) collection, in case of overdue payments</td>
<td><a href="https://library.sahamati.org.in/PROD/fairuse/purpose/104/template/CT035/version/1.1.xml">XML</a></td>
<td><a href="https://library.sahamati.org.in/PROD/fairuse/purpose/104/template/CT035/version/1.1.json">JSON</a></td>
</tr>
<tr>
<td>9</td>
<td>CT040</td>
<td>1.0</td>
<td>105</td>
<td>Financial Account Verification</td>
<td>Active</td>
<td>To verify (financial account type) account details for (activity/product)</td>
<td><a href="https://library.sahamati.org.in/PROD/fairuse/purpose/105/template/CT040/version/1.0.xml">XML</a></td>
<td><a href="https://library.sahamati.org.in/PROD/fairuse/purpose/105/template/CT040/version/1.0.json">JSON</a></td>
</tr>
<tr>
<td>10</td>
<td>CT042</td>
<td>1.1</td>
<td>104</td>
<td>Counterparty Risk Monitoring</td>
<td>Active</td>
<td>To monitor the counterparty risks of Recovery Agents / Sourcing Partners / Employees</td>
<td><a href="https://library.sahamati.org.in/PROD/fairuse/purpose/104/template/CT042/version/1.1.xml">XML</a></td>
<td><a href="https://library.sahamati.org.in/PROD/fairuse/purpose/104/template/CT042/version/1.1.json">JSON</a></td>
</tr>
<tr>
<td>11</td>
<td>CT043</td>
<td>1.0</td>
<td>104</td>
<td>Compliance Reporting of Employees</td>
<td>Active</td>
<td>To enable regulatory and internal compliance reporting of investment by employees and associated persons</td>
<td><a href="https://library.sahamati.org.in/PROD/fairuse/purpose/104/template/CT043/version/1.0.xml">XML</a></td>
<td><a href="https://library.sahamati.org.in/PROD/fairuse/purpose/104/template/CT043/version/1.0.json">JSON</a></td>
</tr>
<tr>
<td>12</td>
<td>CT045</td>
<td>1.0</td>
<td>105</td>
<td>Onetime Verification of Financial Condition</td>
<td>Active</td>
<td>Verification of financial condition of (Employees, Vendors and other third parties)</td>
<td><a href="https://library.sahamati.org.in/PROD/fairuse/purpose/105/template/CT045/version/1.0.xml">XML</a></td>
<td><a href="https://library.sahamati.org.in/PROD/fairuse/purpose/105/template/CT045/version/1.0.json">JSON</a></td>
</tr>
<tr>
<td>13</td>
<td>CT046</td>
<td>1.0</td>
<td>104</td>
<td>Government Scheme Beneficiary Monitoring</td>
<td>Active</td>
<td>To measure the efficacy and impact of government schemes</td>
<td><a href="https://library.sahamati.org.in/PROD/fairuse/purpose/104/template/CT046/version/1.0.xml">XML</a></td>
<td><a href="https://library.sahamati.org.in/PROD/fairuse/purpose/104/template/CT046/version/1.0.json">JSON</a></td>
</tr>
<tr>
<td>14</td>
<td>CT047</td>
<td>1.0</td>
<td>104</td>
<td>Monitoring by Credit Rating Agency</td>
<td>Active</td>
<td>To analyse the financials to assign and review the credit rating periodically</td>
<td><a href="https://library.sahamati.org.in/PROD/fairuse/purpose/104/template/CT047/version/1.0.xml">XML</a></td>
<td><a href="https://library.sahamati.org.in/PROD/fairuse/purpose/104/template/CT047/version/1.0.json">JSON</a></td>
</tr>
<tr>
<td>15</td>
<td>CT048</td>
<td>1.0</td>
<td>103</td>
<td>Priority Sector Loan Underwriting</td>
<td>Active</td>
<td>To process borrowers' Loan Application for Priority Sector loans or housing loan under IBA scheme for EWS, LIG and MIG categories</td>
<td><a href="https://library.sahamati.org.in/PROD/fairuse/purpose/103/template/CT048/version/1.0.xml">XML</a></td>
<td><a href="https://library.sahamati.org.in/PROD/fairuse/purpose/103/template/CT048/version/1.0.json">JSON</a></td>
</tr>
</tbody>
</table>
