# Data processing brief — VR Competitive Intelligence Copilot

For a Data Protection Officer with no prior knowledge of this project. Factual
description of data flows only; it draws no conclusions about lawfulness, and
the author is not a lawyer. Companion to `docs/SYSTEM_BRIEF.md`.

---

## 1. What personal data the system processes

The system's *subject matter* is companies and software products, not people.
Personal data nevertheless enters through two doors.

### A. Third-party review content — the material category

Scraped at run time from G2, Capterra, Trustpilot and Reddit:

| Data | Example as it actually appears |
| --- | --- |
| Opinion text written by an identified person | *"Been on lodgify 3 months… Lodgify creates a multitude of problems as a host"* |
| Reviewer role and employer size | "Verified User in Real Estate — Small-Business (50 or fewer emp.)" |
| Pseudonymous usernames | Reddit account names on quoted threads |
| Date of the review | "1/28/2025" |
| Source URL | Links back to the review, and so to its author's profile |
| Commercial circumstances disclosed voluntarily | "we had reservations between $3k-$5k and lost hundreds of dollars" |

This is **text written by identifiable individuals about their working lives**.
It is pseudonymous rather than anonymous: a quote plus its source URL can lead
back to a profile. Reviewers are not customers, employees or contacts of the
operator — they are members of the public who published opinions on a review
platform.

### B. Requester identifiers — incidental

Slack delivers a user ID, channel ID and message timestamp with each question.
These stay inside the process and in Slack itself; see §4 for what is and is not
forwarded onward.

### C. Inferred attributes

The system derives, per quote and per vendor:

- a **criticism / not-criticism classification** of each review sentence
  (`reads_as_criticism`);
- an **attribution judgement** — whether a quote describes the vendor being
  researched (`names_another_vendor`);
- an aggregated **sentiment characterisation** per vendor.

These are inferences about *text and about companies*. No attribute is inferred
about the reviewer as a person, and reviewers are never grouped, scored or
profiled.

### D. Deliberately not processed

No customer records, no employee data, no contact details, no authentication
data, no special-category data is sought. Free-text reviews are uncontrolled
input, so a reviewer may have written anything — including health or other
sensitive detail — and the system has no filter that would detect it.

**Corpus note:** the vendor documentation corpus (1,241 local documents) is
product documentation, and support-agent bylines are stripped at ingest —
`import_scrape.py` removes Zendesk avatars and "X Team" bylines and Intercom
"Written by …" lines. Residual author names in body text are possible but not
systematically present.

## 2. Where the data comes from

| Source | Route | Consent |
| --- | --- | --- |
| Review platforms (G2, Capterra, Trustpilot, Reddit) | Scraped from public pages via Firecrawl, discovered via Tavily search | None sought. Reviewers published on those platforms under those platforms' terms; they did not submit anything to this system and are unaware of it |
| Vendor help centres and product pages | Scraped in advance, stored locally | N/A — corporate content |
| The requester | Types a question in Slack | Implied by using the tool |

**No data subject provided their data to this system directly, and none has a
relationship with its operator.** All review data is collected from third-party
platforms without notice to the individuals concerned.

## 3. What the data is used for — each purpose separately

1. **Evidence for a comparative report.** Review text is quoted verbatim in the
   Customer Sentiment section of a report about software vendors.
2. **Classification of that text** as criticism or praise, to prevent an
   all-positive report — an editorial-balance purpose.
3. **Attribution checking**, discarding quotes that describe a different
   product, to prevent misattribution.
4. **Aggregate characterisation** of a vendor's reception, combined with star
   ratings and review counts.
5. **Publication and retention** as an internal knowledge asset: reports persist
   in a Notion database and are intended to be read months later by people who
   did not commission them.
6. **Query interpretation** — the requester's question text is sent to a
   language model to extract which companies and topics are meant.

Not used for: training or fine-tuning any model, marketing, profiling
individuals, or contacting anyone.

## 4. Who processes it

| Processor | Role | What reaches it |
| --- | --- | --- |
| **This system** (local Python) | Collects, filters, classifies, assembles | Everything |
| **Tavily** (search) | Finds candidate pages | The *search query* only — e.g. "Lodgify reviews pros cons". No personal data outbound |
| **Firecrawl** (scraping) | Fetches pages on request | Outbound: a URL. **Inbound: the review text**, i.e. this is where personal data enters |
| **OpenAI** (language model) | Writes the report | The requester's question, plus the assembled evidence — **including the verbatim review quotes** |
| **OpenAI** (embeddings) | Semantic retrieval | The **vendor corpus only**, plus per-run query strings. Review text is never embedded — the vector store is built solely from `rag_index.json` |
| **Notion** | Storage and presentation | The finished report, quotes included. **This is the durable copy** |
| **Slack** | Question intake and link delivery | The question, requester identity, and a link. Report text is not posted back |

Two details worth noting because they narrow exposure:

- The Slack mention prefix (`<@U04ABCDEF>`) is stripped by `clean_question`
  **before** the text is sent to OpenAI, so the requester's user ID is not
  forwarded to the model provider.
- No run log, query log or analytics store is written to disk. Diagnostic output
  goes to the terminal and is ephemeral unless the operator redirects it.

**No data processing agreement has been executed with any of these providers.**
The system runs under individual accounts on standard terms as a personal
project. Provider-side retention (for example OpenAI's abuse-monitoring
retention) applies on default terms; no zero-retention or EU-residency option
has been requested or configured.

## 5. Where data is stored and processed

| Location | What | Region |
| --- | --- | --- |
| Operator's laptop | Vendor corpus (7.2 MB), retrieval index, 41.7 MB vector cache, `.env` credentials | Spain (EU), on one unmanaged personal machine |
| Notion | All published reports, indefinitely | US-hosted (Notion Labs, Inc.) |
| Slack | Questions, requester identity, delivered links | Workspace region depends on the workspace's plan and settings — **not verified for this project** |
| OpenAI | Transient processing of prompts | US |
| Tavily, Firecrawl | Transient processing of queries and fetches | US-based services; no region configured or verified |

So: **personal data collected in the EU is transmitted to and processed by US
providers**, with no transfer mechanism assessed by this project.

**Retention: none is defined.** Notion reports persist indefinitely with no
deletion policy; the local corpus and vector cache persist until manually
deleted. There is no mechanism to locate or delete a specific individual's quote
once it is published in a report, and **no process exists for handling an access
or erasure request** — a reviewer would have no way to know their words were
used.

## 6. Does the system make or assist decisions affecting people?

**No automated decision is made about any individual.** Nobody is scored,
ranked, filtered, flagged or subject to any consequence. Reviewers are quoted;
they are not assessed.

The system does **assist human decisions about companies**: which software to
buy, how to position a product against competitors. Those decisions affect
organisations and, indirectly, their staff and customers — but not the
identifiable individuals whose data is processed.

**No human reviews the output before it is published.** The report is written to
Notion and the link posted to Slack automatically, with no approval step. A
reader may check the sources afterwards; nothing requires it. A quote can
therefore be attributed to a vendor, published, and read by colleagues without
any person having verified that the attribution is correct — a failure mode
observed in practice, where a review of a different product was published as one
vendor's customer sentiment before the attribution checks in §3.3 were added.

## 7. Open points a DPO would need to resolve

Stated as facts, not conclusions:

1. No lawful basis has been identified or documented for processing the review
   content.
2. Data subjects receive no notice and have no practical route to object, access
   or erase.
3. No DPAs are in place with OpenAI, Tavily, Firecrawl, Notion or Slack, and no
   international-transfer mechanism has been assessed.
4. No retention limit exists at any layer.
5. Scraping is performed against platform terms of service that have not been
   reviewed.
6. Special-category data cannot be detected if a reviewer volunteers it.
7. The operator is a competitor of two of the assessed vendors, which is a
   fairness consideration for the individuals whose criticism of those
   competitors is selectively republished.
