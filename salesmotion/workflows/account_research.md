# account_research

Deep-dive research on a company: full account intelligence, recent buying signals, key contacts, and a synthesized brief. Start here when you are new to an account.

## Inputs

Required (take from the user's message):
- `company` — Company name or domain to research

Optional modifiers (apply only if the user mentions them, otherwise use the defaults built into the workflow):
- `depth` — 'standard' (default) or 'deep' — deep also pulls news history, job postings, earnings calls, and filings

## Workflow

Follow this exactly, using the Salesmotion connector's tools by the names given.

Research <the company the user named> using Salesmotion and produce an account brief.

## Gather

1. account_insights with query="<the company the user named>" (use the domain if it looks like one).
   This returns profile, summary, research, SWOT, and value sections in one call.
If account_insights returns not_found or multiple_matches:
- multiple_matches: re-call account_insights with the accountId of the best match.
- not_found: the company may not be in the account list, or this may be an API-only organization.
  Fall back to get_company with input=<domain> and build from the company sub-resource tools
  (get_company_news, get_company_jobs, get_company_earnings_calls, get_company_filings).
  Say clearly which path you used, because the depth of the answer depends on it.
2. get_signals for the account — the 10 most recent. Note what changed and when.
3. get_contacts for the account — top 10 by score. Flag anyone who recently changed roles.
4. If the company is public and you need strategy in management's own words,
   call get_company_earnings_calls for the most recent call's AI analysis.

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

**Company snapshot** — what they do, industry, size, HQ, ownership, and how they make money.

**Strategic priorities** — the 3-5 things leadership is actually trying to accomplish, each with its source.

**What changed recently** — signals from the last 90 days that a seller could act on, newest first, with dates.

**People** — who matters, what they own, and who recently joined or moved (role changes are openings).

**Where we could help** — 2-3 hypotheses linking a specific problem of theirs to a specific capability. Label these as hypotheses.

**Open questions** — what you could not determine and would need discovery to answer.

Lead with what is decision-useful. Do not pad it.

Presentation rules (for any output longer than a short message; skip them for an email or DM draft):
- Open with a three-line bottom line: the situation, the opportunity, the next move. No preamble before it.
- Use a table wherever items share attributes: stakeholders (name, title, role in the deal, evidence), SWOT (a 2x2),
  objectives (metric, target, date), actions (owner, action, date), signals (date, type, what it means).
- Keep prose to short paragraphs of at most three sentences. One idea per bullet, no nested bullets.
- Put the source and date in the same row or line as the claim, not in a block at the end.
- Bold only the few phrases a reader skimming for 20 seconds must see. No emoji, no decorative dividers.
- If you can produce a formatted document or artifact, deliver the full output there and keep the chat reply to the bottom line.
