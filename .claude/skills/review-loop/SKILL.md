---
name: review-loop
description: Make the work, look at what was actually made, have an independent reviewer judge it against a written bar, fix what failed, and go again until it passes. Use for any task where "done" can be checked (code, a web page, a document, an email, a spreadsheet, a design), when the user asks for work they'll rely on, or says "check it before you show me", "make sure it's right", or "review loop".
---

# Review loop

Don't trust what you meant to make. Check what you made.

A loop has three parts: **eyes** (a way to see the real result), **a bar** (what "right" means, written down) and **permission to go again** (fix and re-check before the user sees it).

## 1. Find the bar

Look for the bar in this order:

1. A bar the user gave in the request.
2. `bars/<task>.md` in the project (for example `bars/landing-page.md`).
3. `BAR.md` in the project root.

If there is none, write a short one from the request, using `BAR.md`'s template: what the result must do, the checks that decide it, and any examples of good work the user pointed to. Show it to the user in one or two lines ("I'll judge this against: …") and go on unless they object.

A good bar is checkable. "Looks professional" is not a check; "every heading under 8 words", "loads without errors on a 390 px wide screen" and "all totals match the source sheet" are.

## 2. Make it

Do the work as you normally would.

## 3. Look at the real result

Look at what exists, not at what you wrote. Pick the way that fits:

| What you made | How to look |
|---|---|
| Code | Run it. Run the tests. Run the linter or type checker if the project has one. Read the actual output. |
| A web page | Open it in a browser or take screenshots at phone and desktop width. Click the links and buttons that matter. Check the console for errors. |
| A document or email | Read the final file back from disk, as the reader will get it. Count what the bar counts (words, sections, asks). |
| Data or a spreadsheet | Recompute two or three figures from the source by a different route. Check totals, empty cells and units. |
| An image, slide or design | Render or export it and look at it at full size and at the size it will be seen. |

Write down what you observed, with evidence (the command and its output, the screenshot path, the counts). If something in the bar can't be checked with the tools you have, say so; never mark it as passed.

## 4. Have it judged

Hand the result to the `reviewer` agent (`.claude/agents/reviewer.md`). Give it:

- where the result is (files, URL, screenshots),
- the bar,
- your observations from step 3.

Don't give it your reasoning or your intentions. It judges the result, not the effort. If the reviewer agent isn't installed, review it yourself against the bar, line by line, as a stranger would.

The reviewer answers **PASS**, **NOT YET** or **NO**, with what exactly fails.

## 5. Fix and go again

- **PASS:** go to step 6.
- **NOT YET:** fix only what failed, then go back to step 3. Don't rework what passed.
- **NO:** the approach is wrong, not the details. Say why in one line, change the approach, and start again from step 2.

Stop after **3 rounds** unless the bar or the user sets a different number. A loop that can't converge is telling you something: report it instead of polishing forever.

## 6. Report

Tell the user, briefly:

- the result and where it is,
- how many rounds it took, and what was fixed along the way,
- anything that still doesn't meet the bar, or that couldn't be checked, said plainly.
