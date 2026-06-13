# Connect Acrool with MCP-Compatible AI Assistants

[Documentation Home](README.md) | [繁體中文](locales/zh-TW/connect-acrool-mcp.md)

Acrool provides an MCP (Model Context Protocol) server so AI assistants such as Claude Desktop, Claude Code (CLI), and OpenAI Codex CLI can read and update your Acrool tasks directly inside a conversation.

## Table of Contents

- [What is this?](#what-is-this)
- [Connection Details](#connection-details)
- [Authentication](#authentication)
- [Connect Claude Desktop (OAuth)](#connect-claude-desktop-oauth)
- [Connect Claude Code (CLI)](#connect-claude-code-cli)
- [Connect OpenAI Codex CLI (v0.137.0+)](#connect-openai-codex-cli-v01370)
- [Available Tools and Required Scopes](#available-tools-and-required-scopes)
- [Troubleshooting](#troubleshooting)

## What is this?

Once Acrool is connected to an MCP-compatible AI assistant, you can ask the AI directly in a chat to:

- List and view your tasks and projects
- Read task comments and attached images
- Report progress and update task status

## Connection Details

- **MCP endpoint:** `https://api-workspace.acrool.com/mcp`
- **Transport:** HTTP
- **Authentication:** OAuth (recommended) or Personal Access Token (PAT)

## Authentication

| Method | Best for | Notes |
|---|---|---|
| **OAuth** (recommended) | Everyday users | Click "Connect", approve in the Acrool consent page, pick a workspace, and continue without managing a token manually |
| **PAT** (Personal Access Token) | Advanced / CLI automation | Generate a long-lived token in Acrool and pass it as a Bearer token |

### How to generate a PAT

1. Sign in to [Acrool](https://acrool.com/) and open your workspace
2. Go to **Personal Settings -> Personal Access Tokens (API Token)**
3. Create a new token, select the scopes you need (see table below), and copy the `acr_pat_...` value
4. The token is shown only once, so store it safely

> See [docs.acrool.com](https://docs.acrool.com/) for the detailed settings page.

## Connect Claude Desktop (OAuth)

1. Open Claude Desktop -> **Settings -> Connectors**
2. Click **Add custom connector**
3. Paste the MCP endpoint: `https://api-workspace.acrool.com/mcp`
4. Save, click **Connect**, approve in the Acrool authorization page, and pick a workspace
5. Acrool tools are now available in your conversations

## Connect Claude Code (CLI)

**Option A - OAuth:**

```bash
claude mcp add acrool --transport http https://api-workspace.acrool.com/mcp
```

Then run `/mcp` inside Claude Code to trigger the login/authorization flow.

**Option B - PAT:** add this to `.claude/settings.json` in your project root:

```json
{
  "mcpServers": {
    "acrool": {
      "type": "http",
      "url": "https://api-workspace.acrool.com/mcp",
      "headers": {
        "Authorization": "Bearer <YOUR_ACROOL_PAT>"
      }
    }
  }
}
```

Replace `<YOUR_ACROOL_PAT>` with the PAT you generated.

## Connect OpenAI Codex CLI (v0.137.0+)

**Option A - PAT:**

```bash
npx @openai/codex mcp add acrool \
  --url https://api-workspace.acrool.com/mcp \
  --bearer-token-env-var ACROOL_PAT

export ACROOL_PAT=acr_pat_your_token   # add to ~/.zshrc to persist
```

**Option B - OAuth:**

```bash
npx @openai/codex mcp add acrool --url https://api-workspace.acrool.com/mcp
npx @openai/codex mcp login acrool     # opens the browser to authorize
```

Verify with: `npx @openai/codex mcp list`

## Available Tools and Required Scopes

| Tool | Description | Scope |
|---|---|---|
| `acrool_list_my_workspaces` | List accessible workspaces | `tasks:read` |
| `acrool_get_current_workspace` | Get the current default workspace | `tasks:read` |
| `acrool_set_default_workspace` | Switch the default workspace | `tasks:read` |
| `acrool_list_tasks` | List tasks | `tasks:read` |
| `acrool_get_task` | Get task details (with attachments) | `tasks:read` |
| `acrool_get_task_image` | Fetch an attachment image | `tasks:read` |
| `acrool_get_comments` | Get task comments | `comments:read` |
| `acrool_post_comment` | Add a task comment | `comments:write` |
| `acrool_update_status` | Update task status | `status:write` |
| `acrool_get_repo` | Get repository info | `repos:read` |

> A PAT can only call tools within its selected scopes. If a tool returns `Scope '...' is required`, go back to the token settings and add the missing scope.

## Troubleshooting

- **`Scope '...' is required`**: Your PAT is missing a scope; regenerate or edit it with the required permission.
- **Authorization failed / cannot connect**: Confirm the endpoint is exactly `https://api-workspace.acrool.com/mcp` and that your token has not expired.
- **No workspace selected**: Use `acrool_set_default_workspace`, or include a `workspaceId` when a tool asks for it.
