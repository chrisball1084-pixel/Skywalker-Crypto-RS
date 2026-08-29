# Codex Instructions — Skywalker Crypto RS

Read `docs/PROJECT.md` before making changes.

GitHub is the technical source of truth. The Notion page `Skywalker Crypto RS` is the product source of truth for new ideas, bugs, open requirements, decisions, and product status.

## Standard command: `Notion Sync durchführen`

When asked to run a Notion sync:

1. Read this file and `docs/PROJECT.md`.
2. Read only the current Notion sections: `CURRENT STATE`, `INBOX`, `OPEN`, and relevant `PRODUCT DECISIONS`.
3. Do not read the full historical changelog unless needed.
4. Verify every new request against the current code before implementing it.
5. Classify requests as bug, feature, improvement, question, or user decision.
6. Implement only well-defined changes and keep them as small as practical.
7. Preserve validated RS/market-breadth logic unless there is explicit evidence and approval to change it.
8. Run relevant tests/checks available in the project.
9. Update `docs/PROJECT.md` only for durable technical changes.
10. Update Notion after successful implementation: current state, open items, user decisions, compact changelog.
11. Report what changed, what was tested, and what still needs user input.

Never store API keys, tokens, or other secrets in Git or Notion.
