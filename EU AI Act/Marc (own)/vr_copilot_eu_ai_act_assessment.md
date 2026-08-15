# EU AI Act Compliance Assessment
## VR Competitive Intelligence Copilot
### Project 3 – First-Pass Compliance Review

---

# Executive Summary

This report provides a first-pass compliance assessment of the **VR Competitive Intelligence Copilot**, an AI system developed as Project 3 of this course. The objective is not to perform a formal legal conformity assessment, but to evaluate the system against the structure of the EU AI Act and identify practical compliance considerations before a hypothetical production deployment.

The assessment concludes that the system **does not fall under any prohibited practices (Article 5)** and **does not qualify as a High-Risk AI System under Annex III**. Instead, it is best classified as a **Limited Risk AI System**, primarily because it automatically generates analytical reports for human users using a large language model. Consequently, the principal obligations arise from the AI Act's transparency requirements, while GDPR and copyright considerations remain important parallel legal topics.

Although the project already incorporates several good governance practices—including confidence scores, explicit limitations, and source attribution—additional transparency measures and governance controls would strengthen its readiness for real-world deployment.

---

# Phase 1 – System Brief

## 1.1 What the system does

The VR Competitive Intelligence Copilot is an AI-powered internal research assistant designed to help Product Managers and Competitive Intelligence teams compare vacation rental software platforms.

A user submits a natural-language question through Slack—for example asking for a comparison between Lodgify, Guesty and Hospitable. The system automatically searches both an internal documentation corpus and live public web sources before generating a structured comparison report using a large language model. The finished report is published to Notion and shared back in the original Slack conversation.

The system is intended to reduce the manual effort required to perform competitive research while providing transparent references and confidence indicators for its conclusions.

---

## 1.2 Inputs

The system combines multiple sources of information during every execution:

- User questions submitted through Slack.
- A locally stored corpus of previously scraped vendor documentation.
- Live search results retrieved through Tavily.
- Live web pages scraped using Firecrawl.
- Public software reviews from websites including G2, Capterra, Trustpilot and Reddit.

Most inputs consist of publicly available information. However, user messages contain limited personal data (such as Slack user identifiers), while publicly available reviews may include usernames or other identifiable information posted by reviewers.

No internal customer data or special-category personal data is intentionally processed.

---

## 1.3 Outputs

The system produces a structured written report rather than an automated decision.

Each report includes:

- Executive summary
- Feature comparison
- Integration analysis
- Customer sentiment
- Recent product developments
- Strategic observations
- Confidence levels
- Sources and limitations

The reports include evaluative statements and recommendations but do not generate scores or make legally significant decisions.

---

## 1.4 Who is affected

The primary stakeholders include:

- Product Managers requesting competitive research.
- Other internal employees who later consult the generated reports.
- The software vendors discussed in the reports.
- Individuals whose publicly available reviews may be quoted.
- Indirectly, prospective customers if the research informs positioning or sales material.

No individual person is evaluated, scored or subjected to automated decision-making.

---

## 1.5 Human review

The current implementation operates automatically from end to end.

After a user submits a question, the report is generated, stored in Notion and shared through Slack without requiring human approval.

Human judgement exists only after publication. Users may review the cited sources and confidence indicators before relying on the report, but no mandatory review step currently exists.

---

## 1.6 Development and intended deployment

The prototype was developed by a single developer (Marc Tanguy) using Python together with several third-party services including OpenAI, Tavily, Firecrawl, Slack and Notion.

Although the system currently runs locally as a course project, its intended production users would be Product Managers, Product Marketing, Competitive Intelligence and Strategy teams inside a vacation rental software company.

---

# Phase 2 – Risk Tier Classification

## Classification

**First-pass AI Act classification:** **Limited Risk (Transparency Obligations)**

The system does not perform any prohibited AI practices under Article 5 and does not operate in any of the eight High-Risk sectors defined by Annex III.

Its purpose is to support internal market research by generating analytical reports for human users. It neither makes decisions affecting natural persons nor significantly influences decisions in regulated domains such as employment, education, healthcare, law enforcement or access to essential services.

However, because the system generates AI-created analytical content delivered directly to users, transparency obligations under Article 50 are likely to apply.

### Risk Assessment

| Question | Assessment |
|-----------|------------|
| Does this system fall under any prohibited category (Article 5)? | No |
| Does this system operate in an Annex III High-Risk area? | No |
| If Annex III, does it significantly influence decisions? | Not applicable |
| Does the system generate AI content for users? | Yes |
| First-pass risk tier | **Limited Risk** |
| Justification | The system generates AI-written reports but does not operate in a prohibited or Annex III high-risk domain. |

### Areas of uncertainty

This classification represents an initial compliance assessment rather than legal advice.

The precise scope of Article 50 transparency obligations depends on the final implementation and on whether users are sufficiently informed that the reports have been generated using AI.

---

# Phase 3 – Role Mapping

| Role | Entity | Key AI Act Responsibilities |
|------|--------|-----------------------------|
| Provider | Marc Tanguy (developer of the custom AI system) | Design the system responsibly, provide appropriate documentation, implement applicable transparency measures and support compliance before deployment. |
| Deployer | Product Management / Competitive Intelligence team using the system | Use the system according to instructions, exercise human judgement over outputs and implement internal governance procedures. |
| Third-party AI provider | OpenAI | Responsible for obligations applicable to the underlying General-Purpose AI model. |
| Technology vendors | Tavily, Firecrawl, Slack, Notion | Provide supporting infrastructure rather than the AI decision logic itself. |

Although OpenAI supplies the language model, the complete AI system assessed in this report is the orchestration developed for the project. The custom workflow determines what information is collected, how evidence is evaluated and how reports are generated.

---

# Phase 4 – Applicable Obligations

Because the system is **not classified as High Risk**, the provider obligations contained in Articles 9–15 and related conformity assessment requirements do not apply.

Instead, the relevant obligations concern transparency.

| Obligation | Status | Notes |
|------------|--------|------|
| Users informed that reports are AI-generated | Partial | Reports do not currently include an explicit AI-generated notice. |
| Transparency regarding limitations | Met | Confidence levels and limitations are already included. |
| Source attribution | Met | Reports provide references and supporting evidence. |
| Human judgement remains responsible | Partial | Users can review reports, but no governance guidance accompanies deployment. |

Additional legal frameworks remain relevant, particularly GDPR for processing publicly available personal data and copyright law for reproducing review excerpts.

---

# Phase 5 – Gap Analysis and Remediation

## Gap 1

**Obligation**

Transparency toward users (Article 50).

**Current state**

Users receive AI-generated reports without an explicit disclosure stating that the content has been generated by an AI system.

**Required state**

Users should be informed that the report has been generated using AI so they can interpret its conclusions appropriately.

**Remediation**

Add a standard notice at the beginning of every report explaining that the analysis was generated with AI assistance and should support—not replace—human judgement.

**Escalation required**

No.

---

## Gap 2

**Obligation**

Appropriate governance over AI outputs.

**Current state**

Reports are automatically published to Notion and shared in Slack without any review or approval stage.

**Required state**

Although the AI Act does not require mandatory human approval for this category of system, organisations should establish governance practices that reduce the risk of inappropriate reliance on AI-generated analyses.

**Remediation**

Introduce an optional review workflow, draft mode or approval mechanism before reports become visible to a wider audience.

**Escalation required**

No.

---

## Gap 3

**Obligation**

Compliance with parallel legal requirements (GDPR).

**Current state**

Public software reviews may contain usernames or other identifiable personal information which can be quoted inside generated reports.

**Required state**

Personal data should be processed lawfully, proportionately and only where justified.

**Remediation**

Implement data minimisation techniques such as removing usernames where unnecessary and establish documented retention and processing policies.

**Escalation required**

Yes.

**Responsible specialist**

Data Protection Officer or privacy counsel.

---

# Phase 6 – Compliance Memo

**To:** Head of Product

**Subject:** First-Pass EU AI Act Compliance Assessment – VR Competitive Intelligence Copilot

The VR Competitive Intelligence Copilot has been assessed against the EU AI Act as part of a preliminary compliance review.

Based on the current system design, the solution is best classified as a **Limited Risk AI System**. It does not perform prohibited AI practices under Article 5 and does not fall within any of the High-Risk application areas defined by Annex III. Instead, the primary regulatory consideration relates to transparency because the system automatically generates analytical reports using artificial intelligence.

From a governance perspective, the project already demonstrates several positive practices. Reports include confidence levels, limitations and supporting sources, helping users understand the evidence behind generated conclusions.

The assessment nevertheless identified three opportunities for improvement before any production deployment.

First, reports should explicitly disclose that they have been generated using AI. Second, although not legally required for this category of system, introducing an optional review or approval workflow would reduce the risk of inappropriate reliance on automatically generated analyses. Finally, because the system reproduces excerpts from publicly available reviews that may contain identifiable personal information, GDPR compliance should be reviewed alongside the AI Act assessment.

Overall, the system presents a relatively low regulatory risk under the AI Act. The recommended next steps are to strengthen transparency for end users, document internal governance practices and perform a separate privacy review before production deployment.

This document represents a first-pass compliance assessment only. It is **not** a legal opinion, a conformity assessment or a certification under the EU AI Act.

---

# Overall Conclusion

The VR Competitive Intelligence Copilot demonstrates that not every AI system falls into the High-Risk category under the EU AI Act. While the system uses advanced generative AI capabilities, its intended purpose—supporting internal competitive research—places it outside Annex III. The primary compliance focus should therefore be transparency, responsible governance and compliance with related legislation such as the GDPR.

Implementing the remediation actions described in this report would strengthen the system's readiness for deployment while improving user trust and regulatory preparedness.
