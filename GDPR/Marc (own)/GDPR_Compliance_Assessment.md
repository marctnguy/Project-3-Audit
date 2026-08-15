# GDPR Compliance Assessment
## VR Competitive Intelligence Copilot
### Project 3 – First-Pass GDPR Compliance Review

---

# Executive Summary

This report presents a first-pass GDPR compliance assessment of the **VR Competitive Intelligence Copilot**, the AI system developed as Project 3 during the AI Consulting Bootcamp.

Unlike the accompanying Data Processing Brief, which documents the system's data flows factually, this report evaluates those processing activities through the lens of the General Data Protection Regulation (GDPR). The objective is not to determine legal compliance definitively but to identify the principal compliance obligations, assess current gaps and recommend practical remediation before any production deployment.

The assessment concludes that the system processes a relatively limited amount of personal data compared with many enterprise AI applications. Nevertheless, several important GDPR accountability requirements are currently absent, including documented lawful bases, processor agreements, defined retention periods and documented procedures for responding to data subject rights.

Accordingly, the overall recommendation is:

> **Proceed with Conditions**

The system can likely be deployed only after appropriate contractual, organisational and governance controls have been implemented.

---

# Phase 1 – Personal Data Inventory

## Personal Data Inventory

| Data Category | Source | Purpose | Estimated Retention | Crosses EU Border? |
|--------------|--------|---------|--------------------|-------------------|
| Slack user ID | Slack | Process user requests | Slack retention policy | Potentially |
| Slack message content | User | Interpret research request | Temporary processing | Yes (OpenAI) |
| Review text | Public review platforms | Evidence for reports | Indefinite (Notion) | Yes |
| Reddit usernames | Reddit | Quote attribution | Indefinite | Yes |
| Reviewer role / employer size | Public reviews | Context for quotations | Indefinite | Yes |
| Review publication date | Public reviews | Source attribution | Indefinite | Yes |
| Review URLs | Public reviews | Source verification | Indefinite | Yes |

---

## Purpose Limitation Assessment

The project processes publicly available review content to generate comparative market intelligence reports.

Although the information is publicly accessible, it was originally published by reviewers for the purpose of sharing product experiences on third-party platforms rather than supporting an internal competitive intelligence system. This represents a secondary use of personal data and should therefore be assessed carefully under GDPR's purpose limitation principle.

No evidence suggests that review data is reused for unrelated purposes such as advertising, profiling individuals or model training.

---

# Phase 2 – Role Mapping

| Entity | GDPR Role | Processing Activity | DPA Status |
|---------|-----------|--------------------|-----------|
| Client organisation | Controller | Determines purposes and means of processing | Required |
| Marc Tanguy (developer) | Processor during implementation / Provider of the solution | Develops and configures the application | Would require contractual clarification |
| OpenAI | Processor (likely) | LLM inference | DPA required |
| Notion | Processor | Stores generated reports | DPA required |
| Slack | Processor | User interaction | DPA required |
| Firecrawl | Processor | Retrieves public webpages | DPA required |
| Tavily | Processor | Search queries | DPA required |

---

## International Transfers

Several service providers appear to process information outside the European Economic Area.

| Provider | Transfer |
|-----------|----------|
| OpenAI | United States |
| Notion | United States |
| Firecrawl | United States |
| Tavily | United States |
| Slack | Region not verified |

For production deployment, appropriate transfer mechanisms (for example Standard Contractual Clauses where applicable) should be confirmed.

---

# Phase 3 – Lawful Basis Assessment

| Processing Purpose | Proposed Lawful Basis | Justification | Legal Review |
|-------------------|----------------------|--------------|-------------|
| Interpret user requests | Contract / Legitimate Interests | Necessary to provide requested functionality | No |
| Search public review platforms | Legitimate Interests | Necessary for competitive intelligence research | Yes |
| Quote review content | Legitimate Interests | Supports evidence-based reporting | Yes |
| Generate comparative reports | Legitimate Interests | Legitimate business need | Yes |
| Store reports in Notion | Legitimate Interests | Internal knowledge management | Yes |

---

## Legitimate Interests Assessment

### Legitimate interest

The intended client has a legitimate commercial interest in monitoring competitors, understanding market perception and supporting product strategy through competitive intelligence.

### Necessity

The processing is broadly necessary to generate evidence-based reports. However, less intrusive alternatives should be evaluated, such as reducing the amount of verbatim personal data reproduced or minimising reviewer identifiers.

### Balancing Test

Reviewers voluntarily published their comments on public platforms, reducing their expectation of complete privacy. Nevertheless, the system republishes those comments in a different context without notifying the individuals involved.

Whether the organisation's interests outweigh the privacy impact requires legal assessment.

**Conclusion:** **TBD – Legal Review Required**

---

# Phase 4 – Risk and Rights Analysis

## Article 9 – Special Category Data

The system does not intentionally collect or process special-category personal data.

However, because review platforms contain unrestricted free text, reviewers may voluntarily disclose information relating to health, political opinions, religion or other protected characteristics. The current system contains no mechanism for detecting or filtering such disclosures before they are reproduced in generated reports.

Although no Article 9 processing is intended, this represents a residual compliance risk.

---

## Article 22 – Automated Decision-Making

The system does not make decisions about identifiable individuals.

It generates analytical reports concerning software vendors rather than evaluating natural persons. No individual is scored, ranked, accepted or rejected, and therefore Article 22 is unlikely to apply.

---

## DPIA Assessment

Applying the European Data Protection Board screening criteria suggests that a Data Protection Impact Assessment should be considered before production deployment.

Relevant criteria include:

- Innovative use of AI technology.
- Combination of multiple public datasets.
- International transfers.
- Large-scale automated retrieval of publicly available information.

Although the project does not involve automated decisions affecting individuals, a DPIA would provide stronger accountability before deployment.

---

## Data Subject Rights

| Right | Current Capability | Assessment |
|--------|-------------------|------------|
| Right of access | No process exists | Gap |
| Right to rectification | Manual only | Partial |
| Right to erasure | No deletion mechanism | Gap |
| Right to object | No process | Gap |
| Right to restriction | Not implemented | Gap |

Current documentation indicates that there is no operational process for responding to access or erasure requests.

---

# Phase 5 – Law Stacking Check

### AI Act

The accompanying AI Act assessment classified the system as **Limited Risk**, primarily due to transparency obligations associated with AI-generated reports.

The AI Act introduces transparency obligations that complement—but do not replace—the GDPR's requirements relating to lawful processing, accountability and data subject rights.

---

### ePrivacy

The project does not implement cookies, tracking technologies or device-level monitoring.

Slack messages are processed as part of the communication workflow rather than intercepted electronic communications.

No additional ePrivacy-specific obligations were identified for the current implementation.

---

### Data Act

Not applicable.

The system does not process connected-device data, IoT telemetry or cloud portability scenarios covered by the EU Data Act.

---

# Phase 6 – Compliance Memo

**To:** Data Protection Officer

**Subject:** Preliminary GDPR Compliance Assessment – VR Competitive Intelligence Copilot

A preliminary GDPR assessment has been conducted for the VR Competitive Intelligence Copilot, an AI-powered competitive intelligence system intended to assist Product Management teams with market research.

Based on the current implementation, my recommendation is **Proceed with Conditions**. Although the volume of personal data processed is relatively limited, several fundamental GDPR accountability requirements have not yet been implemented and should be addressed before production deployment.

The highest priority action is to establish appropriate contractual arrangements with every third-party processor involved in handling personal data, including OpenAI, Notion, Slack and other service providers. Secondly, the organisation should document and validate the lawful basis for each processing activity, including a Legitimate Interests Assessment where appropriate. Finally, governance procedures should be established for responding to data subject rights requests, together with defined retention periods for generated reports and supporting data.

Even after these measures are implemented, some residual risks remain. Publicly available review content may contain unexpected special-category information that the current system cannot detect automatically. Cross-border transfers to US-based providers require ongoing monitoring as contractual arrangements and regulatory guidance evolve. Finally, compatibility between the original purpose for which review content was published and its reuse in competitive intelligence reports should be reviewed with legal counsel.

This assessment represents a preliminary GDPR review only. It is **not** a legal opinion, a Data Protection Impact Assessment, or a certification of compliance. Formal legal advice should be obtained before relying on this assessment for production deployment.

---

# Overall Conclusion

The VR Competitive Intelligence Copilot processes relatively modest volumes of personal data, primarily through publicly available review content and operational identifiers associated with user requests.

From a GDPR perspective, the project's greatest risks do not arise from the AI itself but from organisational governance. The absence of documented lawful bases, processor agreements, retention schedules, international transfer assessments and procedures for exercising data subject rights represents the principal compliance gaps.

These issues are common for early-stage prototypes and are largely organisational rather than technical. Addressing them before deployment would significantly strengthen the system's overall GDPR readiness while improving accountability and demonstrating compliance with the Regulation's core principles.
