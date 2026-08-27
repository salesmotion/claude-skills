# Salesmotion skills for Claude

Twelve guided B2B sales workflows — account briefs, account plans, value pyramids, MEDDIC qualification, stakeholder maps, meeting prep, signal-anchored outreach, pipeline and territory reviews, earnings and hiring analysis — packaged as a [Claude Skill](https://support.claude.com/en/articles/12512180-skills) that drives the [Salesmotion](https://salesmotion.io) connector.

Type `/salesmotion account plan for Honeywell` and get the plan. Every claim is tied to a dated source from Salesmotion; nothing is invented.

> The skill needs the **Salesmotion MCP connector** enabled in your chat. It calls the connector's tools; it has no data of its own. Set up the connector first: [salesmotion.io/help/getting-started-with-salesmotion-in-claude](https://salesmotion.io/help/getting-started-with-salesmotion-in-claude).

## Install

**claude.ai / Claude Desktop** — download [`salesmotion-claude-skill.zip`](https://github.com/salesmotion/claude-skills/releases/latest) and upload it under **Settings → Capabilities → Skills**. Then type `/salesmotion` in any chat.

**Claude Code** — copy the folder into your skills directory:

```bash
git clone https://github.com/salesmotion/claude-skills.git
cp -r claude-skills/salesmotion ~/.claude/skills/salesmotion
```

**Vercel Skills CLI** (installs into Claude Code, Cursor, Codex, Copilot and others):

```bash
npx skills add salesmotion/claude-skills
```

## Use

```
/salesmotion Honeywell                            → one-page brief
/salesmotion account plan for Honeywell           → strategic plan, 90-day actions
/salesmotion value pyramid Honeywell              → goals → strategy → obstacles → value paths
/salesmotion qualify the Bayer deal with MEDDIC   → scorecard and the gaps
/salesmotion who decides at Hitachi               → stakeholder map
/salesmotion meeting with Jane Doe at Honeywell   → meeting prep
/salesmotion email the CFO at Bayer about earnings → signal-anchored draft
/salesmotion what's new this week                 → pipeline review
```

A bare company name gives you the brief. A person plus a company gives you meeting prep. Everything else is matched on intent.

## What's inside

| File | Purpose |
|---|---|
| `salesmotion/SKILL.md` | The router: picks the workflow from your request, carries the shared rules |
| `salesmotion/workflows/*.md` | The twelve workflows — which Salesmotion tools to call, in what order, and what the output must contain |

The same twelve workflows ship inside the Salesmotion MCP server as prompts and as the `run_skill` tool, so they work by name in any MCP client without this package. This package is the `/salesmotion` shortcut.

## Rules every workflow follows

1. **Evidence over assertion** — every material claim is attributed to a signal, earnings call, filing, job posting, or article, with a date.
2. **Never invent** — if Salesmotion doesn't have it, the output says so and lists it as an open question.
3. **Inference is labeled** — what the data says and what Claude concludes are kept apart.

## Docs

- [Getting started in 5 minutes](https://salesmotion.io/help/getting-started-with-salesmotion-in-claude)
- [Using Salesmotion skills in Claude](https://salesmotion.io/help/mcp-skills)
- [The account card](https://salesmotion.io/help/mcp-account-card)
- [Connecting a whole workspace](https://salesmotion.io/help/mcp-workspace-keys)

Questions, or a workflow your team runs that isn't here: support@salesmotion.io.

## License

MIT. The workflows are text; use and adapt them freely. Salesmotion data is available through the Salesmotion API under your Salesmotion agreement.
