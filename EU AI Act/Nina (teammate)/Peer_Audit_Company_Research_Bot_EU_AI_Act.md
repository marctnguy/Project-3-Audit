# EU AI Act Peer Audit
## Company Research Bot
### Independent First-Pass Compliance Assessment

**Auditor:** Marc Tanguy  
**Project Author:** Janaina Hoffmann 

---

# Executive Summary

This report presents an independent first-pass compliance assessment of the **Company Research Bot**, based solely on the system brief provided by the project author. The objective is to assess the system against the EU AI Act without reference to the author's own conclusions or self-audit.

Based on the available documentation, the system appears to fall outside both the prohibited practices listed in Article 5 and the High-Risk AI categories defined in Annex III. The system generates factual summaries about companies using publicly available information and does not make decisions or recommendations affecting natural persons.

Overall, the system is provisionally classified as a **Minimal Risk AI System**. Although no specific obligations under the AI Act appear to apply, some implementation details require clarification before this assessment could be considered final. Parallel legal considerations, particularly GDPR compliance due to Telegram identifiers and third-party processing, should also be considered if the system were deployed beyond a prototype.

---

# Phase 1 – Read and Annotate

## Initial observations

After reviewing the system brief twice, the following elements were identified as most relevant to the compliance assessment.

### Elements affecting risk classification

- The system generates factual company reports rather than making decisions or recommendations about individuals.
- No person is scored, ranked or evaluated.
- The workflow is fully automated from Telegram to report generation.
- Reports concern companies rather than natural persons.
- The intended use is informational rather than decision-making.

### Elements requiring clarification

Several implementation details are not described in the system brief and would require confirmation before issuing a final opinion.

- Whether conversation history is retained beyond operational messaging.
- Whether users could submit the names of natural persons instead of companies.
- Whether generated reports are stored after delivery.
- Whether the system would eventually become publicly available.

### Potential obligations identified

No High-Risk obligations appear to apply.

The project should nevertheless consider:

- Transparency regarding AI-generated content.
- General governance documentation.
- GDPR obligations arising from Telegram identifiers and third-party providers.

---

# Phase 2 – First-Pass Classification

## Classification

**First-pass AI Act classification:** **Minimal Risk**

The available documentation indicates that the Company Research Bot retrieves publicly available company information, generates a textual summary using a large language model and returns that summary to the requesting user. It does not perform prohibited AI practices under Article 5 and does not operate in any Annex III High-Risk sector.

The generated output is descriptive rather than predictive or evaluative, and no decisions affecting natural persons are made or supported. Consequently, based on the available information, no specific obligations under the AI Act appear to apply beyond general good governance practices.

---

## Risk Assessment

| Question | Assessment |
|-----------|------------|
| Does this system fall under any prohibited category (Article 5)? | No |
| Does this system operate in an Annex III High-Risk area? | No |
| If Annex III, does it significantly influence decisions? | Not applicable |
| Does this system interact with end users or generate content requiring Article 50 transparency? | Based on the available documentation, no specific Article 50 obligation appears to apply. |
| First-pass risk tier | **Minimal Risk** |
| One-sentence justification | The system generates factual summaries about companies and does not perform prohibited practices, operate in an Annex III sector or make decisions affecting natural persons. |

---

## Areas of uncertainty

This assessment is based exclusively on the system brief provided by the project author.

If the system were later expanded to evaluate people, make recommendations affecting individuals, or operate within a regulated sector, its classification would require reassessment.

---

# Phase 3 – Clarifying Questions Log

## Question 1

**Information requested**

Does the application permanently store Telegram messages, reports or user identifiers?

**Why it matters**

Persistent storage would introduce additional governance and potentially affect both AI Act documentation and GDPR obligations.

**Provisional assumption**

The information is processed transiently and is not stored beyond the operational messaging platform.

---

## Question 2

**Information requested**

Can users submit the names of identifiable individuals rather than companies?

**Why it matters**

Generating reports about natural persons could significantly change both the AI Act assessment and the project's GDPR obligations.

**Provisional assumption**

The intended use is limited to companies only.

---

## Question 3

**Information requested**

Is the project intended to remain an educational prototype or become a production service?

**Why it matters**

The deployment context affects governance expectations, provider responsibilities and operational controls.

**Provisional assumption**

The project remains a prototype developed for educational purposes.

---

# Phase 4 – Audit Report

## Section 1 – System Summary

The Company Research Bot is an AI-assisted research tool that allows users to request a summary of a company through Telegram. After receiving a company name, the system searches publicly available information using Tavily, generates a structured report with OpenAI and returns the report to the requesting user through Telegram.

The workflow is fully automated and no human reviews the generated report before delivery. The system's stated purpose is to provide a quick factual overview of companies rather than to support decisions about identifiable individuals.

---

## Section 2 – Risk Classification

Based on the documentation reviewed, the system is provisionally classified as **Minimal Risk** under the EU AI Act.

No prohibited practices under Article 5 are identified, and the system does not operate in any Annex III High-Risk domain. The generated reports concern companies rather than individuals and do not appear to influence decisions affecting legal rights or similarly significant interests.

The principal uncertainty relates to future deployment and possible expansion of functionality rather than the current implementation.

---

## Section 3 – Role Map

| Role | Entity | Key Responsibilities |
|------|--------|----------------------|
| Provider | Janaina Hoffmann | Responsible for developing the AI system and implementing appropriate governance before deployment. |
| Deployer | Future users or client organisation | Responsible for operating the system in accordance with applicable law and organisational policies. |
| Third-party AI provider | OpenAI | Provider of the underlying general-purpose AI model. |
| Technology vendors | Telegram, n8n, Tavily | Supporting infrastructure and communication services. |

---

## Section 4 – Compliance Findings

### Finding 1 – Governance documentation

**Severity:** Minor

**Description**

The available documentation clearly describes the system but does not indicate whether governance documentation would accompany a production deployment.

**Recommended action**

Prepare basic documentation describing intended use, known limitations and operational responsibilities before deployment.

**Escalation needed?**

No.

---

### Finding 2 – Transparency toward users

**Severity:** Minor

**Description**

Although the intended use of the system makes it apparent that AI is generating the report, the documentation does not indicate whether users are explicitly informed that the report is AI-generated.

**Recommended action**

Include a short disclaimer informing users that the report has been generated using AI and should be verified before relying upon it.

**Escalation needed?**

No.

---

### Finding 3 – Parallel legal considerations

**Severity:** Significant

**Description**

The system processes Telegram identifiers and relies on several third-party providers. While these issues do not appear to change the AI Act classification, they introduce GDPR considerations relating to personal data processing, processor agreements and international data transfers.

**Recommended action**

Perform a separate GDPR assessment before any production deployment.

**Escalation needed?**

Yes – Data Protection Officer or legal counsel.

---

## Section 5 – Overall Recommendation

### Recommendation

**Proceed with Conditions**

### Rationale

Based on the available information, no blocking AI Act compliance issues have been identified. The system does not appear to fall within any prohibited or High-Risk category and therefore does not trigger the extensive provider obligations associated with Annex III systems.

Before production deployment, the project should strengthen its governance documentation, clarify user transparency measures and complete a separate privacy assessment covering the processing of Telegram identifiers and the use of third-party service providers.

---

# Phase 5 – Debrief

This section should be completed after discussing the findings with the project author.

## Areas of agreement

_To be completed following the peer discussion._

## Areas of disagreement

_To be completed following the peer discussion._

## Additional information received

_To be completed following the peer discussion._

## Impact on assessment

_To be completed following the peer discussion._

---

# Overall Conclusion

Based solely on the documentation reviewed, the Company Research Bot appears to present a low regulatory risk under the EU AI Act. The project generates factual company summaries without evaluating individuals or supporting decisions within regulated sectors, making a **Minimal Risk** classification appropriate as a first-pass assessment.

The principal recommendations relate not to the AI Act itself but to general governance and parallel legal compliance. If the system evolves beyond its current educational scope or begins processing information about identifiable individuals, a new compliance assessment should be conducted before deployment.

---

# What this report is not

This report is an independent first-pass compliance assessment prepared for educational purposes. It is **not** a legal opinion, a conformity assessment or a certification under the EU AI Act. Any decision to deploy the system within the European Union should be supported by appropriate legal review and, where necessary, specialist regulatory advice.
