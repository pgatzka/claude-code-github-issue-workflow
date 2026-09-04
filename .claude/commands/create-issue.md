---
description: Turn a rough description into a ready GitHub issue, Story, Task, or Bug, resolving every decision first, then create it with labels and native relationships.
argument-hint: [rough description]
---

Create one or more GitHub issues from this request: $ARGUMENTS

Follow these steps in order. Nothing is drafted and nothing is created while a decision is open.

1. Read `.claude/skills/issue-conventions/SKILL.md` in full, then the reference file for the type in the same directory once you know it.
2. Decide the type from the description: Story for a new or changed user-facing feature, Task for a unit of implementation work, Bug for unexpected behavior that should be fixed. If it is ambiguous, ask once, offering the choice between the types with a one-line reason for each.
3. Readiness check, before any drafting. Read the repository for context. Then work out every decision the implementer would face that the request does not answer, applying the readiness rule in `SKILL.md`. Present them together in one round, each with a recommended option and a one-line reason, so they can be answered quickly. Do not ask about things the repository already answers, and do not ask about the cause of a problem or the shape of a solution the implementer will work out. Repeat only if the answers open genuinely new decisions.
4. If the work looks like a feature spanning more than one area, delegate to the `issue-splitter` agent and propose a Story with child Tasks, one per area.
5. Delegate drafting to the `issue-author` agent, one call per issue, passing the type, the request, and the resolved decisions. If it comes back with unresolved decisions, return to step 3 rather than creating anything.
6. Determine the area from the repository structure and the allowed list in `labels.md`. If a new area label is needed, propose it and wait for confirmation before adding it to `labels.md`.
7. Check every drafted issue: the title follows `titles.md`, the labels include exactly one type label, and the body has no question, no "Open questions" section, no unmade decision, no relationship written as text, and no list of files. Then show the full proposed issue or issue set with titles, bodies, and labels, and ask for confirmation before creating anything.
8. On confirmation, using the commands in `SKILL.md`: create the labels that do not yet exist, create the issues, then link each Task to its Story as a native sub-issue. Create the Story first so its number is known.
9. Report the created issue numbers and links.
