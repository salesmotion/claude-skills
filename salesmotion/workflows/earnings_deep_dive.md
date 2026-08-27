# earnings_deep_dive

Mine a public company's earnings calls and filings for strategy, priorities, and pressure in management's own words — the most credible material for executive conversations.

## Inputs

Required (take from the user's message):
- `company` — Company name, domain, or stock symbol

Optional modifiers (apply only if the user mentions them, otherwise use the defaults built into the workflow):
- `quarters` — How many recent quarters to analyse (default 4)

## Workflow

Follow this exactly, using the Salesmotion connector's tools by the names given.

Analyse the last 4 quarters of earnings commentary for <the company the user named>.

## Gather

1. get_company with input="<the company the user named>" to resolve the company and confirm it is publicly listed.
   If it is not public, say so and stop — this skill needs public disclosures.
2. get_company_earnings_calls with perPage=4. Read the AI analysis for each call.
   For the most recent call, consider includeTranscript=true with perPage=1 to quote precisely.
3. get_company_filings — 10-K and 10-Q risk factors, and any 8-K material events.
4. get_signals filtered to earnings-call and sec-10q for how Salesmotion scored these events.

Evidence rules:
- Attribute every material claim to what produced it: a signal, an earnings call, a filing, a job posting, or a news article. Include dates.
- Quote executives verbatim when you have their words. Paraphrased strategy is weak; quoted strategy is credible.
- If something is unknown, write "Not available in Salesmotion" and list it as an open question. Never fill a gap with a guess.
- Separate what the data says from what you infer. Label inferences as hypotheses.

## Deliver

**Strategic priorities** — what management repeats across calls. Repetition across quarters is the signal;
a one-off mention is not a priority. Quote them, with the quarter attached.

**What changed** — language that shifted between quarters. New initiatives named, old ones gone quiet,
guidance revised, tone hardened or softened. Changes in emphasis are where the opportunity usually is.

**Stated pressures** — the problems management has admitted publicly: cost programs, margin pressure,
competitive threats, integration challenges. Cross-reference against 10-K risk factors.

**Numbers that matter** — the metrics leadership holds itself to. These are the metrics any business case
you build should connect to.

**How to use this** — 3-4 specific ways a seller could use this material: an executive talking point, a
quote to open with, a pressure to align a value hypothesis to. Be concrete.

Quote rather than paraphrase wherever you can. "Our CFO said X on the Q3 call" is credible in a way that
"they are focused on efficiency" never is.
