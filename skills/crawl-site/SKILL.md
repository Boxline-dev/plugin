---
name: crawl-site
description: Crawl a website with Boxline - follow its links from a start page, read every page as a real browser renders it, and return the pages as markdown, a site map or a summary. Use when the user asks to read, map, index, audit or summarize a whole site or a section of it (docs, a blog, a help center), not just one page.
---

# Crawl a site with Boxline

A crawl starts from one URL, follows the site's own links and reads each page in a real browser. It runs on Boxline's
side (no machine for you to manage), respects the site's robots.txt, and stays on the start page's host unless asked.

## Tools

- `web_crawl_start` starts a crawl and waits briefly for it. Options:
  - `url`: the start page;
  - `maxPages` (default 20; the plan's crawl limit applies) and `maxDepth` (default 3);
  - `include` / `exclude`: regular expressions on URLs;
  - `format`: markdown, text or html.

  It returns the pages read so far, or a `crawlId` while it is still running.
- `web_crawl_get` takes a `crawlId` (and `after` to page through) and returns the next pages and whether the crawl has
  finished.
- For one page, `web_fetch` is enough. For something behind clicks or a form, use the `browse` skill.

## Steps

1. Agree the scope in one line if it is unclear: which section, how many pages. Start small (20 pages) and grow only
   if needed.
2. Narrow with `include` (for example `^https://docs\.example\.com/guides/`) rather than crawling everything.
3. Call `web_crawl_start`. While it runs, call `web_crawl_get` with the `crawlId` until it says it has finished.
4. Work from the pages: answer the question, build the site map (title, URL, depth), or summarize each section. Name
   the pages each statement comes from.
5. Report what was skipped: pages refused by robots.txt (`skippedByRobots`), failed pages, and anything cut by
   `maxPages`.

## Rules

- Public pages only. Never crawl behind a sign-in, and never try to get past a CAPTCHA or a block.
- Keep crawls proportionate: no more pages than the task needs, and never the same site over and over.
- Quote sparingly; summarize in your own words.
