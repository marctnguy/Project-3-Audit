# System brief — VR Competitive Intelligence Copilot

For an external reviewer who has not seen this system before. Plain description,
no claims about quality.

---

## What the system does

A person types a question in Slack — for example *"compare OTA integrations
across Lodgify, Guesty and Hospitable"*. The system then, with no further human
involvement:

1. Reads the question with a language model and extracts which companies and
   which topics it concerns.
2. Searches a local library of previously scraped vendor documentation.
3. Searches and scrapes the live web: vendor product pages, pricing pages,
   changelogs, and public software-review sites.
4. Passes the collected material to a language model, which writes a structured
   comparison report.
5. Publishes that report as a page in a Notion database and posts the link back
   into the Slack thread where the question was asked.

A run takes roughly three to fourteen minutes depending on the question. The
subject matter is vacation-rental property management software; three vendors
are currently supported.

## What inputs it takes

| Input | Source | Personal data? |
| --- | --- | --- |
| The question, in free text | Slack message, or a command line | The Slack message carries the asker's user ID, channel ID and timestamp |
| Vendor documentation corpus — 1,241 markdown documents, 6,522 passages | Scraped in advance from three vendors' public help centres and product pages | No. Third-party **copyrighted** material, held locally |
| Live search results | Tavily search API | No |
| Live page content | Firecrawl scraping of vendor sites, pricing pages, changelogs | No |
| Public software reviews | G2, Capterra, Trustpilot, Reddit — scraped at run time | **Yes.** Review text written by identifiable or pseudonymous individuals, sometimes with employer size, job function or Reddit username attached |

No internal company data, customer records, or employee data is used. No
special-category data is deliberately collected, though free-text reviews are
uncontrolled input and may contain anything a reviewer chose to write.

## What it outputs

**Generated text**, not a score or a machine-readable decision. A report of up to
nine sections: executive summary, company overview, feature comparison, OTA
integration matrix, customer sentiment, recent product developments, strategic
observations, limitations, sources.

Within that text the system does make **evaluative judgements**, and a reviewer
should treat these as the real output:

- Comparative verdicts about named companies — "Guesty has the broadest
  documented channel coverage", "Lodgify's messaging is the most beta-led".
- Buyer recommendations — "choose Hospitable if you want automation-first".
- A pricing comparability verdict, computed rather than written: whether the
  vendors' prices can be ranked at all.
- Confidence labels per topic (none / low / moderate) and an explicit
  limitations section.
- Verbatim quotes from named review sites, attributed to a vendor.

Delivery is a Notion page plus a Slack message containing the link.

## Who is affected by the output

- **The person who asked** — receives the report and may act on it.
- **Colleagues who read it later.** Reports accumulate in a shared Notion
  database, so a report outlives the question and may be read by people with no
  knowledge of how it was produced.
- **The three named vendors.** The system publishes evaluative and comparative
  claims about identifiable companies. Two of them are direct competitors of the
  organisation the builder works for; the third is that organisation itself. A
  reviewer should note that the system assesses its operator alongside its
  operator's competitors.
- **Individual reviewers whose words are quoted.** Their published complaints
  are extracted, attributed and republished into an internal system, without
  their knowledge, in a context they did not write for.
- **Indirectly, buyers.** If the reports inform positioning or sales enablement,
  claims about competitors may reach prospective customers second-hand.

No individual is scored, ranked, or subject to an automated decision. The
subjects of assessment are companies and products.

## Is there human review before action?

**No human reviews the report before it is published.** The pipeline runs
end to end: the report is written to Notion and the Slack link is posted
automatically. There is no approval step, no draft state, and no sign-off.

What review exists is **after publication and entirely optional**. The reader may
open the Notion page, read the limitations section, and follow the source links
listed at the bottom. Nothing requires them to. A reader who reads only the
executive summary — which is the shortest and most prominent section, and is
written to be read alone — sees verdicts without seeing what they rest on.

The system is designed to make that easier rather than to enforce it: every
topic carries a stated confidence level, unread sources are declared as
collection failures rather than findings, and sources are listed with links. But
these are prompts to a human's judgement, not controls on it.

There is a `--dry-run` mode that runs the pipeline and publishes nothing. It is
a development convenience, not a review gate.

## Who built it

Built by one person — Marc Tanguy — as an individual course project, with AI
coding assistance. It is custom Python (~10,700 lines across 16 test files and
242 tests), not a configured off-the-shelf product.

It composes third-party services that were **not** built by the author and are
used as-is: OpenAI (language model and text embeddings), Tavily (search),
Firecrawl (page scraping), Notion and Slack (delivery), plus open-source
libraries including LangGraph, numpy and slack_bolt. The judgement logic —
what counts as evidence, what may appear in which section, how criticism is
identified, how quotes are attributed — is the author's own code, not the
model's.

## Who would use it in production

Not currently in production. It runs as a single local process on the builder's
machine, connected to one Slack workspace, and stops when that machine sleeps.

The intended users, from the original project plan, are **Product Managers** at a
vacation-rental software company, with secondary users in Product Marketing,
Strategy and Competitive Intelligence, Customer Success leadership, and Sales
Enablement. The intended pattern is self-service: any of those people ask a
question in a shared Slack channel and receive a report, with no gatekeeper
between the question and the published answer.
