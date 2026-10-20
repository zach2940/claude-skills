---
name: fresh-start
description: Write a handoff document for the current conversation and offer a fresh session that starts from it.
argument-hint: "What will the next session be used for?"
disable-model-invocation: true
---

Write a handoff document summarising the current conversation so a fresh agent can continue the work. Save it where it will still be there in a week and cannot be committed by accident: `~/.claude/handoffs/<project-folder-name>/YYYY-MM-DD-<short-slug>.md` (create the folders if needed; use `%USERPROFILE%\.claude\handoffs\...` on Windows). Do not save it inside the project or a worktree.

Include a "suggested skills" section in the document, naming which skills the next agent should call the Skill tool for.

Do not duplicate content already captured in other artifacts (specs, plans, ADRs, issues, commits, diffs). Reference them by path or URL instead.

Redact any sensitive information, such as API keys, passwords, or personally identifiable information.

If the user passed arguments, treat them as a description of what the next session will focus on and tailor the doc accordingly.

After the file is written, offer the fresh session as a card the user starts with one click. The prompt for it gives the handoff file's absolute path and says to read it in full and continue from it (starting with what the user's arguments named, else the first open item). Use the first of these tools the session has; a tool listed only as deferred is loaded first with ToolSearch (`select:<name>`), alone in its message:

1. `mcp__ccd_session__start_session` (the current desktop app): call it once with `initiation: "own_initiative"`, `context: "fresh"`, `title` such as "Continue: <topic>", `prompt` as above, and `background` (at least 80 characters): a one-line summary of what the new session will pick up and that the handoff file holds the rest.
2. `mcp__ccd_session__spawn_task` (older app versions): call it once with the same prompt, a title such as "Continue: <topic>", and a one-line summary of what the new session will pick up.

Then tell the user in one or two lines where the file is, that one click on the card starts a new session with it, and that this conversation stays in the sidebar. If neither tool is available, give the path and the one line to paste into a new session instead. Do not clear or compact the current conversation.
