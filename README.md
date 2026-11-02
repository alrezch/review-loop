# review-loop

Make your AI agent check its own work before you see it.

Most AI output isn't bad. The agent just never looked at what it made. This gives a Claude Code agent the three things a loop needs:

- **Eyes**: it looks at the real result (runs the code, opens the page, reads the file back), not at what it meant to make.
- **A bar**: what "right" means, written down, so "looks good" isn't the test.
- **Permission to go again**: an independent reviewer says PASS, NOT YET or NO, and the agent fixes and re-checks before showing you anything.

It works for anything you can check: code, web pages, documents, emails, data, designs.

## Setup (30 seconds)

From your project's folder:

```bash
git clone https://github.com/alrezch/review-loop.git /tmp/review-loop
mkdir -p .claude/skills .claude/agents
cp -r /tmp/review-loop/.claude/skills/review-loop .claude/skills/
cp /tmp/review-loop/.claude/agents/reviewer.md .claude/agents/
cp /tmp/review-loop/BAR.md .
```

This installs it in **this project only** (`.claude/` in the project), not globally, so it doesn't load into projects that don't need it. Commit it with the project and your team gets it too.

## Where to use it

Anywhere "done" can be checked. `USE-CASES.md` walks through 15 situations, from a landing page and a bug fix to a client email, a spreadsheet, a chatbot's answers and a team how-to.

## Use it

1. Fill in `BAR.md`: what the result is for, and the checks that decide it. Examples for a landing page, a client email and a code change are in `examples/`.
2. Ask for the work as usual, and add "use the review loop", or just "check it before you show me".
3. The agent makes it, looks at the result, has the reviewer judge it against the bar, fixes what failed and goes again: up to 3 rounds by default. Then it tells you what it fixed and anything it couldn't.

## What's inside

| File | What it does |
|---|---|
| `.claude/skills/review-loop/SKILL.md` | The loop: find the bar, make, look, judge, fix, report |
| `.claude/agents/reviewer.md` | An independent reviewer that never saw how the work was made |
| `BAR.md` | The template for your bar |
| `examples/` | Ready bars for a landing page, a client email and a code change |
| `USE-CASES.md` | 15 situations where the loop helps (code, pages, emails, data, agents, slides, translations…), each with its bar, how to look and what it usually catches |

## Why a separate reviewer

The agent that made something is the worst judge of it: it knows what it meant, so it sees that instead of what's there. The reviewer gets only the result and the bar.

## License

MIT. Use it, change it, make it yours.

Made by Aliz ([@builtbyalizz](https://instagram.com/builtbyalizz)).
