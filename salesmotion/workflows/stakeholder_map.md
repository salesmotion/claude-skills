# stakeholder_map

Map the buying committee at an account: who holds power, who is likely to champion, who could block, and where the coverage gaps are.

## Inputs

Required (take from the user's message):
- `company` — Company name or domain

Optional modifiers (apply only if the user mentions them, otherwise use the defaults built into the workflow):
- `dealContext` — Optional: what you are selling and who you have already engaged

## Workflow

Follow this exactly, using the Salesmotion connector's tools by the names given.

Map the buying committee at <the company the user named>.

## Gather

1. get_contacts for the account — request up to 50 so you see the whole org, not just the top scores.
   Resolve the account first with account_insights query="<the company the user named>" if you need the accountId.
If account_insights returns not_found or multiple_matches:
- multiple_matches: re-call account_insights with the accountId of the best match.
- not_found: the company may not be in the account list, or this may be an API-only organization.
  Fall back to get_company with input=<domain> and build from the company sub-resource tools
  (get_company_news, get_company_jobs, get_company_earnings_calls, get_company_filings).
  Say clearly which path you used, because the depth of the answer depends on it.
2. get_contact on the 5-8 most important people for full profiles, person insights, and talking points.
3. get_contacts with changeType filters (newJoiner, promotion, internalChange) — people new in role are
   disproportionately open to new vendors and are often the best entry point.
4. get_signals — leadership changes and reorganizations reshape who matters.

Evidence rules:
- Attribute every material claim to what produced it: a signal, an earnings call, a filing, a job posting, or a news article. Include dates.
- Quote executives verbatim when you have their words. Paraphrased strategy is weak; quoted strategy is credible.
- If something is unknown, write "Not available in Salesmotion" and list it as an open question. Never fill a gap with a guess.
- Separate what the data says from what you infer. Label inferences as hypotheses.

## Deliver

**The map.** For each person: name, title, what they own, likely role in a purchase (economic buyer,
champion, influencer, technical buyer, blocker, or unknown), and how you inferred it. Mark inferred
roles as inferred — a title is evidence of scope, not of intent.

**Power and interest.** Who has authority, and who actually cares about the problem. The overlap is
where deals are won; people with power but no interest are the ones who kill deals late.

**Recent movers.** Anyone who joined, was promoted, or changed roles in the last 6 months, with dates.
New leaders bring mandates and budget, and they are rarely loyal to incumbent vendors.

**Coverage gaps.** Which roles you would expect on a buying committee for this kind of purchase that
you have no contact for. Name the gap explicitly — unknown stakeholders are risk, not absence of risk.

**Entry strategy.** Given the above, who to approach first and why, and the specific reason each
person would take the meeting. Ground it in something real about them or their business.
