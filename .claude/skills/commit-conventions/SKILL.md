---
name: commit-conventions
description: Use when committing, writing a commit message, deciding how to split a change into commits, or writing a pull request description. Defines when to commit, how small a commit is, the exact subject and body format, and what a pull request description may contain.
---

# Commit conventions

## When to commit

Commit only when asked. Working on an issue through `/work-on-issue` is asking: its outcome is a review-ready pull request, so it commits, pushes its branch, and opens the pull request. Outside that, never commit, push, or open a pull request as a side effect of finishing work.

## One commit per logical change

A change set is several small commits, never one large commit for a whole issue or pull request. Split by concern: the production code, its tests, a refactoring that made room for it, a documentation update, a dependency change. Each commit leaves the repository in a state that builds and passes its tests on its own, so any commit can be reviewed, reverted, or bisected alone.

Order commits so each builds on the previous one: preparatory refactoring first, then the behavior, then tests if they are not in the same commit, then documentation.

## Subject line

- Lowercase throughout, including the first word and any proper noun that has a lowercase form.
- Imperative mood: `add`, `remove`, `rename`, `fix`, not `added` or `adds`.
- One line of at most seventy-two characters, no trailing period.
- Says what the commit does, specifically: `add connection pooling to the order service`, not `update code` or `fixes`.
- No prefix, tag, scope, or issue number in the subject. No abbreviations.

Issue titles use the same subject style; the issue side is in `.claude/skills/issue-conventions/titles.md`.

## Body

A commit message is short but explanatory. Add a body when the subject cannot carry the reason, and keep it to a few sentences: why the change is made and what it replaces, not what the diff already shows and not a narrative of the work. Separate it from the subject with one blank line and wrap it at seventy-two characters. Reference the issue by number in the body, such as `part of #42`, never in the subject.

## Pull request description

The pull request title is the issue title. The commits are the record of what was done. A pull request description does not repeat them, and it is never a long account of the work. Write one only when the commit messages leave something unsaid that a reviewer needs: the reason for the change as a whole, a decision that spans several commits, a manual step to take after merging, or what to look at first. When the commit messages already say everything, leave the description at a single line naming the issue, such as `closes #42`.

## Example

```text
add connection pooling to the order service

Each request opened its own database connection, which exhausted the
database's connection limit under load. Use the pool from the client
library already in use, with limits read from the service
configuration.

part of #42
```
