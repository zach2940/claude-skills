---
name: handoff
description: Compact the current conversation into a handoff document for another agent to pick up.
argument-hint: "What will the next session be used for?"
disable-model-invocation: true
---

Write a handoff document summarising the current conversation so a fresh agent can continue the work. Save it where it will still be there in a week and will not be committed: `private/handoffs/YYYY-MM-DD-<short-slug>.md` in the project's main checkout (not a worktree, which may be deleted) when the project has a gitignored `private/` folder; otherwise the temporary directory of the user's OS (`$TMPDIR`, else `/tmp`; `%TEMP%` on Windows). Confirm with `git check-ignore` that a file saved inside a project is ignored.

Include a "suggested skills" section in the document, naming which skills the next agent should call the Skill tool for.

Do not duplicate content already captured in other artifacts (specs, plans, ADRs, issues, commits, diffs). Reference them by path or URL instead.

Redact any sensitive information, such as API keys, passwords, or personally identifiable information.

If the user passed arguments, treat them as a description of what the next session will focus on and tailor the doc accordingly.

After the file is written, offer the fresh session: if the `mcp__ccd_session__spawn_task` tool is available, call it once with a prompt that gives the handoff file's absolute path and says to read it in full and continue from it (starting with what the user's arguments named, else the first open item), a title such as "Continue: <topic>", and a one-line summary of what the new session will pick up. Then tell the user in one or two lines where the file is and that one click on the card starts a new session with it, and that this conversation stays in the sidebar. If that tool is not available, give the path and the one line to paste into a new session instead. Do not clear or compact the current conversation.
