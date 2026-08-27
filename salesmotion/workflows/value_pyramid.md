# value_pyramid

Build a value pyramid for an account: their company goals, business strategy, challenges and obstacles, and the value paths that connect your solution to their goals.

## Inputs

Required (take from the user's message):
- `company` — Company name or domain

Optional modifiers (apply only if the user mentions them, otherwise use the defaults built into the workflow):
- `solution` — Optional: what you sell, so value paths connect to your actual capabilities

## Workflow

Follow this exactly, using the Salesmotion connector's tools by the names given.

Build a value pyramid for <the company the user named>.

A value pyramid connects what a company is trying to achieve to why they would buy. It has four layers,
top to bottom: company goals, business strategy, challenges and obstacles, and value paths.

## Gather

1. account_insights with query="<the company the user named>", sections="value,research,summary".
   Salesmotion generates a value pyramid directly — read it from the value section and use it as your base.
   The same section carries the three whys (why change, why now, why you) and value hypotheses.
If account_insights returns not_found or multiple_matches:
- multiple_matches: re-call account_insights with the accountId of the best match.
- not_found: the company may not be in the account list, or this may be an API-only organization.
  Fall back to get_company with input=<domain> and build from the company sub-resource tools
  (get_company_news, get_company_jobs, get_company_earnings_calls, get_company_filings).
  Say clearly which path you used, because the depth of the answer depends on it.
2. If public: get_company_earnings_calls — management states goals and strategy in their own words on
   these calls. This is the strongest possible evidence for the top two layers.
3. get_company_filings — 10-K risk factors map directly to the challenges layer.
4. get_signals — recent events that create urgency around any obstacle.

Evidence rules:
- Attribute every material claim to what produced it: a signal, an earnings call, a filing, a job posting, or a news article. Include dates.
- Quote executives verbatim when you have their words. Paraphrased strategy is weak; quoted strategy is credible.
- If something is unknown, write "Not available in Salesmotion" and list it as an open question. Never fill a gap with a guess.
- Separate what the data says from what you infer. Label inferences as hypotheses.

## Deliver

Present the pyramid top-down, each layer sourced:

**Layer 1 — Company goals.** What the business is trying to achieve, in their language. Quote leadership
where you can. These are outcomes (revenue, margin, share, growth), not activities.

**Layer 2 — Business strategy.** How they have chosen to pursue those goals: the initiatives, bets, and
operating changes they have committed to.

**Layer 3 — Challenges and obstacles.** What stands between the strategy and the goals. Evidence these
from filings, earnings commentary, and signals rather than assuming the pains your product happens to solve.

**Layer 4 — Value paths.** For each significant obstacle, the specific path by which your solution removes
or reduces it, and the metric that would move as a result.
  Note: no solution was specified, so keep value paths at the level of capability outcomes and mark
  them as hypotheses to be validated.

**The connection test.** For each value path state, in one sentence: if we do X, their obstacle Y shrinks,
which advances goal Z. If you cannot complete that sentence with evidence, the path is speculative — say so.

Close with the two or three value paths that are strongest, and what you would need to confirm in discovery.
