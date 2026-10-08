---
name: sandbox
description: Run code and shell commands in a clean, isolated Boxline machine instead of on the user's computer - try a script, install a package, reproduce a bug, or check what a command prints. Use when the user asks to run, test or try code, or when running it locally would be unsafe.
---

# Run code in a Boxline sandbox

A Boxline session with a shell is a fresh Linux machine of its own (Node, Python, git and a browser), with `/workspace`
as its disk. Nothing in it touches the user's computer. It uses the user's Boxline credit while it runs.

## Steps

1. `session_create` with `shell: true`, and `browser: false` when no browser is needed (a shell-only machine has no live
   view and its browser tools are refused). Keep the `sessionId` it returns and pass it to every other tool;
   `session_list` finds it again.
2. Put files in place with `files_write` (paths under `/workspace`), or fetch them inside the machine with `shell_exec`
   (for example `git clone …` or `curl -O …`).
3. Run things with `shell_exec` (bash; it returns the output and the exit code). Give long jobs a `timeoutMs`, or start
   them in the background (`nohup … > job.log 2>&1 &`) and read `job.log` later. A machine that has a browser can also
   be driven with `browser_act`.
4. Read results with `files_read` or `files_list`, and report what happened: the command, the exit code, and the
   important lines of output (not pages of logs).
5. When finished, `session_stop` (saves it and stops billing) or `session_delete` (nothing to keep). Say which.

## The disk

- `/workspace` is the machine's disk. Use it for downloads, cloned repositories, build output and results.
- `files_list` shows a folder with sizes, `files_read` returns a text file, `files_write` creates or replaces one, and
  `files_delete` removes one.
- To check space, use `shell_exec` with `df -h /workspace` and `du -sh /workspace/*`.
- `session_stop` keeps the disk as it is, and `session_resume` brings it back for a later step. `session_delete` erases
  it.
- To hand a result to the user, read it back (`files_read`) or put it somewhere they can reach, and say where.

## Rules

- Show the user any command that changes something outside the machine (pushing code, calling an API with their key)
  and ask first.
- Never put the user's secrets in files or commands unless they gave them for this.
- Do not run anything meant to attack, scan or flood other systems.
