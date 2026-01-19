## Fair Use Implementation Guidelines for FIPs (on Fair Use Enforcement)

Being the custodians of customer data integrity and security, **FIPs** have reserved the right to act as *second checkers* of incoming **Consent Requests** and **FI/Request**.

While **Account Aggregators (AAs)** serve as the **primary enforcers** of Fair Use compliance, FIPs may:

- Deploy internal rule engines to evaluate the parameters of incoming consent requests in real-time, checking them against the values defined in the **Fair Use Templates**.
- In the absence of a shared **Fair Use Template ID** in the consent request, adopt the same logic and rules as AAs to independently determine which template a request may correspond to.
- Block consent requests that do not comply with Fair Use templates and respond to the AA with a standardized error code:  
  **`412 — Precondition Failed`**
- Educate the end-user in a clear and customer-friendly way on **why their approved consent request could not be processed**.

This role as a **second checker** enables FIPs to reinforce Fair Use safeguards while protecting customer interests and maintaining ecosystem harmony.

Since Fair Use Template IDs are not passed in consent requests, FIPs are expected to follow the same Fair Use rules and matching logic as Account Aggregators (AAs) when evaluating incoming requests. By implementing internal rule engines, FIPs can assess requests in real-time, enforce boundaries defined in the templates, and block those that do not comply.

---

For reference, the same content is available in the Google Doc: https://docs.google.com/document/d/19cwoaZVvl-ULUKYpSW9NMj_tseiYC8NV0hm1fyjhQN0/edit?tab=t.0
