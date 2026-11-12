# pipeline_signals

Scan your accounts for recent buying signals and turn them into a prioritized action list. Use for a daily or weekly territory review.

## Inputs

Required (take from the user's message):

Optional modifiers (apply only if the user mentions them, otherwise use the defaults built into the workflow):
- `days` — Look-back period in days (default 7)
- `signalType` — Optional: filter to one signal type
- `focus` — Optional: 'new business', 'expansion', or 'renewal risk'

## Workflow

Follow this exactly, using the Salesmotion connector's tools by the names given.

Review buying signals across my accounts from the last 7 days.

## Gather

1. get_signal_counts with afterDate="<today's date minus 7 days, as YYYY-MM-DD>" for the distribution.
2. list_accounts with hasSignalsAfterDate="<today's date minus 7 days, as YYYY-MM-DD>", sorted by score, up to 20.
3. get_signals for the top accounts to see what actually happened.

Signal types you can filter on: relevant-news, press-release, hiring-alert, earnings-call,
m-and-a-alert, funding-alert, sec-10q, sec-def-14a, clinical-trial, document, and relevant-media
(relevant-media is podcast and video mentions).

## Deliver

This is a working document, not a report. Optimize it for deciding what to do this week.

**Act now** — accounts where something happened that creates a genuine reason to reach out in the next
few days. For each: the account, the signal with its date, why it matters, and the specific next action.

**Worth watching** — accounts with movement that is not yet actionable, and what would make it actionable.

**Quiet** — high-value accounts with no recent signals. Silence is itself information; note them.

Rank by the strength of the reason to act, not by signal volume. One leadership change at a target
account beats twelve press mentions somewhere else. Cap the act-now list at five so it stays a real
priority list — and say plainly if fewer than five genuinely qualify.

Presentation rules (for any output longer than a short message; skip them for an email or DM draft):
- Open with a three-line bottom line: the situation, the opportunity, the next move. No preamble before it.
- Use a table wherever items share attributes: stakeholders (name, title, role in the deal, evidence), SWOT (a 2x2),
  objectives (metric, target, date), actions (owner, action, date), signals (date, type, what it means).
- Keep prose to short paragraphs of at most three sentences. One idea per bullet, no nested bullets.
- Put the source and date in the same row or line as the claim, not in a block at the end.
- Bold only the few phrases a reader skimming for 20 seconds must see. No emoji, no decorative dividers.
- If you can produce a formatted document or artifact, deliver the full output there and keep the chat reply to the bottom line.
