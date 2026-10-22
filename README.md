# Pairwise MCP skills

Connect your AI assistant to Pairwise, then ask it about your hiring work in plain language.

Pairwise hosts an MCP server for its customers. This repo shows you how to connect your assistant to it. It will also hold optional skills that help your assistant give better answers.

## Who it is for

Hiring managers, recruiters and delivery managers at companies that use Pairwise.

The Pairwise MCP server is available to Pairwise customers with a registered company account. Sign in with the same account you use for the Pairwise web app.

## What you can ask

Once connected, your assistant sees the same service requests, candidates and evaluations that you see in Pairwise. For example:

- "What needs my attention in Pairwise today?"
- "Give me a pipeline summary for the Senior Data Engineer request."
- "Who is in Evaluation for that request? Summarize the two strongest candidates."
- "Show me new feedback from this week."

To create or change something, use the Pairwise web app.

## Connect

Server URL:

```
https://mcp.pairwise.ai/mcp
```

Every assistant connects the same way: add the server URL, then sign in with your Pairwise account when asked. You do not need an API key.

Supported assistants:

- [Claude Code](#claude-code)
- [Claude (claude.ai and Claude Desktop)](#claude-claudeai-and-claude-desktop)
- [ChatGPT](#chatgpt)
- [Codex](#codex)
- [Cursor](#cursor)
- [Grok and Grok Bot](#grok-and-grok-bot)
- [Other assistants](#other-assistants)

### Claude Code

```bash
claude mcp add --transport http pairwise https://mcp.pairwise.ai/mcp
claude mcp login pairwise
```

The login opens Pairwise in your browser. Approve access, then run `/mcp` in Claude Code to check that `pairwise` shows as connected.

### Claude (claude.ai and Claude Desktop)

1. Open **Settings > Connectors**.
2. Select **Add custom connector**.
3. Enter the name `Pairwise` and the server URL.
4. Select **Connect**, then sign in to Pairwise and approve access.

### ChatGPT

1. In ChatGPT settings, create a custom connector with the server URL.
2. Leave the OAuth client ID and client secret empty.
3. Sign in to Pairwise and approve access.

If you do not see an option to add a custom connector, your ChatGPT plan or workspace admin may need to turn it on.

### Codex

```bash
codex mcp add pairwise --url https://mcp.pairwise.ai/mcp
codex mcp login pairwise
```

### Cursor

Add Pairwise to `~/.cursor/mcp.json` (all projects) or `.cursor/mcp.json` (one project):

```json
{
  "mcpServers": {
    "pairwise": {
      "url": "https://mcp.pairwise.ai/mcp"
    }
  }
}
```

Then open Cursor's MCP settings and sign in to `pairwise`.

### Grok and Grok Bot

Add a custom connector (MCP server) with the server URL, then sign in to Pairwise and approve access.

### Other assistants

Any assistant that supports remote MCP servers with a sign-in step can connect. Give it the server URL and sign in when asked.

### Check the connection

Ask your assistant: "Who am I signed in as on Pairwise?" It should answer with your email and your company.

## Skills

Skills are short instructions that teach your assistant how to work with Pairwise: which steps to take, which words to use, and how to link back to Pairwise pages. They are optional. Your assistant works without them.

No skills have been published yet. They will be added here one at a time.

## Your data

Your assistant can read the hiring data you can see in Pairwise, including candidate information. Follow your company's policy on AI tools.

To disconnect, remove the Pairwise connector from your assistant.

## Troubleshooting

- **The assistant says Pairwise is not connected, or asks you to sign in again.** Sign in again with the steps for your assistant. Sessions expire after a while.
- **"Your account is not eligible for MCP."** The server is available to Pairwise customers with a registered company account. Contact support if you think your account should have access.
- **"Permission denied" for a service request or candidate.** Your account cannot see it in the Pairwise web app either. Ask your company's Pairwise admin for access.
- **Anything else.** Email [support@pairwise.ai](mailto:support@pairwise.ai) with the name of your assistant, what you asked, and the error text.

## Contributing

Suggestions and fixes are welcome. See [CONTRIBUTING.md](CONTRIBUTING.md).

## License

[MIT](LICENSE). Copyright (c) 2026 Pairwise.
