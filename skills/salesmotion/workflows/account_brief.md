# account_brief

A one-page brief you can read in two minutes before a call. Tight, current, and focused on what changed and what to say.

## Inputs

Required (take from the user's message):
- `company` — Company name or domain

Optional modifiers (apply only if the user mentions them, otherwise use the defaults built into the workflow):
- `context` — Optional: why you need the brief (e.g. 'discovery call', 'renewal', 'cold outreach')

## Workflow

Follow this exactly, using the Salesmotion connector's tools by the names given.

Write a one-page account brief on <the company the user named>.

## Gather

1. account_insights with query="<the company the user named>" — pull the summary and value sections.
If account_insights returns not_found or multiple_matches:
- multiple_matches: re-call account_insights with the accountId of the best match.
- not_found: the company may not be in the account list, or this may be an API-only organization.
  Fall back to get_company with input=<domain> and build from the company sub-resource tools
  (get_company_news, get_company_jobs, get_company_earnings_calls, get_company_filings).
  Say clearly which path you used, because the depth of the answer depends on it.
2. get_signals — the 5 most recent signals only. Recency matters more than volume here.
3. get_contacts — top 5 by score.

Evidence rules:
- Attribute every material claim to what produced it: a signal, an earnings call, a filing, a job posting, or a news article. Include dates.
- Quote executives verbatim when you have their words. Paraphrased strategy is weak; quoted strategy is credible.
- If something is unknown, write "Not available in Salesmotion" and list it as an open question. Never fill a gap with a guess.
- Separate what the data says from what you infer. Label inferences as hypotheses.
- Contacts are the people this organization tracks, not the full org chart. If a role that matters (CEO, CFO, CRO, the economic buyer)
  is missing from get_contacts, search get_signals and get_company_news for the title and for recent leadership changes, name the person
  from that source with its date, and mark them "not yet a tracked contact". Never report a role as vacant or a person as unknown
  only because the contact search came back empty.

## Deliver

Keep the whole thing under 400 words. A brief that takes ten minutes to read is not a brief.

**The one-liner** — what this company does, in a single sentence a colleague would understand.

**Why now** — the single most compelling recent development, with its date and source. If nothing recent
is compelling, say so plainly rather than inflating something minor.

**Three things to know** — the facts that would embarrass you not to know on this call.

**Who you are talking to** — names, titles, and one relevant detail each.

**Two openers** — specific, non-generic conversation starters anchored to real events. No flattery, no
"I saw you're growing fast". Reference something concrete enough that it could only apply to this company.

**One question worth asking** — a question that earns a real answer and moves the conversation forward.

Presentation rules (for any output longer than a short message; skip them for an email or DM draft):
- Open with a three-line bottom line: the situation, the opportunity, the next move. No preamble before it.
- Use a table wherever items share attributes: stakeholders (name, title, role in the deal, evidence), SWOT (a 2x2),
  objectives (metric, target, date), actions (owner, action, date), signals (date, type, what it means).
- Keep prose to short paragraphs of at most three sentences. One idea per bullet, no nested bullets.
- Put the source and date in the same row or line as the claim, not in a block at the end.
- Bold only the few phrases a reader skimming for 20 seconds must see. No emoji, no decorative dividers.
- If you can produce a formatted document or artifact, deliver the full output there and keep the chat reply to the bottom line.
