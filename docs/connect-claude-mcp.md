# Connect Acrool to Claude / AI Agents (MCP)

Acrool provides an **MCP (Model Context Protocol)** server so AI assistants such as
**Claude Desktop**, **Claude Code (CLI)**, and **OpenAI Codex CLI** can read and update
your Acrool tasks directly inside a conversation.

- **MCP endpoint:** `https://api.workspace.acrool.com/mcp`
- **Transport:** HTTP
- **Authentication:** OAuth (recommended) or Personal Access Token (PAT)

---

## 繁體中文

### 這是什麼？

把 Acrool 連到 Claude 之後，你可以直接在對話裡請 AI：

- 列出 / 查看你的任務與專案
- 讀取任務留言與附件圖片
- 回報執行進度、更新任務狀態

### 認證方式

| 方式 | 適合對象 | 說明 |
|---|---|---|
| **OAuth**（推薦） | 一般使用者 | 點「連接 / 授權」後，瀏覽器開啟 Acrool 同意頁，選擇工作區即可，不需手動管理 token |
| **PAT**（Personal Access Token） | 進階 / CLI 自動化 | 自行在 Acrool 產生長期 token，以 Bearer 方式帶入 |

#### 如何產生 PAT

1. 登入 [Acrool](https://acrool.com/) 並開啟你的工作區
2. 進入**個人設定 → Personal Access Tokens（API Token）**頁面
3. 建立新 token，勾選需要的權限（scope，見下表），複製產生的 `acr_pat_...` token
4. token 只會顯示一次，請妥善保存

> 詳細權限頁面可參考 [docs.acrool.com](https://docs.acrool.com/)。

### 連接 Claude Desktop（OAuth）

1. 開啟 Claude Desktop → **Settings（設定）→ Connectors（連接器）**
2. 點 **Add custom connector（新增自訂連接器）**
3. 貼上 MCP 端點：`https://api.workspace.acrool.com/mcp`
4. 儲存後點 **Connect**，瀏覽器會開啟 Acrool 授權頁，選擇工作區並同意
5. 完成後即可在對話中使用 Acrool 工具

### 連接 Claude Code（CLI）

**方式 A — OAuth：**

```bash
claude mcp add acrool --transport http https://api.workspace.acrool.com/mcp
```

加入後，在 Claude Code 內輸入 `/mcp` 觸發登入授權即可。

**方式 B — PAT：** 在專案根目錄的 `.claude/settings.json` 加入：

```json
{
  "mcpServers": {
    "acrool": {
      "type": "http",
      "url": "https://api.workspace.acrool.com/mcp",
      "headers": {
        "Authorization": "Bearer <YOUR_ACROOL_PAT>"
      }
    }
  }
}
```

將 `<YOUR_ACROOL_PAT>` 替換為你產生的 PAT。

### 連接 OpenAI Codex CLI（v0.137.0+）

**方式 A — PAT：**

```bash
npx @openai/codex mcp add acrool \
  --url https://api.workspace.acrool.com/mcp \
  --bearer-token-env-var ACROOL_PAT

export ACROOL_PAT=acr_pat_你的token   # 建議加入 ~/.zshrc
```

**方式 B — OAuth：**

```bash
npx @openai/codex mcp add acrool --url https://api.workspace.acrool.com/mcp
npx @openai/codex mcp login acrool    # 開啟瀏覽器授權
```

確認設定：`npx @openai/codex mcp list`

### 可用工具與所需權限（scope）

| 工具 | 說明 | Scope |
|---|---|---|
| `acrool_list_my_workspaces` | 列出可存取的工作區 | `tasks:read` |
| `acrool_get_current_workspace` | 取得目前預設工作區 | `tasks:read` |
| `acrool_set_default_workspace` | 切換預設工作區 | `tasks:read` |
| `acrool_list_tasks` | 列出任務列表 | `tasks:read` |
| `acrool_get_task` | 取得任務詳情（含附件清單） | `tasks:read` |
| `acrool_get_task_image` | 取得附件圖片 | `tasks:read` |
| `acrool_get_comments` | 取得任務留言 | `comments:read` |
| `acrool_post_comment` | 新增任務留言 | `comments:write` |
| `acrool_update_status` | 更新任務狀態 | `status:write` |
| `acrool_get_repo` | 取得 Repo 資訊 | `repos:read` |

> PAT 只能使用其勾選 scope 內的工具；若工具回報 `Scope '...' is required`，請回到 token 設定補上對應權限。

---

## English

### What is this?

Once Acrool is connected to Claude, you can ask the AI directly in a chat to:

- List and view your tasks and projects
- Read task comments and attached images
- Report progress and update task status

### Authentication

| Method | Best for | Notes |
|---|---|---|
| **OAuth** (recommended) | Everyday users | Click "Connect", approve in the Acrool consent page, pick a workspace — no token to manage |
| **PAT** (Personal Access Token) | Advanced / CLI automation | Generate a long-lived token in Acrool and pass it as a Bearer token |

#### How to generate a PAT

1. Sign in to [Acrool](https://acrool.com/) and open your workspace
2. Go to **Personal Settings → Personal Access Tokens (API Token)**
3. Create a new token, select the scopes you need (see table below), and copy the `acr_pat_...` value
4. The token is shown only once — store it safely

> See [docs.acrool.com](https://docs.acrool.com/) for the detailed settings page.

### Connect Claude Desktop (OAuth)

1. Open Claude Desktop → **Settings → Connectors**
2. Click **Add custom connector**
3. Paste the MCP endpoint: `https://api.workspace.acrool.com/mcp`
4. Save, click **Connect**, approve in the Acrool authorization page, and pick a workspace
5. Acrool tools are now available in your conversations

### Connect Claude Code (CLI)

**Option A — OAuth:**

```bash
claude mcp add acrool --transport http https://api.workspace.acrool.com/mcp
```

Then run `/mcp` inside Claude Code to trigger the login/authorization flow.

**Option B — PAT:** add this to `.claude/settings.json` in your project root:

```json
{
  "mcpServers": {
    "acrool": {
      "type": "http",
      "url": "https://api.workspace.acrool.com/mcp",
      "headers": {
        "Authorization": "Bearer <YOUR_ACROOL_PAT>"
      }
    }
  }
}
```

Replace `<YOUR_ACROOL_PAT>` with the PAT you generated.

### Connect OpenAI Codex CLI (v0.137.0+)

**Option A — PAT:**

```bash
npx @openai/codex mcp add acrool \
  --url https://api.workspace.acrool.com/mcp \
  --bearer-token-env-var ACROOL_PAT

export ACROOL_PAT=acr_pat_your_token   # add to ~/.zshrc to persist
```

**Option B — OAuth:**

```bash
npx @openai/codex mcp add acrool --url https://api.workspace.acrool.com/mcp
npx @openai/codex mcp login acrool     # opens the browser to authorize
```

Verify with: `npx @openai/codex mcp list`

### Available tools and required scopes

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

> A PAT can only call tools within its selected scopes. If a tool returns
> `Scope '...' is required`, go back to the token settings and add the missing scope.

---

## Troubleshooting

- **`Scope '...' is required`** — Your PAT is missing a scope; regenerate or edit it with the required permission.
- **Authorization failed / cannot connect** — Confirm the endpoint is exactly `https://api.workspace.acrool.com/mcp` and that your token has not expired.
- **No workspace selected** — Use `acrool_set_default_workspace`, or include a `workspaceId` when a tool asks for it.
