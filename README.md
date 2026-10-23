<img src="assets/pairwise-icon.svg" width="48" alt="Pairwise">

# Pairwise MCP skills

Connect your AI assistant to Pairwise, then ask it about your hiring work in plain language.

Pairwise hosts an MCP server for its customers. This repo shows you how to connect your assistant to it. It will also hold optional skills that help your assistant give better answers.

## Who it is for

Hiring managers, recruiters and delivery managers at companies that use Pairwise.

The Pairwise MCP server is available to Pairwise customers with a registered company account. Sign in with the same account you use for the Pairwise web app.

## What you can ask

Once connected, your assistant sees the same service requests (or jobs), candidates and evaluations (or interviews) that you see in Pairwise. Use whichever words your team uses. For example:

- "What needs my attention in Pairwise today?"
- "How is the Data Engineer request going?"
- "Who is in evaluation for that request? Summarize the two strongest candidates."
- "How many people have we interviewed for the Product Designer job?"
- "Show me new feedback from this week."

To create or change something, use the Pairwise web app.

## Connect

Server URL:

```
https://mcp.pairwise.ai/mcp
```

Every assistant connects the same way: add the server URL, then sign in with your Pairwise account when asked. You do not need an API key.

If your assistant does not offer custom connectors, your plan or your workspace admin may need to allow them. Each section links to the assistant's own guide.

- [Claude Code](#claude-code)
- [Claude (claude.ai and Claude Desktop)](#claude-claudeai-and-claude-desktop)
- [ChatGPT](#chatgpt)
- [Codex](#codex)
- [Cursor](#cursor)
- [Grok](#grok)
- [Grok Bot](#grok-bot)
- [Other assistants](#other-assistants)

### Claude Code

Install the Pairwise plugin. It connects the server and adds the [skills](#skills) in one step:

```bash
claude plugin marketplace add Pairwise-Technologies/pairwise-mcp-skills
claude plugin install pairwise@pairwise-mcp-skills
```

Then run `/mcp` in Claude Code, select `pairwise`, and sign in. Approve access in your browser.

To connect the server without the skills, add it directly instead:

```bash
claude mcp add --transport http pairwise https://mcp.pairwise.ai/mcp
claude mcp login pairwise
```

Use one way, not both, or Pairwise shows up twice. To check, run `claude mcp list`: `pairwise` shows as connected.

Guide: [Connect Claude Code to tools via MCP](https://code.claude.com/docs/en/mcp)

### Claude (claude.ai and Claude Desktop)

1. Open **Customize > Connectors**.
2. Select **+ Add**, then **Add custom connector**.
3. Enter the name `Pairwise` and the server URL, then select **Continue**.
4. Keep the suggested sign-in settings and select **Add**.
5. Select **Connect**, sign in to Pairwise, and approve access.

**Team and Enterprise:** an owner adds Pairwise first, under **Organization settings > Connectors**. Then each person selects **Connect** on Pairwise under **Customize > Connectors**.

Guide: [Getting started with custom connectors](https://support.claude.com/en/articles/11175166-getting-started-with-custom-connectors-using-remote-mcp)

### ChatGPT

1. Open **Plugins** (chatgpt.com/plugins).
2. Select **+**, then **Add custom MCP server**.
3. Enter the name `Pairwise` and the server URL.
4. Choose **OAuth** for authentication. Leave the client ID and client secret empty.
5. Create the plugin, install it, then select **Connect**, sign in to Pairwise, and approve access.

To use it, type **@** in a chat and choose Pairwise.

**Business, Enterprise and Edu:** your workspace admin may need to add Pairwise, or give you permission to add it.

Guide: [Connecting custom MCP servers in ChatGPT](https://help.openai.com/en/articles/12584461-connecting-custom-mcp-servers-in-chatgpt)

### Codex

In the terminal:

```bash
codex mcp add pairwise --url https://mcp.pairwise.ai/mcp
codex mcp login pairwise
```

In the Codex IDE extension or app:

1. Open **Settings > MCP servers > Add server**.
2. Enter the name `pairwise`, choose **Streamable HTTP**, and enter the server URL.
3. Save, select **Restart**, then **Authenticate**, and sign in to Pairwise.

To check, run `codex mcp list`, or `/mcp` in Codex.

Guide: [Model Context Protocol in Codex](https://learn.chatgpt.com/docs/extend/mcp)

### Cursor

1. Add Pairwise to `~/.cursor/mcp.json` (all projects) or `.cursor/mcp.json` (one project):

   ```json
   {
     "mcpServers": {
       "pairwise": {
         "url": "https://mcp.pairwise.ai/mcp"
       }
     }
   }
   ```

2. Open **Customize > MCPs** and select **Authenticate** next to `pairwise`.
3. Sign in to Pairwise and approve access.

**Teams and Enterprise:** your admin may need to allow Pairwise first.

Guide: [Model Context Protocol in Cursor](https://cursor.com/docs/context/mcp)

### Grok

1. Open **grok.com/connectors**.
2. Select **New Connector**, then **Custom**.
3. Enter the server URL, sign in to Pairwise, and approve access.

**Business and Enterprise:** a team admin adds Pairwise first.

Guide: [Grok connectors](https://docs.x.ai/grok/connectors)

### Grok Bot

Ask your bot in chat:

> Add the MCP server https://mcp.pairwise.ai/mcp

Then sign in to Pairwise when the bot sends you a link.

**Team bots:** an owner or manager adds Pairwise under **Setup > Plugins** as a custom remote MCP server. Each person signs in once.

Guide: [Team bots](https://docs.x.ai/grok-bot/team-bots)

### Other assistants

Any assistant that supports remote MCP servers with a sign-in step can connect. Give it the server URL and sign in when asked.

### Check the connection

Ask your assistant: "Who am I signed in as on Pairwise?" It should answer with your email and your company.

## Skills

Skills are short instructions that teach your assistant how to work with Pairwise: which steps to take, which words to use, and how to link back to Pairwise pages. They are optional. Your assistant works without them.

No skills have been published yet. They will be added here one at a time.

### Install the skills

- **Claude Code:** the [Pairwise plugin](#claude-code) installs all skills.
- **Other assistants:** copy the folders under [`skills/`](skills/) into your assistant's skills folder. Each folder is one skill in the [Agent Skills](https://agentskills.io/) format.

## Your data

Your assistant can read the hiring data you can see in Pairwise, including candidate information. Follow your company's policy on AI tools.

To disconnect, remove the Pairwise connector from your assistant.

## Troubleshooting

- **The assistant says Pairwise is not connected, or asks you to sign in again.** Sign in again with the steps for your assistant. Sessions expire after a while.
- **"Your account is not eligible for MCP."** The server is available to Pairwise customers with a registered company account. Contact support if you think your account should have access.
- **"Permission denied" for a service request, job or candidate.** Your account cannot see it in the Pairwise web app either. Ask your company's Pairwise admin for access.
- **Anything else.** Email [support@pairwise.ai](mailto:support@pairwise.ai) with the name of your assistant, what you asked, and the error text.

## Contributing

Suggestions and fixes are welcome. See [CONTRIBUTING.md](CONTRIBUTING.md). To report a security issue, see [SECURITY.md](SECURITY.md).

## License

[MIT](LICENSE). Copyright (c) 2026 Pairwise.

The license covers the content of this repo only. It grants no rights to the Pairwise name or logo.
