## Guidelines for AAs - Setting up a Rule Database for FI Request

AA must maintain a rule database for FI Requests to ensure compliance with the Fair Use Policy and meet the FIP-wise constraints around the maximum data range allowed in a single request.

### Fair Use Rule Set for FI / Request

| Purpose Code | FI Type      | Maximum FI Data Range | Maximum FI Data per Request |
|-------------|---------------|----------------------|--------------------------|
| 101         | SEBI FI Types | 20 years            | 2 years                  |
| 101         | Other FI Types| 13 months           | 13 months                |
| 102         | SEBI FI Types | 10 years            | 2 years                  |
| 102         | Other FI Types| 13 months           | 13 months                |
| 103         | DEPOSIT       | 24 months           | 24 months                |
| 103         | All FI Types  | 14 months           | 14 months                |
| 104         | All FI Types  | 6 months            | 6 months                 |
| 105         | All FI Types  | 1 day               | 1 day                    |

## Implementing Rule Matching Logic for FI Requests

### Rule Components
The system should match each FI Request against predefined rules using Purpose Code, FI Type, and maximum FI Data Range.

### SEBI FI Type Handling
For Purpose Codes 101 and 102, ensure that no single FI Request exceeds 2 years for SEBI FI Types, even if the overall limit allows more(due to the FIP implementation constraints as communicated to AAs).

### DEPOSIT FI Type Handling
For Purpose Codes 103, ensure that no single FI Request exceeds 24 months FI Type - DEPOSIT.

### Multiple FI Types
If multiple FIP IDs are in the same request, the system should apply the strictest FI Data Range applicable to SEBI and non-SEBI entities.

### Automatic Adjustments
If the requested FI Data Range exceeds the allowed limit, the system should adjust it to the maximum permissible range before forwarding to the FIP.

### Request Rejection
If an FI Request cannot be adjusted within the permissible range, it should be rejected to prevent policy violations.

### Consistency with Consent Artefact
Validate FI Requests against the original consent artefact issued to the FIP to ensure alignment.

### Wildcard Handling
Implement logic for wildcard (*) cases, where a rule applies universally to all requests matching certain criteria.

