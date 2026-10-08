---
name: browse
description: Use a real cloud browser with Boxline - open pages, read them as rendered, click, type, scroll and take screenshots, then stop the machine. Use when a task needs an actual browser (a page built by JavaScript, a flow across several pages, a form, a screenshot), not just the text of a page.
---

# Browse with Boxline

Each Boxline session is an isolated cloud machine with Chrome, a shell and a disk. It is the user's own, and it uses
their Boxline credit while it runs, so start one only when a browser is really needed, and stop it when done.

## Steps

1. `session_create` starts a machine and returns its `sessionId`. Pass that `sessionId` to every other session tool;
   `session_list` finds it again if you lose it.
2. `browser_navigate` opens a URL. `browser_read` returns the page as markdown (or text);
   `browser_screenshot` shows it when the layout matters.
3. Act on the page with `browser_click` (a CSS selector, or x/y from a screenshot), `browser_type` and `browser_press`
   (`Enter`, `Control+A`, `ctrl+a Delete`). For anything else (hover, scroll, drag, a right or double click) or several
   steps at once, use `browser_act`: each step is a sentence ("scroll to the pricing table") or an exact action such as
   `{"action": "hover", "selector": "text=Products"}`. A sentence is carried out by a model, so prefer exact actions when
   you know the selector. Read or screenshot again after each step that changes the page, to confirm what happened.
4. Files: `files_list`, `files_read` and `files_write` work in the machine's `/workspace`.
5. When the task is done, call `session_stop` (it saves the machine as it is and stops billing; `session_resume` brings
   it back) or `session_delete` if nothing needs keeping. Tell the user which one you did.

## Rules

- Ask before anything with consequences: submitting a form, posting, buying, sending a message, deleting.
- Sign in only to the user's own accounts, and only when they ask; never type a password they did not give for that.
- Never try to get past a CAPTCHA, a bot check or a block: stop and tell the user.
- A read-only tool given a stopped session asks for `session_resume`; call it, then retry.
- If a step fails twice, take a screenshot, explain what you see, and ask how to go on.
