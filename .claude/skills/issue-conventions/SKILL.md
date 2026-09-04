---
name: issue-conventions
description: Use when creating, writing, grooming, splitting, or labeling GitHub issues in this repository. Defines the three issue types (Story, Task, Bug), the readiness rule, the closed label set, and the exact gh commands for creating, labeling, and linking issues.
---

# Issue conventions

## The readiness rule

An issue is ready for implementation, never for further planning. Every decision the implementer would otherwise have to make on their own behalf is already made and written down in the issue before it is created.

An issue therefore never contains an "Open questions" section, and never contains a question, a "to be decided", a "we should figure out", or an either-or choice left to the reader. If a decision is unresolved, the issue is not created yet. Resolve the decision in conversation with the requester first, and write only the outcome into the issue.

The distinction that matters:

- An unresolved **decision** blocks issue creation. Something a person must choose, where the choice is theirs to make: which library, which database, which behavior is correct, what the target is. Resolve it before writing.
- An unknown **cause** does not block issue creation. Something that will be discovered by investigating the code. A Bug does not need to be diagnosed before it is filed, and a Task does not need its solution designed in advance. Not knowing why something breaks is normal and belongs in the issue as observed facts. Not knowing what the fix should achieve is a decision, and does not.

Worked example: a request of "set up database connection" is not ready. Which database, which driver or client library, where the connection details come from, and what pooling behavior is expected are all decisions. Ask, get answers, then write an issue that states the chosen database and the chosen approach. Do not write an issue that asks which database to use.

So: "the request fails intermittently and we do not know why" is a ready Bug. "The request fails and we should decide whether to retry or surface the error" is not ready until someone decides.

## Reference files

Read the matching file in full before writing any issue of that type. Each holds the rules for the type, the body skeleton with the exact headings, the readiness checklist, and worked examples.

- Story, a new or changed feature described as user-facing behavior: `story.md`
- Task, one unit of implementation work in one area: `task.md`
- Bug, unexpected behavior that should be fixed: `bug.md`
- Titles, for every type: `titles.md`

## The other universal rules

1. Relationships are real GitHub relationships, never prose. Never write "Parent: #12", "Blocked by #40", "Related to #7", or any similar line in an issue body. Story to Task is a native parent and sub-issue relationship. Blocking is a native blocked-by relationship. The commands below set both.
2. No issue contains a list of files to change, lines to touch, functions to edit, or a prescribed code structure. What to change is the implementer's decision, not the planner's. If you find yourself writing a path into an issue body, stop.
3. The type of an issue is identified only by its label: `type:story`, `type:task`, or `type:bug`. Every issue carries exactly one. Titles never carry a prefix or any other type marker.
4. Titles are written like commit subjects: lowercase, one line, no prefix. The full rules and examples are in `titles.md`. Read it before writing any title.

## Labels

The label set is closed and documented in `labels.md`, together with the allowed area labels for this repository. Labels are created on demand: check whether a label exists before applying it, create it if it does not, and never create the whole set up front.

## Commands

Verified against gh version 2.94.0. Every issue is created with its type label and `needs-triage`, which is what the issue forms apply, so issues created here and issues filed through the browser look the same. Labels passed to `gh issue create` must already exist.

Check whether a label exists. Prints the name if it does, nothing otherwise:

```shell
gh label list --limit 200 --json name --jq '.[] | select(.name == "priority:high") | .name'
```

Create a label, with the color and description from `labels.md`:

```shell
gh label create "priority:high" --color ef6b5f --description "Should be worked on before other open issues"
```

Create an issue from a body file that follows the type's skeleton:

```shell
gh issue create --title "add connection pooling to the order service" --body-file body.md --label "type:task" --label "needs-triage" --label "area:backend"
```

Create a Task directly as a native sub-issue of its Story:

```shell
gh issue create --title "add connection pooling to the order service" --body-file body.md --label "type:task" --label "needs-triage" --parent 12
```

Link an existing Task to its Story as a native sub-issue. Either direction works:

```shell
gh issue edit 40 --parent 12
gh issue edit 12 --add-sub-issue 40,41
```

Apply labels to an existing issue:

```shell
gh issue edit 40 --add-label "priority:high" --add-label "size:small"
```

Record a native blocking relationship:

```shell
gh issue edit 40 --add-blocked-by 38
```

Read an issue including its relationships:

```shell
gh issue view 40 --json number,title,body,labels,parent,subIssues,blockedBy,blocking
```

Replace an issue body, for example after a decision has been recorded:

```shell
gh issue edit 40 --body-file body.md
```
