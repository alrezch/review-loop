# Where to use the loop: 15 situations

Each one has the bar (what "right" means), how the agent looks at the real result, and the kind of thing the loop usually catches. Copy the bar into `BAR.md` or `bars/<task>.md` and change it to fit.

---

## 1. A landing page

**Bar:** the headline says what the business does in under 10 words · the main button is visible without scrolling on a phone · every link works · no console errors · nothing overflows sideways at 390 px.
**Look:** open it in a browser at phone and desktop width, take screenshots, click every button, read the console.
**Usually catches:** a button that points to `#`, a hero image that pushes the call to action below the fold, text cut off on small screens.

## 2. A bug fix

**Bar:** a test reproduces the bug and fails before the fix · it passes after · the whole test suite still passes · nothing unrelated changed.
**Look:** run the new test on the old code, then on the new code, then the full suite. Read the diff.
**Usually catches:** a "fix" that hides the symptom, a test that passes either way, a stray edit in another file.

## 3. A new feature

**Bar:** it does what the request says, end to end, as a user would use it · tests cover the main path and one failure path · the type checker and linter pass.
**Look:** run the app and use the feature yourself, then run the checks.
**Usually catches:** a feature that works in the function but isn't wired into the screen, an error state nobody handled.

## 4. A client email or proposal

**Bar:** under 150 words (or the length agreed) · the first sentence says why you're writing · exactly one ask, with a date · every name, amount and date matches the source.
**Look:** read the final text back as the client will see it, count words, check each figure against the brief or invoice.
**Usually catches:** the wrong client name from an earlier draft, two asks instead of one, a price that doesn't match the quote.

## 5. A report or summary of documents

**Bar:** every claim points to the page or line it came from · nothing in it is missing from the sources · the main conclusion is in the first paragraph · the length fits.
**Look:** pick three claims at random and find them in the sources; search the sources for anything important the summary skipped.
**Usually catches:** a confident sentence that isn't in any source, a key exception left out.

## 6. Data cleaning or a spreadsheet

**Bar:** row counts before and after are explained · no empty cells in required columns · totals match the source · units and date formats are consistent.
**Look:** count rows, recompute two or three totals by a different route (a pivot, a script, by hand), scan for blanks and outliers.
**Usually catches:** duplicated rows from a merge, dates read as text, a total off by a filtered-out row.

## 7. A chart or dashboard

**Bar:** every number on it matches the data · axes are labelled with units · the chart answers the question it's for · it reads at the size it'll be seen.
**Look:** check three plotted values against the data, export the chart and view it at its real size.
**Usually catches:** a y-axis that doesn't start where it should, a legend in the wrong order, numbers too small to read.

## 8. An automation or workflow

**Bar:** it runs end to end on a real example · it handles the empty case and the error case · it doesn't run twice for one trigger · someone is told when it fails.
**Look:** trigger it with a real test input, then with a bad one; read the logs; check what landed in the destination.
**Usually catches:** a step that silently does nothing on an empty field, duplicate records, a failure nobody would ever see.

## 9. An AI agent or chatbot's answers

**Bar:** it answers 10 real questions correctly from your own material · it says "I don't know" when the answer isn't there · it never invents prices, dates or policies · the tone fits the brand.
**Look:** ask it the 10 questions plus 3 it shouldn't be able to answer, and compare every answer with the source.
**Usually catches:** a made-up opening time, a confident answer to a question your material doesn't cover.

## 10. A presentation or slides

**Bar:** one idea per slide · every slide readable from the back of the room (no text under the size you set) · the numbers match the source · the story runs in order.
**Look:** export it, view every slide at full size and as thumbnails, read only the titles in order: do they tell the story?
**Usually catches:** a slide with three ideas, a chart from an old version of the data, titles that don't connect.

## 11. Social media posts or captions

**Bar:** the first line makes sense on its own (it's all people see) · one clear point · no claim you can't back · hashtags and mentions are correct.
**Look:** read the first line alone, check every claim against its source, check every @mention exists.
**Usually catches:** a first line that needs the second to make sense, a statistic with no source.

## 12. A product description or listing

**Bar:** the size, material and price match the product sheet · the first sentence says what it is and who it's for · no claim the product can't back ("waterproof", "best") · under the platform's length limit.
**Look:** compare every specification with the product sheet, count characters, read it on a phone.
**Usually catches:** a dimension copied from a similar product, a claim the supplier never made.

## 13. A translation

**Bar:** every number, name and date survives unchanged · nothing is left untranslated · the length fits the layout · the terms match your glossary.
**Look:** compare the numbers and names side by side, search for words left in the source language, place it in the real layout.
**Usually catches:** a date format flipped, a term translated two different ways, a button label too long for the button.

## 14. A database change or migration

**Bar:** it runs on a copy of real data without errors · row counts are the same before and after (or the difference is explained) · it can be undone · the app still works after it.
**Look:** run it on a copy, count rows in the affected tables, run the undo, run the app's tests against the migrated copy.
**Usually catches:** a column made not-null that has empty rows, an undo that doesn't actually undo.

## 15. A process or how-to document for your team

**Bar:** someone new can follow it without asking anything · every step is something you can do (not "make sure that…") · every link and tool name is current · it says what "done" looks like.
**Look:** have the reviewer follow it literally, step by step, and stop at the first step it can't do with only what's written.
**Usually catches:** a step that assumes knowledge, a link to an old tool, no way to tell when you're finished.

---

The pattern is the same every time: write what "right" means before you start, look at what was actually made, let someone who didn't make it judge, fix only what failed, go again.
