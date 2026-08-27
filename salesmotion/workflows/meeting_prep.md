# meeting_prep

Prepare for a meeting with a specific person: their background and priorities, what changed at their company, conversation starters, and questions worth asking.

## Inputs

Required (take from the user's message):
- `person` — Name of the person you are meeting
- `company` — Company name or domain

Optional modifiers (apply only if the user mentions them, otherwise use the defaults built into the workflow):
- `meetingType` — Optional: 'discovery', 'demo', 'negotiation', 'QBR', 'first call' — shapes emphasis

## Workflow

Follow this exactly, using the Salesmotion connector's tools by the names given.

Prepare me for a meeting with <the person the user named> at <the company the user named>.

## Gather

1. account_insights with query="<the company the user named>" for company context.
If account_insights returns not_found or multiple_matches:
- multiple_matches: re-call account_insights with the accountId of the best match.
- not_found: the company may not be in the account list, or this may be an API-only organization.
  Fall back to get_company with input=<domain> and build from the company sub-resource tools
  (get_company_news, get_company_jobs, get_company_earnings_calls, get_company_filings).
  Say clearly which path you used, because the depth of the answer depends on it.
2. search_contacts for "<the person the user named>", then get_contact on the match for their full profile,
   person insights, talking points, tenure, and any recent role change.
3. get_signals — the most recent 10, filtered mentally to what someone in their role would care about.
   A CFO and a VP Engineering care about different things at the same company.
4. If public and this is a senior commercial conversation: get_company_earnings_calls for the latest
   call, so you can reference what their leadership has publicly committed to.

Evidence rules:
- Attribute every material claim to what produced it: a signal, an earnings call, a filing, a job posting, or a news article. Include dates.
- Quote executives verbatim when you have their words. Paraphrased strategy is weak; quoted strategy is credible.
- If something is unknown, write "Not available in Salesmotion" and list it as an open question. Never fill a gap with a guess.
- Separate what the data says from what you infer. Label inferences as hypotheses.

## Deliver

**Who they are** — role, scope, tenure, and career path. If they are new in the role, lead with that:
it changes everything about how the conversation should go.

**What they likely care about** — inferred from their role and the company's stated priorities. Label
these as inferences.

**What changed at their company** — the 3 most relevant recent developments, dated and sourced.

**Conversation starters** — 2-3 openers tied to something specific and verifiable. They must be specific
enough that they could not be said to any other company.

**Questions to ask** — 4-5 questions that earn real answers. Prefer questions about their priorities and
constraints over questions whose answers you could have looked up.

**What to avoid** — anything sensitive: layoffs, a missed quarter, a failed initiative, litigation.
Knowing what not to raise is as valuable as knowing what to raise.
