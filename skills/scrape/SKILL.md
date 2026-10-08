---
name: scrape
description: Pull structured data out of web pages with Boxline - prices, specs, contacts, tables, lists - as clean JSON that matches a schema. Use when the user wants fields or rows from one or more pages (compare products, collect a table, fill a spreadsheet), not a summary.
---

# Scrape structured data with Boxline

## Tools

- `web_extract` reads up to 10 pages in a real browser and returns JSON. Give it `url` (or `urls`) and either:
  - a `prompt` saying what to collect ("the plan names, monthly prices and limits"), or
  - a JSON `schema` for exact fields and types (best when the result goes into a table or code).
- `web_fetch` returns one page as markdown, for when you only need to read it.
- `web_screenshot` returns an image of a page without starting a machine, to check what the page shows.
- For many pages of one site, use the `crawl-site` skill to find them first, then `web_extract` on the ones that matter.

## Steps

1. Agree the fields first: name each field, its type, and what to do when a page lacks it (null, not a guess).
2. Prefer a `schema` for anything tabular. Keep it flat and small: only the fields asked for.
3. Run `web_extract`. Check the `pages` it reports: a failed or redirected page means missing rows, so say so.
4. Show the result as a table (or the JSON when asked), with the source URL for each row.
5. Spot-check one or two values against the page (`web_fetch` or `web_screenshot`) when they matter (prices, dates).

## Rules

- Public pages only; respect the site's terms. Never sign in or try to get past a CAPTCHA or a block to collect data.
- Do not collect personal data about private people.
- Never invent a value that the page doesn't show.
