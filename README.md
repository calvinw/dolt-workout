# Dolt Codespace

A GitHub Codespace where an AI agent sets up [Dolt](https://www.dolthub.com),
a SQL database with Git-style versioning, and helps you clone, change, commit
and push a database you own on DoltHub.

The codespace has three AI coding agents installed with `npm install -g`:

| Agent | npm package | Command |
|---|---|---|
| OpenCode | `@opencode/cli` | `opencode` |
| Codex | `@openai/codex` | `codex` |
| Claude Code | `@anthropic-ai/claude-code` | `claude` |

`AGENTS.md` tells the agents how to install Dolt, log in to DoltHub and work
with the database, so your prompts can be short.

## Before you start

1. Make an account on [DoltHub](https://www.dolthub.com) and stay signed in.
2. Click **Code → Codespaces → Create codespace on main** on this repo.

## Start OpenCode

1. In the terminal, type `opencode` and press **Enter**.
2. Type `/connect` and press **Enter**. Start typing `openrouter`, highlight
   **OpenRouter**, and press **Enter**.
3. Paste your OpenRouter API key (get one at <https://openrouter.ai/keys>) and
   press **Enter**.

OpenCode starts with **DeepSeek V4.1 Flash** on OpenRouter, set in
`opencode.json`. Use `/models` to switch models.

Treat your API key like a password: paste it only into OpenCode, never into a
file in the repository.

## The exercise

Follow [retail-orders/README.md](retail-orders/README.md). The agent installs
Dolt, logs you in to DoltHub, builds the retail orders database from
`retail-orders/retail-orders.sql`, and pushes it to a new database on your
DoltHub account.

Then do [sales-csv-data/README.md](sales-csv-data/README.md): starting from one
big `sales.csv` file, you and the agent design a database with three tables
(stores, products and sales), build it in Dolt, and push it to DoltHub.

Finally, do [company-analysis/README.md](company-analysis/README.md): the
agent analyzes an existing database,
[calvinw/BusMgmtBenchmarks](https://www.dolthub.com/repositories/calvinw/BusMgmtBenchmarks),
compares two retail companies in two years with charts, and builds a
PowerPoint deck.
