# Workflow

How the skills and the browser automation fit into a normal testing task.

## 1. Understand the feature

Read the story, the design and the change. Ask the `test-charter` skill for charters, then edit them: remove what is already well covered by automation, add what you know from past bugs in the area.

## 2. Explore

Run the sessions yourself. For repetitive checks, the Playwright MCP server lets Claude drive a browser while you watch:

- "Open the store, log in as the standard user and try to check out with an empty cart. Tell me exactly what each page shows."
- "Add every product to the cart one by one and report which buttons did not change."

The model reports what it sees through the page's accessibility tree. Treat that as a lead. Confirm anything that will go into a report with your own eyes or a screenshot.

Use this only on test environments and public demo sites. Do not let an agent drive a browser that is logged in to real accounts.

## 3. Report

Paste your notes into the `bug-report` skill. Read the result against your notes, answer the open questions it lists, and set the severity yourself.

## 4. Automate

Write the regression tests for the paths that must not break. If a model drafts them, run the `playwright-test-review` skill on the draft and then read the tests yourself. Run new tests repeatedly on every browser before trusting them.

## 5. Keep a record of what the AI got wrong

When a generated test or report turns out to be wrong, add the pattern to the review checklist in `playwright-test-review`.

## Setting up the Playwright MCP server

The `.mcp.json` in this repository registers the server for Claude Code:

```json
{
  "mcpServers": {
    "playwright": {
      "command": "npx",
      "args": ["@playwright/mcp@latest"]
    }
  }
}
```

Place it in the root of your project and restart Claude Code. The first run downloads the server with `npx`.
