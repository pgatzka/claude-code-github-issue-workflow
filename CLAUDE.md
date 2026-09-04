# Maintaining this setup

This repository is a reusable GitHub issue workflow that gets copied into other projects. It is not itself an application. This file guides edits to the setup; it says nothing about any project the setup is copied into.

## Copied versus not copied

- Copied into consuming projects: `.github/ISSUE_TEMPLATE/` and `.claude/`.
- Not copied: `README.md` and this `CLAUDE.md`.

Nothing inside `.claude` or `.github` may reference `README.md` or `CLAUDE.md`, because those references break the moment the setup is copied. Nothing inside them may assume anything about the consuming project: no language, no framework, no directory layout, no test runner, no package manager. Anything project-specific is discovered at runtime by reading the repository or asked at the moment it is needed. There are no placeholders to fill in later.

## Duplication that exists on purpose

Each issue form in `.github/ISSUE_TEMPLATE/` has a matching body skeleton in `.claude/skills/issue-conventions/`:

- `story.yml` and `story.md`
- `task.yml` and `task.md`
- `bug.yml` and `bug.md`

The form field labels and the skeleton headings must stay identical, in wording, order, and which fields are required. Changing one means changing the other in the same edit. Any review of a change to either file checks the other.

## Where each rule is written down

An edit to a rule updates every place it appears.

- Readiness rule, in full: `issue-conventions/SKILL.md`. Referenced with a short readiness section in `story.md`, `task.md`, `bug.md`; in `agents/issue-author.md`, `agents/issue-splitter.md`; in `commands/create-issue.md`, `commands/split-task.md`, `commands/work-on-issue.md`; and as the stop-and-ask section of `implementation-standards/SKILL.md`.
- Relationship rule: `issue-conventions/SKILL.md`, `task.md`, `agents/issue-author.md`, `agents/issue-splitter.md`, `commands/split-task.md`, `labels.md` under blocked.
- No-file-lists rule: `issue-conventions/SKILL.md`, `story.md`, `task.md`, `bug.md`, `agents/issue-author.md`, and the constraints field description in `task.yml`.
- Single-area rule: `task.md` in full; referenced in `agents/issue-splitter.md`, `commands/split-task.md`, `commands/work-on-issue.md`, `commands/create-issue.md`.
- Testing rule: `implementation-standards/SKILL.md` in full; referenced in `agents/implementation-verifier.md` and `commands/work-on-issue.md`.
- Type label rule, types are identified only by `type:story`, `type:task`, or `type:bug`: `issue-conventions/SKILL.md`, `labels.md`, the `labels` list of each form, `agents/issue-author.md`, `commands/work-on-issue.md`, `commands/split-task.md`.
- Title rule: `issue-conventions/titles.md` in full, pointed at from `issue-conventions/SKILL.md`; checked in `agents/issue-author.md`, `commands/create-issue.md`, `commands/split-task.md`; shown in every worked example.
- Commit rule: `commit-conventions/SKILL.md` in full, which also defines the subject style that `titles.md` shares; pointed at from `implementation-standards/SKILL.md` and `commands/work-on-issue.md`.
- Label taxonomy: `labels.md` only. Other files point at it and never list labels themselves, except the type labels, the always-applied `needs-triage`, and the `needs-information` step in `commands/work-on-issue.md`.

## Invariants that must survive any edit

- No open questions anywhere: no form field, skeleton section, or command step that lets an issue be created with a decision unmade.
- No relationships as text. No form field, skeleton, or agent output for a parent, a blocker, or a related issue.
- No file lists in issue bodies.
- Issue type is carried by the type label only. No form sets a title, and no file identifies a type by a title prefix.
- Titles and commit subjects are lowercase and prefix-free, and the subject style is defined once, in `commit-conventions/SKILL.md`.
- The label set stays closed, and area labels are the only per-project part.
- Labels are created on demand, never preemptively.
- No abbreviations in any file, including labels, headings, and command names.
- Reference files stay near or under one hundred lines.

## How to verify a change

1. The three issue forms parse as valid YAML and follow GitHub's issue form schema: every body element has a type, a label, and a unique identifier; required fields declare `required: true`; no form has a `title` key; each form's `labels` list holds its type label and `needs-triage`.
2. Each skeleton heading in `story.md`, `task.md`, and `bug.md` matches the corresponding form's field labels exactly, in the same order.
3. Every `gh` command recorded in `issue-conventions/SKILL.md` exists in the installed version. Check with `gh issue create --help`, `gh issue edit --help`, `gh issue view --help`, and `gh label list --help`. The sub-issue flags `--parent`, `--add-sub-issue`, and the `parent` and `subIssues` output fields were verified against gh 2.94.0.
4. Nothing inside `.claude` or `.github` mentions `README.md` or `CLAUDE.md`.
5. No abbreviations were introduced.

## What deliberately does not exist

- No setup script. The setup works by being copied; a script would be one more thing to keep working across projects.
- No status labels beyond `blocked` and `needs-information`. Open, closed, and the native relationships already carry the state; more labels would drift from reality.
- No issue type beyond Story, Task, and Bug. Anything else has fit one of them so far, and a fourth type would need its own form, skeleton, and rules to keep in step.
- No open questions field. Its existence would invite creating issues that are not ready.
