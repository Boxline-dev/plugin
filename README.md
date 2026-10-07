# Boxline

Give your AI agents the infrastructure they need: browsers, shells, storage and isolated machines.

This plugin connects your assistant to Boxline. Your assistant can then do the following, each in an isolated cloud
machine of your own:

- search the web;
- crawl a site;
- scrape structured data from pages;
- read pages as a real browser renders them;
- click, type and take screenshots;
- run code and commands in a clean sandbox.

It works in ChatGPT, Codex, Claude, Claude Code and Cowork.

## What's inside

- **The Boxline MCP server**, hosted at `https://mcp.boxline.dev/mcp`. When you connect, you sign in with your Boxline
  account (OAuth) and choose the project to use. Your assistant never sees a password or an API key.
- **Skills:**
  - `web-research`: search, read the best sources and answer with links;
  - `crawl-site`: read a whole site or section, respecting robots.txt;
  - `scrape`: pull structured data (JSON) out of pages;
  - `browse`: use a real browser, step by step;
  - `sandbox`: run code and shell commands in a clean machine, with its own disk.

## What it sends where

When your assistant uses a tool, the plugin sends that request to Boxline. A request can be a search, a URL to open, a
click, text to type, a file, or a command to run. Boxline runs it in your machine and sends back the result: page text,
a screenshot, or command output.

- **Billing:** machines use your Boxline credit while they run. The skills stop them when a task is done.
- **What stays out of the results:** saved passwords and live-view links.
- **Your control:** you can see and stop every session in the [Boxline console](https://app.boxline.dev). You can
  disconnect the app at any time under **Settings → Connected apps**.
- **Privacy:** see the [privacy policy](https://boxline.dev/legal/privacy) and the [terms](https://boxline.dev/legal/terms).

## Install

- **ChatGPT and Claude:** find **Boxline** in the plugin directory, then **Connect**.
- **Claude Code:**
  ```bash
  claude plugin marketplace add Boxline-dev/plugin
  claude plugin install boxline@boxline
  ```

Docs: [docs.boxline.dev/mcp](https://docs.boxline.dev/mcp). Problems or questions:
[open an issue](https://github.com/Boxline-dev/plugin/issues).

---

This repository holds the Boxline plugin for ChatGPT, Codex, Claude and Claude Code. It is copied from Boxline's main repository on every change. Issues and pull requests are welcome here; accepted changes are made there and arrive with the next copy.
