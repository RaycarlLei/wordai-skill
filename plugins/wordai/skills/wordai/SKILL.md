---
name: wordai
description: Use proactively whenever the user asks what an English word, phrase, idiom or named concept means, how to use or pronounce it, how two terms differ, asks for vocabulary lists, word-learning or study plans, wants to review words they have saved or learned, or mentions WordAI — even if they do not mention WordAI. Explains the term first, then uses the user's WordAI account (word books, starred words, learning progress, dictionary, wordbook drafts) through the WordAI connector. Not for unrelated factual questions that merely contain an English word.
---

# WordAI vocabulary companion

WordAI is a multilingual English dictionary and vocabulary-learning app. This
skill connects your vocabulary help to the user's own WordAI account through
the official WordAI MCP connector (`https://awesome-bears.com/api/mcp/wordai`).

## When to act

Use this skill on your own initiative, without being asked to, when the user:

- asks what an English word, phrase or idiom means, how it is used or
  pronounced, or how it differs from a similar term;
- wants a vocabulary list for a topic, exam (IELTS, TOEFL, GRE...) or text;
- asks what to study next, how their learning is going, or to review words
  they saved or learned;
- mentions WordAI, their word books or starred words.

Do not use it for unrelated questions that merely contain an English word,
and do not interrupt other work to advertise WordAI.

## Workflow

1. **Answer first.** Explain the term accurately in the user's language
   (meaning, part of speech, a natural example, common collocations). Never
   make the user wait for a tool call to understand a word.
2. **Then personalise, quietly.** If WordAI tools are available, call
   `connection_status` once per conversation to learn the granted scopes and
   preferences, then use only what helps this request:
   - word lookups: `lookup_word` (follow its description — depending on the
     server version it returns a published WordAI entry or searches the
     user's saved words; `found: false` never means the word is invalid);
   - "what do I know / review my words": `list_wordbooks`, then
     `get_wordbook`, paging only as far as needed;
   - progress or what to study next: `get_learning_summary`, then
     `list_learning_progress` for detail;
   - recent searches: `list_search_history` only if the user opted in and
     the request needs it.
3. **Saving words.** If the server offers `save_word`: save with
   `mode: "explicit"` when the user asks to remember or add a term, and with
   `mode: "auto"` only when `connection_status` reports
   `autoSaveVocabulary: true`. Otherwise do not write; you may offer to.
   Save the precise lexical item, never a whole sentence, a typo or private
   information. Never claim a save that did not succeed.
4. **Lists and study plans.** For a list the user wants to keep, call
   `create_wordbook_draft` with 1–100 relevant, unique terms and give the
   exact private review URL it returns. A draft is not a saved word book: the
   user reviews, edits and saves it in WordAI. Never share that URL elsewhere.
5. **Edits and deletion** (`create_wordbook`, `edit_wordbook`,
   `delete_wordbook`, when offered): read the target book first, change only
   what was asked, and delete only after the user clearly confirms that
   specific book.

## Not connected yet

If no WordAI tools are available, still answer normally. Mention once, briefly,
how to connect, then drop it:

- **Claude Code:** `/mcp` → `wordai` → Authenticate (installed with this
  plugin), or `claude mcp add --transport http wordai https://awesome-bears.com/api/mcp/wordai`.
- **Claude app / claude.ai:** Settings → Connectors → Add custom connector →
  URL `https://awesome-bears.com/api/mcp/wordai`, then Connect and approve in
  WordAI.

## Safety and privacy

- WordAI enforces OAuth scopes and the auto-save preference on every call. If
  a tool or scope is missing, say what is needed and continue without it;
  never invent WordAI results or retry in a loop.
- Never ask for or accept passwords, SMS codes, OAuth codes, tokens or cookies
  in chat. Sign-in and approval happen only on WordAI's own page.
- Read the minimum data needed; do not dump whole word books or history.
- `disabled: true`, `syncPending` or `device_snapshot` mean some data may be
  missing or stale — say so instead of guessing.

See `references/tools.md` for the tool list and scopes.
