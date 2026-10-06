# WordAI MCP tools

Endpoint: `https://awesome-bears.com/api/mcp/wordai` (streamable HTTP, OAuth
2.1 with PKCE and dynamic client registration). The user approves scopes on
WordAI's own consent page and can revoke access in the app under
Settings → AI connections.

The server is the source of truth: always follow the live tool descriptions.
Some tools exist only on newer server versions.

| Tool | Scope | Purpose |
|---|---|---|
| `connection_status` | — | Connected account, granted scopes, preferences (e.g. `autoSaveVocabulary` on newer servers) |
| `get_profile` | — | Distinguish the connected account; not for identifying a person |
| `list_wordbooks` | `wordbooks:read` | The user's word books (starred, custom, built-in) |
| `get_wordbook` | `wordbooks:read` | Words in one book; page with `nextCursor` / `nextOffset` |
| `lookup_word` | `dossier:read` or `wordbooks:read` | Published WordAI entry, or (newer servers) a search of the user's saved words |
| `get_learning_summary` | `learning:read` | Overall learning stages |
| `list_learning_progress` | `learning:read` | Per-sense progress (not started / passed in context / learned) |
| `list_search_history` | `history:read` | Opt-in recent searches, kept up to 90 days |
| `create_wordbook_draft` | `drafts:write` | Private 7-day draft of 1–100 terms; the user saves it in WordAI |
| `save_word` | `wordbooks:write` | Newer servers: save one term (`mode: explicit` or `auto`) |
| `create_wordbook` / `edit_wordbook` | `wordbooks:write` | Newer servers: create or change a custom word book |
| `delete_wordbook` | `wordbooks:delete` | Newer servers: delete a custom word book after explicit confirmation |

Learning stages are WordAI's own measure, not a CEFR level.
