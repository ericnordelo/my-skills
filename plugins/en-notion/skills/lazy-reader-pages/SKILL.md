---
name: lazy-reader-pages
description: Write Notion pages for a reader who will not read them. Turns research, analysis, or review work into a page that looks short, reveals its shape at a glance, and expands on demand. Covers framing, collapsible structure with numbered toggles, concise human language, and the Notion markdown and API details that bite. Use when publishing a study, guide, process document, runbook, or assessment to Notion.
---

# Pages for lazy readers

Assume the reader will not read the page. They will skim the titles, decide whether it applies to them, and open one section at most. Research nobody opens is worth nothing, so design for the skimmer: a page that looks short on arrival, reveals its shape at a glance, and expands only where the reader chooses. Every rule below serves that.

## Frame it before writing

1. **Put the angle in the title.** If the page exists to change how people work, the title should say so. "Incident Response" became "Incident Response by Design" once its purpose was to shape design decisions rather than describe a procedure.
2. **Say who should read it and when, in the first two sentences.** A reader deciding whether this applies to them should not have to guess. For example: "Most of it is about design, which is why it is worth reading before you add anything to the library, not on the day something breaks."
3. **Open with plain paragraphs and no heading.** Two or three at most: what the page is, then the one fact that makes everything else follow.
4. **Put the single most important statement above the fold**, in a callout or a quote. Never bury a load-bearing commitment, definition, or warning inside a collapsed section. If a reader must know one thing, they should not have to click for it.
5. **Keep the front light.** Prose, then at most one callout and one quote. If a paragraph and a quoted block make the same point, shorten the paragraph and let the quote carry the detail. Two shaded blocks in a row read as a wall.

## Structure

6. **Use numbered toggle lists for the main sections, not toggle headings.** Toggle lists are visually compact, and numbering makes a sequence read as a sequence. Ten to twelve top-level items fit on one screen collapsed, where the same count as headings does not.
7. **State the outline tradeoff once.** Toggle lists do not appear in Notion's page outline; toggle headings do. For a page whose collapsed view is already its own map, losing the sidebar is the right trade. Say so rather than letting the user discover it.
8. **Nest one level, never two.** A numbered top-level toggle holds a one-line framing sentence and then its own sub-toggles. Anything deeper should become its own top-level step.
9. **Bold every toggle summary at both levels.** An open toggle whose title looks like body text is disorienting. Top level is bold and numbered, sub-level is bold and indented, so the two stay distinguishable.
10. **One idea per toggle**, one to three short paragraphs. If it needs a second idea, split it or cut it.
11. **Make the steps relate to each other.** Each top-level toggle opens with a framing sentence that follows from the previous step. Cross-reference by number ("see the trap in step 8"), which only works because the steps are numbered.
12. **Titles are claims, not labels.** "Unvetting works, with conditions" beats "Unvetting". Read the titles top to bottom on their own: they should tell the story without any body text.

## Language

13. **Cut filler openers.** Never "worth saying out loud", "there is one thing worth knowing", "worth knowing where the bar sits", "one practical note", "the honest one line summary is that". Say the thing directly.
14. **Name the specific subject.** Vague umbrella nouns hide meaning. "The platform" should be the language, the ledger, the SDK, or the protocol, whichever is actually meant.
15. **Drop rhetorical scaffolding.** "The facts in step 1 are not trivia, they are constraints" is weaker than "Those three facts are constraints."
16. **No em-dashes.** Use a period, comma, colon, or parentheses.
17. **No AI slop**: "crucially", "importantly", "in the ever-evolving landscape", forced rule-of-three lists, or a sentence that restates the previous one.
18. **Keep one voice and one spelling convention.** If the source material is first person plural, stay there for the whole page.

## Revising an existing page

19. **Reframing is reordering, not deleting.** When the angle changes, move content, rewrite framing sentences, and adjust emphasis. Preserve every fact unless it is wrong.
20. **Keep the structure the reader already learned.** If the page is already easy to traverse, a new angle should not change how it is navigated.
21. **Prefer targeted edits over full replacement.** Search-and-replace on exact strings is safer and cheaper than rewriting the body, and it leaves the rest of the page provably untouched.

## Notion markdown that works

Toggle list, tabs for indentation:

```
<details>
<summary>**1. Top level claim**</summary>
	Framing sentence that connects to the previous step.
	<details>
	<summary>**Sub-section claim**</summary>
		Body paragraph.

		Second paragraph.
	</details>
</details>
```

Callout for the one thing that must not be missed:

```
<callout icon="⚠️" color="red_bg">
	Text.
</callout>
```

22. **Wrap bare filenames in backticks.** `SECURITY.md` written plain is auto-linked into a broken `http://SECURITY.md` link. The same happens to anything shaped like a domain.
23. **Never put inline code inside link text.** The link splits into fragments.

## Workflow

24. **Verify every technical claim against a primary source before publishing.** Do not publish from memory, and prefer live documentation over search snippets, which go stale after a docs migration.
25. **Publish, then fetch the page back and read the rendered result.** Nesting, callouts, and auto-linking all fail quietly. Fix and repeat until it reads naturally top to bottom.
26. **Moving a page into a column.** Creating a page as a child appends it at the end of the parent. To relocate it, make one update call on the parent that removes the appended `<page url="...">` tag and reinserts that same tag inside the target column. Adding a fresh tag instead is rejected.
27. **Tell the user what the API cannot do**: set a toggle open by default, and build a column layout around an already published page.
