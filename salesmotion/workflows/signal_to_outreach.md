# signal_to_outreach

Turn a specific buying signal into outreach that earns a reply — anchored to a real event, written for a real person, with a soft and specific ask.

## Inputs

Required (take from the user's message):
- `company` — Company name or domain

Optional modifiers (apply only if the user mentions them, otherwise use the defaults built into the workflow):
- `person` — Optional: who to write to. If omitted, the best contact is chosen.
- `channel` — 'email' (default) or 'linkedin'
- `signalHint` — Optional: which signal to anchor on, if you already know

## Workflow

Follow this exactly, using the Salesmotion connector's tools by the names given.

Draft an email to the best contact at <the company the user named>, anchored to a real buying signal.

## Gather

1. account_insights with query="<the company the user named>" — the value section gives you the three whys and
   value hypotheses, which are the raw material for a relevant message.
If account_insights returns not_found or multiple_matches:
- multiple_matches: re-call account_insights with the accountId of the best match.
- not_found: the company may not be in the account list, or this may be an API-only organization.
  Fall back to get_company with input=<domain> and build from the company sub-resource tools
  (get_company_news, get_company_jobs, get_company_earnings_calls, get_company_filings).
  Say clearly which path you used, because the depth of the answer depends on it.
2. get_signals — recent signals. Pick the one with the clearest implication for a buyer, not simply the
   newest. A funding round or a leadership change usually beats a routine press mention.
3. get_signal on the chosen signal for the full content, so you reference specifics rather than a headline.
4. get_contacts — pick the person whose role most directly owns the problem this signal implies.

Signal types you can filter on: relevant-news, press-release, hiring-alert, earnings-call,
m-and-a-alert, funding-alert, sec-10q, sec-def-14a, clinical-trial, document, and relevant-media
(relevant-media is podcast and video mentions).

## Write

Email: 50-90 words. Subject line under 6 words, specific, no clickbait.

Rules that decide whether this gets a reply:
- Open with the signal, not with yourself. No "I hope this finds you well", no "I wanted to reach out".
- Reference something only true of this company. If your message would work for a competitor, rewrite it.
- One hook, one proof point, one ask. Multiple asks get zero replies.
- Make the ask small and specific. A soft question outperforms a demo request cold.
- Write like a knowledgeable peer, not a vendor. No buzzwords, no stat dumps, no flattery.
- Never fabricate a customer, number, or result. If you have no proof point, leave it out.

## Deliver

1. The signal you anchored on and why it matters to this person specifically.
2. The draft, ready to send.
3. One alternative opening line taking a different angle.
4. The follow-up you would send if there is no reply, and how long you would wait.
