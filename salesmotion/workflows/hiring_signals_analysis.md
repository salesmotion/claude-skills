# hiring_signals_analysis

Read a company's job postings as strategy: what they are building, which teams are funded, what tools they use, and what that means for timing.

## Inputs

Required (take from the user's message):
- `company` — Company name or domain

Optional modifiers (apply only if the user mentions them, otherwise use the defaults built into the workflow):
- `focus` — Optional: a function or theme to focus on, e.g. 'sales', 'data', 'security'

## Workflow

Follow this exactly, using the Salesmotion connector's tools by the names given.

Analyse hiring activity at <the company the user named> and tell me what it reveals.

Job postings are among the most honest signals a company produces. A company will describe an initiative
vaguely in a press release and then post twelve roles that say exactly what it is building.

## Gather

1. get_company with input="<the company the user named>" to resolve the company.
2. get_company_jobs with perPage=50 for the full picture of open roles.
3. get_company_jobs again with includeDescription=true on the most relevant roles — the description text
   is where tech stack, tooling, and priorities are actually named.
4. get_signals filtered to hiring-alert for how Salesmotion has scored this activity.
5. account_insights with query="<the company the user named>" to connect hiring back to stated strategy.
If account_insights returns not_found or multiple_matches:
- multiple_matches: re-call account_insights with the accountId of the best match.
- not_found: the company may not be in the account list, or this may be an API-only organization.
  Fall back to get_company with input=<domain> and build from the company sub-resource tools
  (get_company_news, get_company_jobs, get_company_earnings_calls, get_company_filings).
  Say clearly which path you used, because the depth of the answer depends on it.

Evidence rules:
- Attribute every material claim to what produced it: a signal, an earnings call, a filing, a job posting, or a news article. Include dates.
- Quote executives verbatim when you have their words. Paraphrased strategy is weak; quoted strategy is credible.
- If something is unknown, write "Not available in Salesmotion" and list it as an open question. Never fill a gap with a guess.
- Separate what the data says from what you infer. Label inferences as hypotheses.

## Deliver

**What they are building** — the initiatives the hiring pattern implies. Cluster roles by theme rather
than listing them. Five backend roles plus a data engineer plus an ML lead is a platform investment, not
six unrelated openings.

**Which teams are growing** — by function and seniority, with counts. Where the headcount goes, the
budget has already gone.

**Tools and stack named** — technologies, platforms, and vendors mentioned in descriptions. This tells you
the incumbent landscape and where you would fit or displace.

**Leadership hires** — senior roles being filled. A new VP arrives with a mandate and usually a budget,
and is the single best-timed entry point into an account.

**Locations** — geographic expansion visible in where roles are posted.

**What this means for us** — the timing implication. Does this hiring create a need we serve, and is the
window opening now or in six months? Be specific about timing and label the reasoning as inference.
