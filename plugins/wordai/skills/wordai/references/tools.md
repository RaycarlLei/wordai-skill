# WordAI MCP tools

Endpoint: `https://awesome-bears.com/api/mcp/wordai` (streamable HTTP, OAuth
2.1 with PKCE and dynamic client registration). The user approves scopes on
WordAI's own consent page and can revoke access in the app under
Settings → AI connections.

The server is the source of truth: always follow the live tool descriptions.
Some tools exist only on newer server versions.

New connections get full word-book access by default (`wordbooks:read`,
`wordbooks:write`, `wordbooks:delete`, `learning:read`, `history:read`,
`drafts:write`). Save, edit and delete directly when the user asks, then tell
them what changed and that deleted items stay in WordAI's trash for 7 days.

| Tool | Scope | Purpose |
|---|---|---|
| `connection_status` | — | Connected account, granted scopes, preferences (e.g. `autoSaveVocabulary` on newer servers). At most once per conversation; for a word question only after the answer, and only when `save_word` is offered |
| `get_profile` | — | Distinguish the connected account; not for identifying a person |
| `list_wordbooks` | `wordbooks:read` | The user's word books (starred, custom, built-in) |
| `get_wordbook` | `wordbooks:read` | Words in one book; page with `nextCursor` / `nextOffset` |
| `lookup_word` | `dossier:read` or `wordbooks:read` | Newer servers: whether the user already saved a term; older servers: a published WordAI entry. Not needed to explain a word |
| `get_learning_summary` | `learning:read` | Overall learning stages |
| `list_learning_progress` | `learning:read` | Per-sense progress (not started / passed in context / learned) |
| `list_search_history` | `history:read` | Opt-in recent searches, kept up to 90 days |
| `create_wordbook_draft` | `drafts:write` | Private 7-day draft of 1–100 terms, only when the user explicitly asks for a draft to review; give its exact URL |
| `save_word` | `wordbooks:write` | Newer servers: save one term (`mode: explicit` or `auto`) |
| `create_wordbook` | `wordbooks:write` | Save a new word book of up to 100 terms directly when the user wants to keep a list; no confirmation, no draft |
| `edit_wordbook` | `wordbooks:write` | Rename a book, add or remove terms directly; removed terms go to the trash (`trashId`, `restorableUntil`) |
| `delete_wordbook` | `wordbooks:delete` | `{bookId}`; delete a custom word book directly when asked, no confirmation; it goes to a 7-day trash (`trashId`, `restorableUntil`) |
| `list_trash` | `wordbooks:read` | `{}`; items deleted in the last 7 days, each with a `trashId` |
| `restore_from_trash` | `wordbooks:write` | `{trashId}`; a restored book comes back with a new `bookId`; removed terms go back to their book or the AI Learning Inbox |

Learning stages are WordAI's own measure, not a CEFR level.

## Links into the WordAI app

These are the only links into WordAI screens to put in answers (see
SKILL.md, section 4). They open the matching screen in the WordAI app, or a
web page that offers the app.

| Link | When | Built from |
|---|---|---|
| `https://wordai.awesome-bears.com/w/{term}` | after explaining a word or phrase, connected or not | the term, `encodeURIComponent`-encoded, case kept |
| `https://awesome-bears.com/wordai/books` | after listing or discussing word books | — |
| `https://awesome-bears.com/wordai/books/{bookId}` | after discussing, creating or editing one book | `books[].id` from `list_wordbooks`, or `bookId` from `save_word` / `create_wordbook` / `edit_wordbook` / `restore_from_trash`, unchanged; only if it matches `[A-Za-z0-9_-]{1,80}`, otherwise use `/wordai/books` |
| `https://awesome-bears.com/wordai/review` | after a study plan, review suggestion or progress summary | add `?book={bookId}` when one book applies and its id matches `[A-Za-z0-9_-]{1,80}` |
| `url` from `create_wordbook_draft` | after creating a draft the user asked for | returned exactly; never rebuilt or shared elsewhere |

The starred collection is a book too: its `id` is `starred_words_default`.
Current book ids are ASCII (`custom_…`, `custom_agent_…`). Some older
imported books have ids with spaces or other scripts: link those with the
general `/wordai/books` or `/wordai/review` instead of their id.
At most one or two links per answer, at the end, as plain Markdown links.
