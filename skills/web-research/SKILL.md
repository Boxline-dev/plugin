---
name: web-research
description: Research a question on the live web with Boxline - search, read the best sources as a real browser renders them, and answer with links. Use when the user asks about something current, wants sources, or asks to compare what several sites say.
---

# Web research with Boxline

Answer from today's web, not from memory, and show where each fact came from.

## Tools

- `web_search` finds pages (title, link, snippet). No machine is started, so it is quick and cheap.
- `web_fetch` reads one page through a real browser and returns markdown. No machine is started either.
- Only when a page needs clicking, scrolling or signing in to the user's own account, use the `browse` skill instead.

## Steps

1. Turn the question into two or three focused searches and run `web_search` for each.
2. Pick the sources most likely to be right: official docs, the vendor's own pages, primary data, then reputable press.
   Skip content farms and pages that only repeat others.
3. Read each chosen page with `web_fetch` (format `markdown`). Read three to six pages, more only if they disagree.
4. Answer the question first, in a few lines. Then the details, each with its link. Say when sources disagree, and
   which one you trust and why. Give dates when they matter (a release, a price, a rule).
5. If nothing reliable was found, say so plainly instead of guessing.

## Rules

- Quote sparingly; summarize in your own words.
- Read public pages only. Never try to get past a paywall, a sign-in wall, a CAPTCHA or a block: tell the user what
  stopped you.
