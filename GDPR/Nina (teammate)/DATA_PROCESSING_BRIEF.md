# Data Processing Brief — Company Research Bot

**Student:** Janaina Hoffmann
**Class:** W15D03
**Lab:** Audit your teammate's project — GDPR lens

This is a simple explanation of the data in my project. I made this so my
teammate can review it. I'm still a student, so this is not a legal
document, just an honest description of what my bot does with data.

---

## 1. What personal data my bot touches

My bot is about **companies**, not people. It barely touches any personal
data at all.

| Data | Where it comes from |
|---|---|
| Telegram user ID and chat ID | Telegram adds this automatically to every message, I don't ask for it |
| The company name someone types (like "Nike") | This is not personal data, it's just a company name |
| Company facts my bot finds online (location, industry, revenue) | Public company info, not personal data. Sometimes a source might mention a boss's name, but that's rare |

**That's basically it.** No customer info, no employee info, no reviews
written by real people, no passwords or login info.

## 2. Where the data comes from

| Source | How it gets in |
|---|---|
| The person using the bot | Types a message in Telegram |
| Company facts | Found live on the internet by my search tool (Tavily) |

Nobody sends personal data to my bot on purpose. The only personal detail
(the Telegram ID) is just something Telegram adds automatically, I don't
even use it for anything.

## 3. What I use the data for

1. **Reading the message** — to know which company to look up.
2. **Searching the internet** for facts about that company.
3. **Writing a report** — I use OpenAI to turn the search results into a
   simple summary.
4. **Sending the report back** to the same Telegram chat.

I don't use any of this for training an AI, ads, or anything else.

## 4. Who else touches the data

| Who | What they do | What they get |
|---|---|---|
| **My code** (Python) | Runs everything | Everything |
| **n8n** | Connects Telegram to my code | The message and the report pass through here |
| **Tavily** | Searches for the company | Just the company name |
| **OpenAI** | Writes the report | The company name plus search results |
| **Telegram** | Sends and receives messages | The user's ID and message text |

I don't have any signed data agreement with any of these tools. It's just a
school project, using free/personal accounts.

## 5. Where everything is stored

| Place | What's there | Where |
|---|---|---|
| My laptop | My code, nothing saved | Not checked |
| n8n | Just passes messages through, doesn't save anything | Not checked |
| Telegram | Keeps the chat history on its side | Not checked |
| OpenAI | Processes the request | US |
| Tavily | Processes the search | Not checked |

**I don't keep anything.** I don't save reports anywhere — once it's sent
back to Telegram, my code forgets about it.

## 6. Does my bot decide anything about people?

**No.** It doesn't score or judge anyone. It just writes facts about a
**company**. Whoever reads the report might use it to make a decision, but
my bot itself doesn't decide anything.

**Nobody checks the report before it's sent.** It's all automatic:
Telegram → n8n → my code → back to Telegram.

## 7. Things I still need to figure out

Just being honest here:

1. I never wrote down a legal reason for using the Telegram ID, even though
   it's a tiny amount of data.
2. I don't have any data agreements with n8n, Telegram, OpenAI, or Tavily.
3. I never set a rule for how long anything is kept.
4. This is just a demo for school, not something real people use yet.
