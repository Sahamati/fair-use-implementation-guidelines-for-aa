# Fair Use Implementation Guidelines for AA Ecosystem

## Introduction

The Fair Use Implementation Guidelines for the AA Ecosystem serve as a shared reference point for participants in the Account Aggregator (AA) ecosystem — including Account Aggregators (AAs), Financial Information Providers (FIPs), and Financial Information Users (FIUs). These guidelines promote responsible data sharing practices while maintaining user trust, regulatory compliance, and ecosystem-wide consistency.

The guidelines define upper bounds for data collection and storage through pre-agreed Fair Use templates, which specify limits on parameters such as purpose, frequency, validity, consent type, and data range. They were developed through participatory governance, with active involvement from industry stakeholders via Use Case Councils and the Fair Use Committee.

Each participant of the AA ecosystem plays a distinct and complementary role in enforcing Fair Use:

- **Financial Information Users (FIUs):** FIUs are expected to initiate consent and data requests strictly within the boundaries defined by Fair Use templates. Please note that Fair Use templates are not regulatory advice, but ecosystem-wide guidelines. FIUs must also ensure that their practices remain compliant with laws such as the RBI’s Master Directions on NBFC-AA and the DPDP Act.

- **Account Aggregators (AAs):** AAs are the primary enforcers of Fair Use. They validate whether incoming consent and data requests comply with published Fair Use templates.

- **Financial Information Providers (FIPs):** FIPs are the custodians of customer data and may act as a second line of enforcement.

This dual-layered enforcement — at both AA and FIP ends — enhances trust and reliability in the system.

Sahamati will continue to evolve the Fair Use framework by adding new templates, revising existing ones based on feedback or regulatory developments, and publishing clarifications and FAQs to support adoption.

# Fair Use Implementation Guidelines for AAs

This repository contains the **Fair Use Implementation Guidelines** prepared in collaboration with [Finvu AA](https://finvu.in/) to help standardize the implementation of the fair use templates published by [Sahamati](https://sahamati.org.in/aa-fair-use-template-library/), which were finalized by the council of FIUs under the [Fair Use Framework](https://sahamati.org.in/aa-fair-use-committee/).

The guidelines are based on the **default rule with exceptions**, where rules are applied to all FIUs by default based on Purpose Code. On an exception basis, new rules are applied to a specific set of FIUs where more than one fair use template is assigned to a Purpose Code. This ensures that Consent Requests and FI Requests adhere to the upper bounds set for various consent attributes as per the Fair Use Template Library.

## Repository Files for AAs
1. [Implementation Guidelines](Implementation%20Guidelines.md)
2. [Consent Request Rules and Rule Matching Guidelines](Consent%20Request%20Rules%20and%20Rule%20Matching%20Guidelines.md)
3. [FI-Request Rules and Rule Matching Guidelines](FI-Request%20Rules%20and%20Rule%20Matching%20Guidelines.md)
4. [Error Codes and Messages for Deviant Transactions](https://github.com/Sahamati/fair-use-implementation-guidelines-for-aa/blob/main/AAs%20-%20Fair%20Use%20Implementation%20Guidelines.md#error-codes-and-messages-for-deviant-transactions)
5. [Monthly Fair Use Reporting by AAs – Guidelines on Data Collation](https://github.com/Sahamati/fair-use-implementation-guidelines-for-aa/blob/main/AAs%20-%20Fair%20Use%20Implementation%20Guidelines.md#error-codes-and-messages-for-deviant-transactions)

### Fair Use Implementation Guidelines for FIUs
FIUs must initiate consent and data requests within the boundaries defined by Fair Use templates published by Sahamati. These templates set upper limits for parameters like purpose, frequency, and data range to ensure responsible data access and ecosystem consistency.

## Repository Files for FIUs
FIUs - Fair Use Implementation Guidelines(https://github.com/Sahamati/fair-use-implementation-guidelines-for-aa/blob/main/FIUs%20-%20Fair%20Use%20Implementation%20Guidelines.md)

### Fair Use Implementation Guidelines for FIPs
FIPs may act as a secondary layer of enforcement for Fair Use compliance by following the same rules as AAs, validating consent and data requests against Fair Use templates. Since Fair Use Template IDs are not passed in consent requests, FIPs are expected to follow the same Fair Use rules and matching logic as Account Aggregators (AAs) when evaluating incoming requests.

## Repository Files for FIPs
[FIPs - Fair Use Implementation Guidelines.md](https://github.com/Sahamati/fair-use-implementation-guidelines-for-aa/blob/main/FIPs%20-%20Fair%20Use%20Implementation%20Guidelines.md)
