# claude-skills

Skills for [Claude Code](https://claude.com/claude-code).

## fresh-start

Writes a handoff document for the current conversation so a fresh session can pick up the work, then offers that fresh session.

Based on the `handoff` skill by Matt Pocock, renamed so the two can be installed side by side ([mattpocock/skills](https://github.com/mattpocock/skills), `skills/productivity/handoff`, MIT). Two changes from the original:

- **The file is saved where it lasts.** The original saves to the system temp folder, which the system cleans out. This version saves to `~/.claude/handoffs/<project>/YYYY-MM-DD-<slug>.md`: outside the project, so it is never committed, and kept until you delete it.
- **It offers the new session.** In the Claude desktop app, after writing the file it puts up a card that starts a new session with "read the handoff and continue" in one click. Where that isn't available (the terminal CLI, for example), it gives the path and a line to paste. It never clears or compacts the current conversation.

### Install

Copy the folder into your skills directory:

```bash
git clone https://github.com/zach2940/claude-skills.git
cp -r claude-skills/skills/fresh-start ~/.claude/skills/fresh-start
```

Then run it in any session with `/fresh-start`, optionally followed by what the next session is for:

```
/fresh-start finish the migration and open the pull request
```

### Notes

- The skill only runs when you type `/fresh-start`; Claude does not invoke it by itself.
- The card relies on a tool that exists in the Claude desktop app's Code tab. The rest works anywhere.
- It asks Claude to leave out keys, passwords and personal details, and to point at existing specs, issues and commits by path or URL instead of repeating them.

## Licence

MIT. See [LICENSE](LICENSE). The original skill is copyright Matt Pocock.
