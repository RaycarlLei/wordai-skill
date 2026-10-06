# WordAI MCP tools

Endpoint: `https://awesome-bears.com/api/mcp/wordai` (streamable HTTP, OAuth
2.1 with PKCE and dynamic client registration). The user approves scopes on
WordAI's own consent page and can revoke access in the app under
Settings → AI connections.

The server is the source of truth: always follow the live tool descriptions.
Some tools exist only on newer server versions.

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
| `create_wordbook_draft` | `drafts:write` | Private 7-day draft of 1–100 terms; the user saves it in WordAI |
| `save_word` | `wordbooks:write` | Newer servers: save one term (`mode: explicit` or `auto`) |
| `create_wordbook` / `edit_wordbook` | `wordbooks:write` | Newer servers: create or change a custom word book |
| `delete_wordbook` | `wordbooks:delete` | Newer servers: delete a custom word book after explicit confirmation |

Learning stages are WordAI's own measure, not a CEFR level.

## Links into the WordAI app

These are the only links into WordAI screens to put in answers (see
SKILL.md, section 4). They open the matching screen in the WordAI app, or a
web page that offers the app.

| Link | When | Built from |
|---|---|---|
| `https://awesome-bears.com/wordai/w/{term}` | after explaining a word or phrase, connected or not | the term, `encodeURIComponent`-encoded, case kept |
| `https://awesome-bears.com/wordai/books` | after listing or discussing word books | — |
| `https://awesome-bears.com/wordai/books/{bookId}` | after discussing, creating or editing one book | `books[].id` from `list_wordbooks`, or `bookId` from `save_word` / `create_wordbook` / `edit_wordbook`, unchanged; only if it matches `[A-Za-z0-9_-]{1,80}`, otherwise use `/wordai/books` |
| `https://awesome-bears.com/wordai/review` | after a study plan, review suggestion or progress summary | add `?book={bookId}` when one book applies and its id matches `[A-Za-z0-9_-]{1,80}` |
| `url` from `create_wordbook_draft` | after creating a draft | returned exactly; never rebuilt or shared elsewhere |

The starred collection is a book too: its `id` is `starred_words_default`.
Current book ids are ASCII (`custom_…`, `custom_agent_…`). Some older
imported books have ids with spaces or other scripts: link those with the
general `/wordai/books` or `/wordai/review` instead of their id.
At most one or two links per answer, at the end, as plain Markdown links.
