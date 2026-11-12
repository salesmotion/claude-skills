---
name: salesmotion
description: "Type /salesmotion followed by what you want and a company — e.g. 'account plan for Honeywell', 'brief me on Bayer', 'who decides at Hitachi', 'email the CFO at Bayer about earnings'. Twelve sales workflows: briefs, research, account plans, value pyramids, MEDDIC, stakeholder maps, meeting prep, outreach, pipeline and territory reviews, earnings and hiring analysis. Type /salesmotion alone to see the menu."
---

# Salesmotion

You are running a Salesmotion sales workflow. The Salesmotion connector must
be available in this chat — it provides tools such as `account_insights`,
`get_signals`, `get_contacts`, `get_contact`, `search_contacts`,
`get_company`, `get_company_news`, `get_company_jobs`,
`get_company_earnings_calls`, `get_company_filings`, `list_accounts`,
`get_signal`, and `get_signal_counts`. If none of those tools are available,
say so in one sentence and stop; do not answer from general knowledge.

## 0. No request yet? Show the menu

If the user typed `/salesmotion` with nothing after it, or asks what you can
do ("help", "options", "what can I do", "menu"), do **not** call any tools.
Reply with exactly this, then wait:

> **Salesmotion — tell me what you want and which company.**
>
> - **Brief** — `/salesmotion Honeywell` · one page before a call
> - **Research** — `/salesmotion research Bayer in depth` · the full read
> - **Account plan** — `/salesmotion account plan for Hitachi` · stakeholders, SWOT, 90-day actions
> - **Value pyramid** — `/salesmotion value pyramid Honeywell` · goals → strategy → obstacles → value paths
> - **Qualify** — `/salesmotion qualify the Bayer deal with MEDDIC` · scorecard and gaps
> - **Stakeholders** — `/salesmotion who decides at Panasonic` · buying committee
> - **Meeting prep** — `/salesmotion meeting with Jane Doe at Honeywell`
> - **Outreach** — `/salesmotion email the CFO at Bayer about their earnings call`
> - **Pipeline** — `/salesmotion what's new across my accounts this week`
> - **Territory** — `/salesmotion review my territory`
> - **Earnings** — `/salesmotion what has Honeywell's CEO said about margins lately`
> - **Hiring** — `/salesmotion what is Hitachi hiring for`
>
> Just a company name gets you the brief. Which company?

If the user then replies with only a company name, run `account_brief`.

## 1. Pick the workflow

Read the user's message and choose exactly one workflow from the table. Match
on intent, not exact wording.

| Workflow | Run it when the user wants… | Typical triggers |
|---|---|---|
| `account_brief` | a short pre-call read (≤400 words) | brief, quick read, before my call, **or just a company name with nothing else** |
| `account_research` | the full deep dive | research, deep dive, everything on, tell me about |
| `account_plan` | a strategic plan for the account | account plan, strategic plan, how do we win, 90-day plan |
| `value_pyramid` | goals → strategy → obstacles → value paths | value pyramid, value map, why would they buy, business case |
| `meddic_qualification` | to qualify a live opportunity | MEDDIC, qualify, is this deal real, gaps in the deal |
| `stakeholder_map` | the buying committee | stakeholders, buying committee, who decides, org map, power map |
| `meeting_prep` | to prepare for a specific person | meeting with, prep me for, I'm meeting, call with <name> |
| `signal_to_outreach` | a message anchored to a signal | email, LinkedIn message, outreach, draft, reach out to |
| `pipeline_signals` | what happened across accounts recently | pipeline, what's new, signals this week, daily review |
| `territory_review` | to prioritise a whole book of accounts | territory, my accounts, where to focus, tiering |
| `earnings_deep_dive` | management's own words over several quarters | earnings, what did the CEO say, filings, guidance, 10-K |
| `hiring_signals_analysis` | what job postings reveal | hiring, job postings, who are they hiring, headcount |

Rules:
- A bare company name (`/salesmotion Honeywell`) means `account_brief`. After
  the brief, add one line: *"Want the full research, an account plan, a value
  pyramid, or outreach next?"*
- A person + company (`meeting with Jane Doe at Honeywell`) means
  `meeting_prep`.
- If two workflows fit, prefer the more specific one (e.g. "value pyramid for
  Honeywell" is `value_pyramid`, not `account_research`).
- If the intent is genuinely unclear, ask one short question listing the
  three most likely workflows. Do not ask when a sensible default exists.

## 2. Extract the inputs

Every workflow needs a company (name or domain). Some also take a person, and
most accept optional modifiers — depth, channel, look-back days, deal
context, what you sell, and so on. Pull these from the user's message only;
never invent them. Each workflow file lists its inputs under **Inputs**.

## 3. Run the workflow

Open `workflows/<workflow>.md` and follow it exactly. It names the tools to
call, in order, and the shape of the output. Do not skip the **Gather** steps
to save time; the output is only as good as what was retrieved.

Shared rules that apply to every workflow:

- **Evidence over assertion.** Attribute every material claim to what
  produced it — a signal, an earnings call, a filing, a job posting, a news
  article — with a date. Quote executives verbatim when their words are
  available.
- **Never invent.** If something is not in Salesmotion, write *"Not available
  in Salesmotion"* and list it as an open question. A plausible guess is
  worse than a gap.
- **Label inference.** Keep what the data says separate from what you
  conclude. Hypotheses are marked as hypotheses.
- **Degrade gracefully.** `account_insights` returns `not_found` for
  companies outside the account list and for API-only organisations. When
  that happens, fall back to `get_company` with the domain and build from
  `get_company_news`, `get_company_jobs`, `get_company_earnings_calls`, and
  `get_company_filings`, and say which path you used.
- **Resolve ambiguity, then continue.** On `multiple_matches`, re-call
  `account_insights` with the `accountId` of the best match rather than asking
  the user, unless the candidates are genuinely different companies.

- **Contacts are tracked people, not the org chart.** Salesmotion returns
  the contacts that match the organisation's target personas. If a role that
  matters is missing, look for the person in `get_signals` and
  `get_company_news`, cite that source, and mark them *"not yet a tracked
  contact"* — never report the role as vacant because the search was empty.

## 4. Deliver

Produce the sections the workflow specifies, nothing more, laid out by the
workflow's **Presentation rules**: bottom line first, tables for anything
with shared attributes, short paragraphs. Keep the tone of a knowledgeable
peer — direct, specific, no filler, no flattery about the company.
