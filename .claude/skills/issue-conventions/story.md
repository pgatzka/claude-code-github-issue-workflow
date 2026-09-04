# Story

## When to use this type

Use a Story when creating a new feature or updating an existing feature. A Story describes what a user can do afterwards, not how it is built.

A Story is never worked on directly. All of its work happens in Task issues linked to it as native sub-issues. A Story is closed when its Tasks are closed and its acceptance criteria hold.

## What belongs and what does not

Belongs:

- The user story sentence: the role, the capability, and the outcome.
- Acceptance criteria describing observable, user-facing behavior. Each criterion is something a person can check by using the software.
- Optionally, what is out of scope.

Does not belong:

- Implementation detail, technical approach, library choices, or file names. Those live on the Tasks.
- A definition of done. That lives on each Task. Acceptance criteria stay on the Story only, so they are written once and cannot drift apart between copies.
- Any question, open decision, or relationship written as text. See the readiness rule and the universal rules in `SKILL.md`.

## Body skeleton

The headings below match the field labels of the Story issue form in `.github/ISSUE_TEMPLATE/story.yml` exactly, so an issue created by a command and an issue filed through the browser are indistinguishable. Keep them identical when editing either. Write `_No response_` under an optional heading you have nothing to put under, which is what the form writes.

```markdown
### User story

As a <role>, I want <capability>, so that <outcome>.

### Acceptance criteria

- [ ]
- [ ]
- [ ]

### Out of scope

_No response_
```

## Readiness

Apply the readiness rule in `SKILL.md`. Before a Story can be written, these must be decided:

- Who the user is, as a role, and what they will be able to do.
- What done looks like from the outside, concretely enough to write each acceptance criterion as a checkable statement.
- Where the feature stops, if there is any risk of it growing.

The technical approach is not decided here. It is decided when each Task is written.

## Worked examples

Good:

> **export the monthly usage report as a spreadsheet**
>
> As an account manager, I want to download the monthly usage report as a spreadsheet, so that I can share it with clients who do not have access to the dashboard.
>
> - [ ] The report page shows a download action for the currently selected month.
> - [ ] The downloaded file opens in common spreadsheet software and contains the same rows the page shows.
> - [ ] A month with no usage produces a file with the header row only.

Every criterion is observable by a user, and nothing says how the export is built.

Written wrongly:

> **Add spreadsheet export using the sheet-writer package**
>
> As a user, I want spreadsheet export.
>
> - [ ] Add an export route to the reports controller.
> - [ ] Tests pass.

The title is not lowercase, the user story names no outcome, the title and the first criterion prescribe a library and a route, and "tests pass" is a definition of done item rather than user-facing behavior. Corrected: the good Story above, with the library choice recorded as a decision in the Task that implements the export.
