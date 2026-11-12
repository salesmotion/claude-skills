# territory_review

Step back and assess a whole book of accounts: where the potential is, which accounts are being under-worked, and where to spend time next quarter.

## Inputs

Required (take from the user's message):

Optional modifiers (apply only if the user mentions them, otherwise use the defaults built into the workflow):
- `owner` — Optional: filter to a specific owner's accounts
- `days` — Signal look-back window in days (default 90)

## Workflow

Follow this exactly, using the Salesmotion connector's tools by the names given.

Assess my territory and tell me where to focus.

## Gather

1. list_accounts sorted by score, up to 50, to see the shape of the book.
2. list_accounts with hasSignalsAfterDate="<today's date minus 90 days, as YYYY-MM-DD>" to see which accounts show activity.
3. get_signal_counts with afterDate="<today's date minus 90 days, as YYYY-MM-DD>" for the overall picture.
4. get_signals on the highest-scoring active accounts to understand what is driving the activity.

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

**The shape of the book** — how many accounts, how scores are distributed, how many show recent activity
versus none. State the numbers.

**Tier 1: invest** — the 5-8 accounts that deserve real planning time, with the reason each qualifies.
High score plus recent activity is the strongest combination.

**Tier 2: maintain** — accounts worth periodic attention, and the trigger that would promote them.

**Tier 3: monitor** — everything else. Automated monitoring rather than active work.

**Under-worked** — high-scoring accounts with signal activity that appear to be getting no attention.
These are the most common source of missed pipeline.

**Where the time should go** — a concrete recommendation on how to split effort across the tiers, and
what to stop doing to make room. A prioritization that adds work without removing any is not a prioritization.

Presentation rules (for any output longer than a short message; skip them for an email or DM draft):
- Open with a three-line bottom line: the situation, the opportunity, the next move. No preamble before it.
- Use a table wherever items share attributes: stakeholders (name, title, role in the deal, evidence), SWOT (a 2x2),
  objectives (metric, target, date), actions (owner, action, date), signals (date, type, what it means).
- Keep prose to short paragraphs of at most three sentences. One idea per bullet, no nested bullets.
- Put the source and date in the same row or line as the claim, not in a block at the end.
- Bold only the few phrases a reader skimming for 20 seconds must see. No emoji, no decorative dividers.
- If you can produce a formatted document or artifact, deliver the full output there and keep the chat reply to the bottom line.
