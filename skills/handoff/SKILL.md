---
name: handoff
description: Turn the current session into a portable brief that another agent, tool or teammate can pick up cold. Run it with /handoff, optionally followed by what the next session should focus on.
argument-hint: "What should the next session focus on?"
disable-model-invocation: true
---

# Handoff

Your job is to write a brief that lets someone with zero context continue this work. The reader might be a fresh agent in another tool, an agent in another repository, or a colleague. Assume they cannot see this conversation and cannot ask you anything.

## 1. Decide the focus

If the user passed text after `/handoff`, that is the goal of the next session. Keep only what serves that goal and drop the rest, however interesting. If they passed nothing, the focus is "continue the current task".

## 2. Write the brief

Use exactly these sections, in this order. Skip a section only if it would be empty.

```markdown
# Handoff: <short title>

Created: <date and time> · From: <tool/agent> · Repo: <path or URL> · Branch: <branch>

## Goal
One or two sentences: what the next session must achieve and what "done" looks like.

## Where things stand
What is finished, what is half done, what has not started. Be concrete: files, functions, endpoints.

## Decisions and why
Each decision taken in this session, with the reason and any option that was rejected.
The reason matters more than the decision: without it, the next agent will reopen the debate.

## Verified vs assumed
- Verified: things you actually checked (a test ran green, you read the file, you saw the output).
- Assumed: things believed but never checked.
Never move an item to "Verified" unless you checked it in this session.

## Next steps
A numbered list, in the order you would do them. The first step must be doable immediately.

## Open questions
Anything that needs a human decision, and who is likely to know.

## References
Paths, URLs, commits, PRs, issues, specs, docs. Link them, do not paste their contents.

## Suggested skills
Skills or commands the next agent should load, and when to use each one.
```

## 3. Rules

- **Reference, don't copy.** If something already lives in a file, commit, PR, issue or doc, point to it. The brief should be a small fraction of the conversation.
- **No secrets.** Remove API keys, tokens, passwords, connection strings, private customer data and personal information. Write `<redacted>` and say where the real value lives (for example "in `.env.local`, key `STRIPE_SECRET_KEY`").
- **Plain language.** Write for a reader who joins cold. Define any nickname or shorthand the session invented.
- **Absolute facts only.** Use real dates instead of "today" or "yesterday", and full paths instead of "the file we changed".

## 4. Save it somewhere durable

Save the brief to `~/.handoffs/<YYYY-MM-DD>-<short-slug>.md`, creating the folder if needed. Do not use the system temp folder: it can be wiped on reboot, and a handoff often waits a day before someone picks it up. Do not save it inside the project unless the user asks, so it never ends up in a commit by accident.

## 5. Tell the user how to use it

Finish by printing:

1. The full absolute path of the file.
2. A ready-to-paste line for the next session:

   ```
   Read <absolute path> and continue the work described there. Check anything listed under "Assumed" before relying on it.
   ```

3. A one-line reminder to skim the brief before passing it on, especially the "Verified vs assumed" section.

Tell the user to point the next agent at the file instead of pasting the brief into a shell command, because shells can silently mangle backticks and `$` signs.
