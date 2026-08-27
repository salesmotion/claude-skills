# account_plan

Build a complete strategic account plan: overview, stakeholder map, SWOT, whitespace, competition, objectives, and a 90-day action plan.

## Inputs

Required (take from the user's message):
- `company` — Company name or domain

Optional modifiers (apply only if the user mentions them, otherwise use the defaults built into the workflow):
- `objective` — Optional: your goal for this account (e.g. 'land first deal', 'expand into EMEA', 'protect renewal')
- `timeframe` — Planning horizon, e.g. '90 days', '2 quarters'. Default 90 days.

## Workflow

Follow this exactly, using the Salesmotion connector's tools by the names given.

Build a strategic account plan for <the company the user named> covering the next 90 days.

## Gather

1. account_insights with query="<the company the user named>" — all sections. The value section carries the
   value pyramid (company goals, business strategy, challenges, value paths) and the three whys.
If account_insights returns not_found or multiple_matches:
- multiple_matches: re-call account_insights with the accountId of the best match.
- not_found: the company may not be in the account list, or this may be an API-only organization.
  Fall back to get_company with input=<domain> and build from the company sub-resource tools
  (get_company_news, get_company_jobs, get_company_earnings_calls, get_company_filings).
  Say clearly which path you used, because the depth of the answer depends on it.
2. get_contacts — up to 25, so you can map the buying committee rather than just the top few.
3. get_signals — the last 90 days, to ground the plan in current reality.
4. get_company_jobs — hiring reveals funded initiatives and team growth.
5. If public: get_company_earnings_calls and get_company_filings for stated strategy and risk factors.

Evidence rules:
- Attribute every material claim to what produced it: a signal, an earnings call, a filing, a job posting, or a news article. Include dates.
- Quote executives verbatim when you have their words. Paraphrased strategy is weak; quoted strategy is credible.
- If something is unknown, write "Not available in Salesmotion" and list it as an open question. Never fill a gap with a guess.
- Separate what the data says from what you infer. Label inferences as hypotheses.

## Deliver

Structure the plan in these sections:

**1. Account overview** — firmographics, business model, how they make money, current relationship status.

**2. Their strategic priorities** — what leadership has committed to publicly, quoted and dated. This is the
spine of the plan: everything else connects back to it.

**3. Stakeholder map** — for each known contact: name, title, what they own, and their likely role
(economic buyer, champion, influencer, technical buyer, or blocker). Mark unknowns explicitly — an
unmapped economic buyer is the single most common reason enterprise deals stall.

**4. SWOT** — specific to this account and our position in it, not a generic company SWOT.

**5. Whitespace and growth** — where the opportunity is: which teams, regions, or use cases are unserved.

**6. Competitive landscape** — incumbents, likely alternatives, and switching costs. Say what you do not know.

**7. Objectives for 90 days** — 2-3 measurable objectives. Each needs a number and a date.

**8. Action plan** — specific actions with who, what, and when. Every action ties to an objective.

**9. Risks and open questions** — what could derail this, and what you must learn next.

A plan is only useful if it drives action. Prefer three concrete commitments over ten vague intentions.
