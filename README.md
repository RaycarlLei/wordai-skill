# WordAI for Claude

Open-source Claude plugin and Agent Skill for [WordAI](https://awesome-bears.com/wordai),
the English dictionary and vocabulary-learning app. Ask Claude about any
English word or phrase and it explains it, links you straight to that word in
WordAI, and, when it helps, uses your own WordAI word books, starred words and
learning progress to personalise the answer, and saves, edits and deletes
your word books directly when you ask. Deleted books and removed words stay
in WordAI's trash for 7 days, and can be restored within that time.

- **Skill** `wordai`: tells Claude when and how to help with vocabulary,
  proactively, without you having to mention WordAI.
- **Connector**: the official WordAI MCP server
  `https://awesome-bears.com/api/mcp/wordai` (OAuth 2.1 + PKCE). You sign in
  and approve access on WordAI's own page. No password, code or
  token ever goes into a chat.

## One tap back to WordAI

After the answer, Claude adds one short link that opens the right screen in
the WordAI app, or a page that helps you get it. Links always come after the
full explanation, at most one or two per answer, and only where they help.

| After | Link | Label (EN · 简体 · 繁體) |
|---|---|---|
| explaining a word or phrase | `https://wordai.awesome-bears.com/w/{term}` | Open in WordAI · 在 WordAI 中查看 · 在 WordAI 中查看 |
| talking about your word books | `https://awesome-bears.com/wordai/books` or `…/books/{bookId}` | Open your word books in WordAI · 在 WordAI 中打开单词本 · 在 WordAI 中開啟單字本 |
| a study plan or progress summary | `https://awesome-bears.com/wordai/review` (`?book={bookId}`) | Review with flash cards in WordAI · 在 WordAI 中用闪卡复习 · 在 WordAI 中用閃卡複習 |
| saving or editing a word book | `https://awesome-bears.com/wordai/books/{bookId}` | Open “…” in WordAI · 在 WordAI 中打开「…」 · 在 WordAI 中開啟「…」 |

The word link works even before you connect your WordAI account.

## Install

### Claude app and claude.ai

1. Open **Customize → Plugins → Add → Add marketplace** and enter
   `RaycarlLei/wordai-skill`.
2. Install **WordAI**, then connect it and approve access on the WordAI page.

### Claude Code

```
/plugin marketplace add RaycarlLei/wordai-skill
/plugin install wordai@wordai
```

Then run `/mcp`, choose **wordai** → **Authenticate** and approve access in the
browser.

### Or paste one prompt

Copy the prompt in [INSTALL_PROMPT.md](INSTALL_PROMPT.md) into Claude. In
Claude Code it installs everything itself; in the Claude app it walks you
through the few taps above.

## What Claude can access

Only what you approve. By default a connection gets full word-book access:
Claude can read your word books, starred words, learning progress and opt-in
search history, and save words, create, rename, edit and delete word books
directly when you ask, without a confirmation step. Deleted books and
removed words go to WordAI's trash for 7 days and can be restored by
asking Claude. Claude makes a private draft for you to review only
when you ask for one. Revoke access anytime in the WordAI app under
**Settings → AI connections**.

- Privacy and terms: https://awesome-bears.com/wordai/terms
- Support: contact@awesome-bears.com

## Repository layout

```
.claude-plugin/marketplace.json        marketplace "wordai"
plugins/wordai/.claude-plugin/plugin.json
plugins/wordai/.codex-plugin/plugin.json   ChatGPT and Codex package
plugins/wordai/.mcp.json               WordAI connector
plugins/wordai/skills/wordai/SKILL.md  the skill (links: section 4)
plugins/wordai/skills/wordai/references/tools.md  tools, scopes, link mapping
```

MIT licensed.
