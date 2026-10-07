---
name: sandbox
description: Run code and shell commands in a clean, isolated Boxline machine instead of on the user's computer - try a script, install a package, reproduce a bug, or check what a command prints. Use when the user asks to run, test or try code, or when running it locally would be unsafe.
---

# Run code in a Boxline sandbox

A Boxline session with a shell is a fresh Linux machine of its own (Node, Python, git and a browser), with `/workspace`
as its disk. Nothing in it touches the user's computer. It uses the user's Boxline credit while it runs.

## Steps

1. `session_create` with `shell: true`. Keep the `sessionId` it returns and pass it to every other tool.
2. Put files in place with `write_file` (paths under `/workspace`), or fetch them inside the machine with `run_command`
   (for example `git clone …` or `curl -O …`).
3. Run things with `run_command` (bash; it returns the output and the exit code). Give long jobs a `timeoutMs`.
   For browser scripts, `run_playwright` runs Playwright code against the machine's own Chrome.
4. Read results with `read_file` or `list_files`, and report what happened: the command, the exit code, and the
   important lines of output (not pages of logs).
5. When finished, `session_stop` (saves it and stops billing) or `session_delete` (nothing to keep). Say which.

## The disk

- `/workspace` is the machine's disk. Use it for downloads, cloned repositories, build output and results.
- `list_files` shows a folder with sizes, `read_file` returns a text file, `write_file` creates or replaces one, and
  `delete_file` removes one.
- To check space, use `run_command` with `df -h /workspace` and `du -sh /workspace/*`.
- `session_stop` keeps the disk as it is, and `session_resume` brings it back for a later step. `session_delete` erases
  it.
- To hand a result to the user, read it back (`read_file`) or put it somewhere they can reach, and say where.

## Rules

- Show the user any command that changes something outside the machine (pushing code, calling an API with their key)
  and ask first.
- Never put the user's secrets in files or commands unless they gave them for this.
- Do not run anything meant to attack, scan or flood other systems.
