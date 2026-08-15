# GDPR Peer Audit
## Company Research Bot
### Independent First-Pass GDPR Compliance Assessment

**Auditor:** Marc Tanguy  
**Project Author:** Janaina Hoffmann  

---

# Executive Summary

This report presents an independent first-pass GDPR compliance assessment of the **Company Research Bot**, based solely on the Data Processing Brief provided by the project author.

The purpose of this review is to independently assess the system's personal data processing activities, identify potential GDPR compliance risks, and recommend appropriate remediation before any production deployment.

Based on the documentation provided, the system processes only a limited amount of personal data, primarily Telegram user identifiers that are required for message delivery. No customer records, employee information, behavioural profiles or special-category data are intentionally processed.

Overall, the system presents a relatively low GDPR risk. However, several organisational requirements expected under the GDPR have not yet been documented, including the lawful basis for processing, processor agreements with third-party vendors, international transfer safeguards and retention policies.

The overall recommendation is therefore:

> **Proceed with Conditions**

---

# Phase 1 – Read and Annotate

## Initial observations

After reviewing the Data Processing Brief, the following elements were identified as most relevant to the GDPR assessment.

### Personal data identified

- Telegram user ID
- Telegram chat ID
- Telegram message content
- Incidental references to company executives that may appear in public sources

### Potential special-category data

No special-category personal data is intentionally processed.

Based on the available documentation, the system searches company information rather than information about natural persons. The brief does not suggest any intentional processing of health, political, religious, biometric or other Article 9 data.

### International data flows

The documentation indicates that OpenAI processes requests in the United States.

The geographic location of Telegram, Tavily and n8n processing is not confirmed within the brief.

### Potential purpose limitation issues

No incompatible secondary use of personal data appears from the available documentation.

Telegram identifiers are used only to deliver the requested report back to the requesting user.

---

# Phase 2 – Personal Data and Role Map

## Personal Data Summary

| Data Category | Source | Purpose | Crosses EU Border? | Special Category? |
|--------------|--------|---------|-------------------|------------------|
| Telegram user ID | Telegram | Message routing | Potentially | No |
| Telegram chat ID | Telegram | Message routing | Potentially | No |
| Telegram message | User | Determine requested company | Yes (OpenAI) | No |
| Company name | User | Internet search | Yes | No |
| Public company information | Tavily search | Generate company report | Possibly | No |
| Incidental executive names | Public websites | Included only if present in search results | Unknown | No |

---

## Role Map

| Entity | GDPR Role | Processing Activity | DPA Needed? |
|---------|-----------|--------------------|------------|
| Future client / operator | Controller | Determines purposes and means of processing | Yes |
| Janaina Hoffmann (developer) | Processor during implementation / System developer | Develops and configures the application | Contract dependent |
| Telegram | Processor | Message delivery | Yes |
| OpenAI | Processor | Report generation | Yes |
| Tavily | Processor | Company search | Yes |
| n8n | Processor | Workflow automation | Yes |

---

## International Transfers

Based on the documentation reviewed, OpenAI processes requests within the United States.

The brief does not specify whether Standard Contractual Clauses, an adequacy decision or another transfer mechanism would apply.

No evidence is provided that international transfer requirements have been assessed.

---

# Phase 3 – Clarifying Questions Log

## Question 1

### Information requested

Does Telegram retain conversation history independently of the application?

### Why it matters

This affects retention obligations and the information that should be communicated through privacy notices.

### Provisional assumption

Telegram retains conversations according to its own platform policies.

---

## Question 2

### Information requested

Will the system ever allow users to search for natural persons instead of companies?

### Why it matters

Processing reports about identifiable individuals could substantially change both GDPR obligations and risk.

### Provisional assumption

The intended use remains limited to company research.

---

## Question 3

### Information requested

Will a production deployment use business accounts with Data Processing Agreements instead of personal accounts?

### Why it matters

Processor relationships require appropriate contractual arrangements under Article 28 GDPR.

### Provisional assumption

No DPAs currently exist because the project is an educational prototype.

---

# Phase 4 – Audit Report

## Section 1 – System Summary

The Company Research Bot is an AI-assisted research application that allows users to request a summary of a company through Telegram. After receiving a company name, the system searches publicly available information using Tavily, generates a report using OpenAI and returns the completed report to the user through Telegram.

The only clearly identified personal data processed by the system consists of operational Telegram identifiers associated with each request. The project intentionally avoids processing customer data, employee records or personal reviews.

---

## Section 2 – Data and Role Map

Based on the available documentation, the project processes a relatively small amount of personal data.

The future operator of the system would likely act as the controller, while OpenAI, Telegram, Tavily and n8n would operate as processors for specific processing activities.

The documentation identifies at least one international transfer involving OpenAI but provides no evidence that transfer mechanisms have been documented.

---

## Section 3 – Compliance Findings

### Finding 1 – Lawful Basis

**Severity:** Significant

**Description**

The documentation explains what personal data is processed but does not identify the lawful basis supporting each processing activity.

**Recommended action**

Document an Article 6 lawful basis for every processing purpose before production deployment.

**Escalation needed?**

Yes – Legal counsel or Data Protection Officer.

---

### Finding 2 – Processor Agreements

**Severity:** Significant

**Description**

The project currently operates through personal or educational accounts and no Data Processing Agreements have been established with third-party providers.

**Recommended action**

Execute appropriate Data Processing Agreements with all processors before processing personal data in production.

**Escalation needed?**

Yes – Legal counsel.

---

### Finding 3 – International Transfers

**Severity:** Significant

**Description**

The documentation identifies processing through OpenAI in the United States but does not identify any transfer mechanism supporting international data transfers.

**Recommended action**

Verify the applicable transfer mechanism and document compliance before deployment.

**Escalation needed?**

Yes – Data Protection Officer.

---

### Finding 4 – Retention Policy

**Severity:** Minor

**Description**

The project intentionally minimises data retention and states that reports are not stored after delivery. However, no documented retention policy exists for data held by third-party providers.

**Recommended action**

Document retention periods and clarify third-party provider retention practices.

**Escalation needed?**

No.

---

### Finding 5 – Data Subject Rights

**Severity:** Minor

**Description**

The brief does not describe how access, rectification or erasure requests would be managed if the project became operational.

**Recommended action**

Prepare basic procedures supporting data subject rights before deployment.

**Escalation needed?**

No.

---

## Section 4 – GDPR Obligations Checklist

| Obligation | Assessment | Notes |
|------------|------------|------|
| Lawful basis identified for each processing purpose | **Gap identified** | No lawful basis documented. |
| Purpose limitation respected | **Appears met** | Processing appears limited to fulfilling the requested company search. |
| Data minimisation | **Appears met** | Only operational identifiers appear to be processed. |
| Controller / processor roles mapped and DPAs in place | **Gap identified** | Roles can be inferred but DPAs are absent. |
| International transfer mechanism documented | **Gap identified** | No documented safeguard identified. |
| DPIA conducted if required | **Appears met** | Based on the available documentation, a DPIA does not appear to be required for this prototype. |
| Article 22 safeguards | **Appears met** | No automated decisions affecting individuals. |
| Privacy notice covers AI processing | **Cannot determine from brief** | No privacy notice described. |
| Data subject rights operationalised | **Cannot determine from brief** | No documented procedure provided. |

---

## Section 5 – Overall Recommendation

### Recommendation

**Proceed with Conditions**

### Rationale

The available documentation suggests that the Company Research Bot presents a relatively low privacy risk. Personal data processing is limited, the system does not profile individuals or make automated decisions, and data minimisation appears to have been considered during development.

Before any production deployment, however, several governance measures should be completed. These include documenting lawful bases, establishing Data Processing Agreements with third-party processors, confirming international transfer safeguards and documenting procedures supporting data subject rights.

None of these issues appear to require redesigning the system, but they should be addressed before real-world use.

---

## Section 6 – What this Report Is Not

This report represents an independent first-pass GDPR assessment prepared for educational purposes. It is **not** a legal opinion, a Data Protection Impact Assessment (DPIA) or a certification of GDPR compliance. Organisations should obtain legal advice before relying on this assessment for production deployment.

---

# Phase 5 – Debrief Conversation

This section should be completed after discussing the findings with the project author.

## Areas of agreement

_To be completed following the peer discussion._

---

## Areas of disagreement

_To be completed following the peer discussion._

---

## Comparison of lawful basis

_To be completed following the peer discussion._

---

## Comparison of DPIA assessment

_To be completed following the peer discussion._

---

## Comparison of identified gaps

_To be completed following the peer discussion._

---

## Joint Closing Note

_To be completed jointly after the debrief._

---

# Overall Conclusion

Based on the documentation reviewed, the Company Research Bot processes only a small amount of operational personal data and appears to follow data minimisation principles by design.

The principal GDPR risks are organisational rather than technical. Before production deployment, the project should establish documented lawful bases, execute appropriate processor agreements, verify international transfer safeguards and prepare procedures supporting data subject rights.

Overall, the system appears capable of achieving GDPR readiness with relatively modest governance improvements while maintaining its current technical architecture.
