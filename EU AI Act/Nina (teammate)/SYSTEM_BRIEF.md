# System Brief — Company Research Bot

Simple description of my project, for someone who has never seen it before.

---

## What the system does

A person sends the name of a company in a Telegram message — for example,
"Adidas." Then, step by step, with no person checking anything in between:

1. Telegram gets the message and sends it to a tool called **n8n**.
2. n8n sends that message to my **Python** code (`api.py`).
3. My code uses a search tool called **Tavily** to look up real information
   about that company on the internet.
4. My code uses **OpenAI** to write a simple report using what it found
   (things like where the company is based, what industry it's in, and how
   much money it makes), and it lists where the information came from.
5. n8n sends that report back to the same person on Telegram.

This whole process takes about 20 seconds.

## What information it uses

| What it uses | Where it comes from | Is it personal data? |
|---|---|---|
| The company name (typed by the user) | The user types it in Telegram | No — it's about a company, not a person |
| Telegram user ID and chat ID | Added automatically by Telegram to every message | Yes — this shows who sent the message, but my code does not save it anywhere |
| Search results from the internet | The Tavily search tool | Usually no — just company facts (location, industry, revenue). Sometimes a company's website might mention a boss's name |
| — | — | The system does not use customer data, employee data, or people's opinions/reviews |

## What it gives back

**Just text** — a report about the company. It is not a score, and it does
not decide anything. It usually includes: a short summary, the industry, the
headquarters location, revenue, and the sources used.

## Who is affected by this report

- **The person who asked** — they get the report on Telegram.
- **The company being researched** — the report says facts about it, all
  taken from public information.
- No person is scored, judged, or picked out. The report is only about
  **companies**, not people.

## Does a person check the report before it is sent?

**No.** Everything happens automatically: Telegram → n8n → Python → back to
Telegram. Nobody reviews it first. The person who asked is the first one to
read it, and that happens only after it has already been sent.

## Who made it

I made it by myself, as a school project for Ironhack, with some help from
AI tools while coding. The tools I used: Python for the code, n8n to connect
everything, Telegram as the chat, Tavily to search the internet, and OpenAI
to write the report.

## Who would use it for real (in the future)

Right now, nobody else uses it — it's just me testing it to show my teacher.
Nobody has it connected for public use yet. If it became a real product,
anyone who wants a fast summary about a company (like before a meeting)
could use it — just by sending a message, with nobody checking it first.
