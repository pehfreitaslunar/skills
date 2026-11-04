# Skills

Agent skills by Pedro Freitas. They work with any agent that supports the [Agent Skills](https://agentskills.io) format, including Claude Code and Codex.

## Install

```bash
npx skills add pehfreitaslunar/skills --skill=handoff
```

Restart your agent if the skill does not show up.

## handoff

Turns the current session into a portable brief that another agent, tool or teammate can pick up cold.

**When to use it:** when the work has to move somewhere the current session cannot follow:

- switching tools (for example Claude Code to Codex)
- moving to another folder or repository
- passing the work to a colleague
- splitting off a side task while you keep going

If you are staying in the same tool and the same folder, your agent's built-in compact command is usually enough.

**How to use it:**

1. In the session you want to hand off, run:

   ```
   /handoff finish the checkout flow
   ```

   The text after the command is optional and tells the skill what the next session should focus on.

2. The skill saves the brief to `~/.handoffs/` and prints the path plus a ready-to-paste line.

3. In the new session, paste that line:

   ```
   Read ~/.handoffs/2026-11-04-checkout-flow.md and continue the work described there.
   ```

**What the brief contains:** goal, where things stand, decisions and the reasons behind them, what was verified versus only assumed, next steps, open questions, references and suggested skills. Secrets are redacted, and anything already written down (specs, PRs, commits) is linked instead of copied.

**What makes it different:**

- Saves to `~/.handoffs/` instead of the temp folder, so the file survives a reboot.
- Separates what was actually verified from what was only assumed, so the next agent does not build on a guess.
- Records why each decision was made, not just what was decided.

## Credits

Inspired by the `handoff` skill in [mattpocock/skills](https://github.com/mattpocock/skills).

## License

[MIT](LICENSE)
