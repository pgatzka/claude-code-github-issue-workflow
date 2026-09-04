# GitHub issue workflow for Claude Code

A reusable issue workflow you copy into a project. It gives you three GitHub issue forms, and Claude Code commands, agents, and skills that create issues which are ready to implement, work on them, and split them when they grow too wide. Its defining rule is that an issue is never created with a decision still open.

## Install

Copy these two directories into the root of the target project:

```text
.github/ISSUE_TEMPLATE/
.claude/
```

Do not copy `README.md` or `CLAUDE.md`. They describe this repository, not yours.

Prerequisites:

- The `gh` command line tool, version 2.94.0 or later, authenticated against the target repository.
- A repository with issues enabled.

Nothing else. There is no setup script and no placeholder to fill in. Anything project-specific is read from the repository or asked at the moment it is needed.

## The three issue types

| Type | Use when | Contains |
| --- | --- | --- |
| Story | Creating a new feature or updating an existing one | A user story sentence and acceptance criteria describing observable behavior |
| Task | One unit of implementation work in one area | A technical description with the decisions already made, and a definition of done |
| Bug | Behavior is unexpected and should be fixed | What is wrong, steps to reproduce, expected and actual behavior, environment |

Full rules and worked examples: [story.md](.claude/skills/issue-conventions/story.md), [task.md](.claude/skills/issue-conventions/task.md), [bug.md](.claude/skills/issue-conventions/bug.md).

## The three commands

| Command | What it does | Example |
| --- | --- | --- |
| `/create-issue` | Resolves every open decision with you, drafts the issue, shows it, then creates it with labels and native relationships | `/create-issue add rate limiting to the public search endpoint` |
| `/work-on-issue` | Implements a Task or Bug, writes tests for our own code, runs it, and has a verifier check the definition of done | `/work-on-issue 42` |
| `/split-task` | Splits a Task that spans more than one area into one Task per area under the same Story | `/split-task 42` |

## Rules you will notice in practice

- No open questions. If a decision is unresolved, you are asked before anything is drafted. An unknown cause is not a decision and never blocks a Bug.
- Relationships are native. Story to Task is a real sub-issue link, blocking is a real blocked-by link, and no body ever says "Parent: #12".
- No file lists. An issue says what must be true afterwards, never which files to touch.
- Types are labels. An issue is a Story, Task, or Bug because it carries `type:story`, `type:task`, or `type:bug`, never because of its title.
- Titles are lowercase, written like commit subjects.
- One area per Task. Wider work is split, and a Task that cannot be split says why.
- Stories are never worked on directly. The work happens in their Tasks.
- Tests cover our own code, never framework or library behavior.
- Commits are small, one per logical change, with lowercase subjects, and only when you ask.

The rules in full: [SKILL.md](.claude/skills/issue-conventions/SKILL.md) and [implementation-standards](.claude/skills/implementation-standards/SKILL.md).

## Labels

The set is closed. Labels are created on demand with a fixed color and description, never all at once.

```text
type:story    type:task        type:bug
priority:low  priority:medium  priority:high  priority:urgent
size:small    size:medium      size:large
area:<name>
needs-triage  needs-information  blocked
regression    security  technical-debt  breaking-change
```

Area labels are the only per-project part. Edit the allowed list in [labels.md](.claude/skills/issue-conventions/labels.md).

## What to adjust after copying

1. Replace the area label list in `.claude/skills/issue-conventions/labels.md` with the real parts of your codebase, fewer than ten.
2. Optionally create the four labels the forms apply, the three type labels and `needs-triage`, so issues filed through the browser carry them from the first one. GitHub skips a form label that does not exist yet; the commands create labels on demand either way.
3. Nothing else. The forms, commands, agents, and skills contain no project assumptions.
