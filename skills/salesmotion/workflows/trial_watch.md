# trial_watch

Life Sciences: turn the trials your accounts start or complete in the next 180 days into a prioritized outreach list.

## Inputs

Required (take from the user's message):

Optional modifiers (apply only if the user mentions them, otherwise use the defaults built into the workflow):
- `therapeuticArea` — Optional: one therapeutic area to focus on, e.g. oncology, neurology, rareDiseases
- `phase` — Optional: one phase to focus on, e.g. phase2, phase3

## Workflow

Follow this exactly, using the Salesmotion connector's tools by the names given.

Find the clinical trials across my accounts that start or reach primary completion in the next 180 days,
and tell me which accounts to contact first and why.

## Gather

1. get_trial_radar with lens="startingSoon" and perPage=50.
   If get_trial_radar is not available, or answers that it is part of the Life Sciences pack, say this workflow needs
   the Life Sciences pack and stop.
2. get_trial_radar with lens="completingSoon" and perPage=50.
3. For the 5-8 accounts with the strongest trials (later phase, larger enrollment, nearer date, several trials):
   - get_clinical_trials with trialId and includeDetails=true on the lead trial, for sponsors, sites and the point of contact.
   - get_contacts with accountId, for the people who run trials (clinical operations, R&D, medical affairs, procurement).
   - get_signals with accountId and signalType=clinical-trial, for recent trial events (starts, phase transitions, readouts).

Evidence rules:
- Attribute every material claim to what produced it: a signal, an earnings call, a filing, a job posting, or a news article. Include dates.
- Quote executives verbatim when you have their words. Paraphrased strategy is weak; quoted strategy is credible.
- If something is unknown, write "Not available in Salesmotion" and list it as an open question. Never fill a gap with a guess.
- Separate what the data says from what you infer. Label inferences as hypotheses.
- Contacts are the people this organization tracks, not the full org chart. If a role that matters (CEO, CFO, CRO, the economic buyer)
  is missing from get_contacts, search get_signals and get_company_news for the title and for recent leadership changes, name the person
  from that source with its date, and mark them "not yet a tracked contact". Never report a role as vacant or a person as unknown
  only because the contact search came back empty.
- Give every date as the registry reports it and mark estimated dates as estimates. Cite the registry ID (NCT or EU CT number).

## Deliver

**This month** — up to five accounts where a trial milestone creates a reason to reach out now. A table with: account,
trial (registry ID, phase, therapeutic area), the milestone and its date, why it matters now, who to contact, next action.

**Next quarter** — accounts whose milestones are 60-180 days out, and what to prepare before then.

**Why it matters now** — a trial about to start is choosing sites, vendors and enrollment support; a trial reaching
primary completion is heading to data analysis, readout and next-phase or launch planning. Tie each account to the one
that applies and label the link to what we sell as a hypothesis.

Rank by the strength of the reason to act, not by the number of trials. Say plainly if fewer than five accounts qualify.

Presentation rules (for any output longer than a short message; skip them for an email or DM draft):
- Open with a three-line bottom line: the situation, the opportunity, the next move. No preamble before it.
- Use a table wherever items share attributes: stakeholders (name, title, role in the deal, evidence), SWOT (a 2x2),
  objectives (metric, target, date), actions (owner, action, date), signals (date, type, what it means).
- Keep prose to short paragraphs of at most three sentences. One idea per bullet, no nested bullets.
- Put the source and date in the same row or line as the claim, not in a block at the end.
- Bold only the few phrases a reader skimming for 20 seconds must see. No emoji, no decorative dividers.
- If you can produce a formatted document or artifact, deliver the full output there and keep the chat reply to the bottom line.
