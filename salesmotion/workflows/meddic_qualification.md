# meddic_qualification

Qualify an opportunity against MEDDIC — metrics, economic buyer, decision criteria, decision process, identified pain, and champion — and expose the gaps that put the deal at risk.

## Inputs

Required (take from the user's message):
- `company` — Company name or domain

Optional modifiers (apply only if the user mentions them, otherwise use the defaults built into the workflow):
- `dealContext` — Optional: what you know so far — stage, deal size, who you have met, what has been said

## Workflow

Follow this exactly, using the Salesmotion connector's tools by the names given.

Qualify the opportunity at <the company the user named> using MEDDIC.

## Gather

1. account_insights with query="<the company the user named>" — full sections.
If account_insights returns not_found or multiple_matches:
- multiple_matches: re-call account_insights with the accountId of the best match.
- not_found: the company may not be in the account list, or this may be an API-only organization.
  Fall back to get_company with input=<domain> and build from the company sub-resource tools
  (get_company_news, get_company_jobs, get_company_earnings_calls, get_company_filings).
  Say clearly which path you used, because the depth of the answer depends on it.
2. get_contacts — up to 25, with titles and role changes, to identify buyer and champion candidates.
3. get_signals — recent events that create or intensify pain.
4. If public: get_company_earnings_calls and get_company_filings for stated metrics and risk factors.

Evidence rules:
- Attribute every material claim to what produced it: a signal, an earnings call, a filing, a job posting, or a news article. Include dates.
- Quote executives verbatim when you have their words. Paraphrased strategy is weak; quoted strategy is credible.
- If something is unknown, write "Not available in Salesmotion" and list it as an open question. Never fill a gap with a guess.
- Separate what the data says from what you infer. Label inferences as hypotheses.

## Deliver

Work through all six elements. For each: what the data supports, what is assumed, and what is unknown.

**M — Metrics.** The quantified economic outcome they expect. Use their own reported numbers where
available (growth rates, margin targets, cost programs). A metric the buyer already tracks beats one you invent.

**E — Economic buyer.** Who controls the budget and can approve unilaterally. Name them if the contact data
supports it. If you cannot identify them, say so — this is the most common fatal gap in enterprise deals.

**D — Decision criteria.** The technical, financial, and functional requirements they will judge against.

**D — Decision process.** The steps from evaluation to signature: stages, approvers, procurement, legal, timing.
Note whether fiscal year end or budget cycles constrain timing.

**I — Identified pain.** The business problem severe enough to force action. Tie it to the metrics above.
Pain that is not connected to a number does not create urgency.

**C — Champion.** Who benefits enough to sell internally on your behalf, and do they have real access?
Distinguish a champion from a friendly contact — they are not the same thing.

**Scorecard.** Rate each element Strong / Partial / Missing, with a one-line justification.

**The gaps that matter.** Rank the missing elements by how much they threaten the deal, and give the
specific next action to close each one — the question to ask, the meeting to request, the person to reach.

Be honest about weakness. A qualification that flatters the deal is worse than useless.
