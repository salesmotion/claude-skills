# Salesmotion for Claude

Account research, account plans, meeting prep, MEDDIC qualification and signal-anchored outreach, built on [Salesmotion](https://salesmotion.io)'s live account intelligence: buying signals, earnings calls, filings, job postings, news and contacts for the companies you sell to.

This plugin bundles two things:

- **The Salesmotion connector** (remote MCP server at `https://mcp.salesmotion.io`). It gives Claude Salesmotion's tools: account insights, signals, contacts, company news, jobs, earnings calls and filings.
- **The Salesmotion skill**: twelve guided B2B sales workflows that tell Claude which tools to call, in what order, and what the output must contain. Every claim is tied to a dated source from Salesmotion; nothing is invented.

Ask for an account plan for Honeywell and you get the plan.

## Install

**Claude Code**

```
/plugin marketplace add salesmotion/claude-skills
/plugin install salesmotion@salesmotion
```

Then run `/mcp`, pick **salesmotion** and sign in (see [Connect and sign in](#connect-and-sign-in)).

**claude.ai, Claude Desktop and Cowork**: once the plugin is listed in the Claude directory, add **Salesmotion** from **Customize > Plugins**, then connect the Salesmotion connector from the plugin's **Connectors** tab. Until then, add the connector by hand (below) and upload the skill: download [`salesmotion-claude-skill.zip`](https://github.com/salesmotion/claude-skills/releases/latest) and add it under **Settings > Capabilities > Skills**.

**Vercel Skills CLI** (the skill only, for Claude Code, Cursor, Codex, Copilot and others):

```bash
npx skills add salesmotion/claude-skills
```

## Connect and sign in

Salesmotion for Claude works with Salesmotion workspaces that have API access switched on. Ask your account manager or hi@salesmotion.io to turn it on for your workspace.

**claude.ai and Claude Desktop** (when adding the connector by hand):

1. Go to **Settings > Connectors > Add custom connector**. On Team and Enterprise plans an Owner adds it once under **Admin settings > Connectors**, then each person selects **Connect**.
2. Name: `Salesmotion`. URL: `https://mcp.salesmotion.io`.
3. Authentication: choose the sign-in option at the top of the list. OAuth client: **Use Claude's published identity**. Add no request headers and leave **Advanced** as it is.
4. Select **Add**, then **Connect**. On the Salesmotion page select **Sign in with Salesmotion**, log in with your normal Salesmotion login (email and password, or Google), and select **Allow and connect**.

**Claude Code**: the plugin adds the connector for you. Run `/mcp`, select **salesmotion**, and complete the same Salesmotion sign-in in your browser.

You don't need an API key. Claude signs in with your own Salesmotion account and sees only what your account can see.

## Use

```
Brief me on Honeywell                           → one-page brief
Account plan for Honeywell                      → strategic plan, 90-day actions
Value pyramid for Honeywell                     → goals → strategy → obstacles → value paths
Qualify the Bayer deal with MEDDIC              → scorecard and the gaps
Who decides at Hitachi                          → stakeholder map
Prep my meeting with Jane Doe at Honeywell      → meeting prep
Email the CFO at Bayer about their earnings     → signal-anchored draft
What's new across my accounts this week         → pipeline review
```

Claude picks the workflow from what you ask. In claude.ai you can also type `/salesmotion` followed by your request, or `/salesmotion` alone for the menu. In Claude Code the skill is `/salesmotion:salesmotion`. A bare company name gives you the brief; a person plus a company gives you meeting prep.

The twelve workflows: account brief, account research, account plan, value pyramid, MEDDIC qualification, stakeholder map, meeting prep, signal to outreach, pipeline signals, territory review, earnings deep dive and hiring signals analysis.

## What's inside

| Path | Purpose |
|---|---|
| `.claude-plugin/plugin.json` | Plugin manifest |
| `.claude-plugin/marketplace.json` | Lets Claude Code add this repository as a plugin marketplace |
| `.mcp.json` | The Salesmotion connector (`https://mcp.salesmotion.io`) |
| `skills/salesmotion/SKILL.md` | The router: picks the workflow from your request and carries the shared rules |
| `skills/salesmotion/workflows/*.md` | The twelve workflows |

The same twelve workflows ship inside the Salesmotion MCP server as prompts and as the `run_skill` tool, so they also work by name in any MCP client.

## Rules every workflow follows

1. **Evidence over assertion**: every material claim is attributed to a signal, earnings call, filing, job posting or article, with a date.
2. **Never invent**: if Salesmotion doesn't have it, the output says so and lists it as an open question.
3. **Inference is labeled**: what the data says and what Claude concludes are kept apart.

## Data and privacy

The plugin contains only text instructions and the connector address. It runs no local code and stores nothing on your machine.

When you use it, Claude calls the Salesmotion connector at `https://mcp.salesmotion.io`. The requests carry what the workflow needs: company names, domains, person names and your search terms. They are authenticated with your Salesmotion sign-in. Salesmotion returns account data from your workspace: signals, contacts, news, jobs, earnings and filings. The plugin sends nothing to any other service.

- Privacy policy: https://salesmotion.io/privacy-policy
- Terms of service: https://salesmotion.io/terms-of-service

## Support

- Getting started: https://salesmotion.io/help/getting-started-with-salesmotion-in-claude
- Using the Salesmotion skills in Claude: https://salesmotion.io/help/mcp-skills
- Questions, or a workflow your team runs that isn't here: hi@salesmotion.io

## License

MIT. The workflows are text; use and adapt them freely. Salesmotion data is available through the Salesmotion API under your Salesmotion agreement.
