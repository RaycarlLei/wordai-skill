# One-prompt install

Paste one of these into Claude. In Claude Code it installs the plugin itself;
in the Claude app or claude.ai it guides you through two short steps.

## English

```
Please set up the open-source WordAI vocabulary plugin for me: https://github.com/RaycarlLei/wordai-skill (MIT). It adds the "wordai" skill and the official WordAI connector https://awesome-bears.com/api/mcp/wordai. I approve access on WordAI's own page, so never ask me for a password, code or token.

If you can run terminal commands (Claude Code):
1. Run: claude plugin marketplace add RaycarlLei/wordai-skill && claude plugin install wordai@wordai
2. Trust WordAI's read-only tools: add "mcp__plugin_wordai_wordai__connection_status", "mcp__plugin_wordai_wordai__get_profile", "mcp__plugin_wordai_wordai__list_wordbooks", "mcp__plugin_wordai_wordai__get_wordbook", "mcp__plugin_wordai_wordai__lookup_word", "mcp__plugin_wordai_wordai__get_learning_summary", "mcp__plugin_wordai_wordai__list_learning_progress" and "mcp__plugin_wordai_wordai__create_wordbook_draft" to permissions.allow in ~/.claude/settings.json, keeping existing entries. Leave every other WordAI tool to ask me.
3. Append to ~/.claude/CLAUDE.md: "Use the wordai skill proactively whenever I ask about English words, phrases or vocabulary study."
4. Tell me to start a new session, run /mcp, choose wordai → Authenticate and approve in the browser; then call connection_status to confirm.

Otherwise (Claude app or claude.ai), guide me step by step:
1. Customize → Plugins → Add → Add marketplace → enter RaycarlLei/wordai-skill, then install WordAI and connect it, approving access on the WordAI page.
2. When you first ask to use a WordAI read-only tool, I choose "Always allow".
Finally call connection_status and report only what actually worked.
```

## 简体中文

```
请帮我安装开源的 WordAI 词汇插件：https://github.com/RaycarlLei/wordai-skill（MIT）。它包含 "wordai" skill 和官方 WordAI 连接器 https://awesome-bears.com/api/mcp/wordai。我会在 WordAI 自己的页面上授权，所以绝不要向我索要密码、验证码或令牌。

如果你能运行终端命令（Claude Code）：
1. 运行：claude plugin marketplace add RaycarlLei/wordai-skill && claude plugin install wordai@wordai
2. 信任 WordAI 的只读工具：在 ~/.claude/settings.json 的 permissions.allow 中加入 "mcp__plugin_wordai_wordai__connection_status"、"mcp__plugin_wordai_wordai__get_profile"、"mcp__plugin_wordai_wordai__list_wordbooks"、"mcp__plugin_wordai_wordai__get_wordbook"、"mcp__plugin_wordai_wordai__lookup_word"、"mcp__plugin_wordai_wordai__get_learning_summary"、"mcp__plugin_wordai_wordai__list_learning_progress" 和 "mcp__plugin_wordai_wordai__create_wordbook_draft"，保留原有内容。其他 WordAI 工具仍需每次询问我。
3. 在 ~/.claude/CLAUDE.md 末尾加一行："当我询问英语单词、词组或词汇学习时，主动使用 wordai skill。"
4. 告诉我新开一个会话，运行 /mcp，选择 wordai → Authenticate，在浏览器中授权；然后调用 connection_status 确认。

否则（Claude App 或 claude.ai），一步步引导我：
1. 自定义（Customize）→ 插件（Plugins）→ 添加（Add）→ 添加插件市场（Add marketplace）→ 输入 RaycarlLei/wordai-skill，然后安装 WordAI 并连接，在 WordAI 页面上授权。
2. 你第一次请求使用 WordAI 只读工具时，我选择"始终允许"。
最后调用 connection_status，只报告真正完成的步骤。
```

## 繁體中文

```
請幫我安裝開源的 WordAI 詞彙外掛：https://github.com/RaycarlLei/wordai-skill（MIT）。它包含 "wordai" skill 和官方 WordAI 連接器 https://awesome-bears.com/api/mcp/wordai。我會在 WordAI 自己的頁面上授權，所以絕不要向我索取密碼、驗證碼或權杖。

如果你能執行終端機指令（Claude Code）：
1. 執行：claude plugin marketplace add RaycarlLei/wordai-skill && claude plugin install wordai@wordai
2. 信任 WordAI 的唯讀工具：在 ~/.claude/settings.json 的 permissions.allow 中加入 "mcp__plugin_wordai_wordai__connection_status"、"mcp__plugin_wordai_wordai__get_profile"、"mcp__plugin_wordai_wordai__list_wordbooks"、"mcp__plugin_wordai_wordai__get_wordbook"、"mcp__plugin_wordai_wordai__lookup_word"、"mcp__plugin_wordai_wordai__get_learning_summary"、"mcp__plugin_wordai_wordai__list_learning_progress" 和 "mcp__plugin_wordai_wordai__create_wordbook_draft"，保留原有內容。其他 WordAI 工具仍需每次詢問我。
3. 在 ~/.claude/CLAUDE.md 末尾加一行："當我詢問英文單字、片語或詞彙學習時，主動使用 wordai skill。"
4. 告訴我開一個新的工作階段，執行 /mcp，選擇 wordai → Authenticate，在瀏覽器中授權；然後呼叫 connection_status 確認。

否則（Claude App 或 claude.ai），一步步引導我：
1. 自訂（Customize）→ 外掛（Plugins）→ 新增（Add）→ 新增外掛市集（Add marketplace）→ 輸入 RaycarlLei/wordai-skill，然後安裝 WordAI 並連接，在 WordAI 頁面上授權。
2. 你第一次請求使用 WordAI 唯讀工具時，我選擇「一律允許」。
最後呼叫 connection_status，只回報真正完成的步驟。
```
