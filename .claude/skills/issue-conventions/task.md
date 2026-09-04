# Task

## When to use this type

Use a Task for a unit of implementation work: building or changing something in the code, the configuration, the build, or the infrastructure. A Task usually belongs to a Story as a native sub-issue. A Task may be standalone when the work has no user-facing feature attached, such as refactoring, dependency upgrades, or continuous integration fixes.

## The single-area rule

A Task touches exactly one area, in the sense of the area labels in `labels.md`. If a Task would touch more than one area, split it into one Task per area. If splitting is genuinely not possible, a multiple-area Task is acceptable, but splitting is the strong default and the Task must state in its description why it could not be split.

To split by area: list every area the work touches, write one Task per area with its own definition of done, and link each to the same parent Story. Where one Task depends on another, record it as a native blocked-by relationship, never as text. Work that only makes sense as a single change across areas, such as renaming a shared contract that both sides must adopt at once, is the usual case where splitting fails.

## What belongs and what does not

Belongs:

- A technical description: what needs to be built or changed, including the decisions already made, such as the chosen library, the chosen approach, or the target behavior.
- A definition of done written as verifiable technical outcomes. Each item can be checked by running, reading, or measuring something.
- Optionally, constraints the implementation must respect, such as backward compatibility or a performance target.

Does not belong:

- User-facing acceptance criteria. Those live on the parent Story and are never duplicated, because duplicated criteria drift apart.
- A list of files to change, functions to edit, or a prescribed code structure. What to change is the implementer's decision.
- Any question, open decision, or relationship written as text. See `SKILL.md`.

## Body skeleton

The headings below match the field labels of the Task issue form in `.github/ISSUE_TEMPLATE/task.yml` exactly, so an issue created by a command and an issue filed through the browser are indistinguishable. Keep them identical when editing either. Write `_No response_` under an optional heading you have nothing to put under, which is what the form writes.

```markdown
### Description

### Definition of done

- [ ]
- [ ]
- [ ]

### Constraints

_No response_
```

## Readiness

Apply the readiness rule in `SKILL.md`. Before a Task can be written, these must be decided:

- The approach, wherever more than one is reasonable: which library, which service, which storage, which protocol, which behavior on failure.
- The target: what the outcome must be, concretely enough to write each definition of done item as a checkable statement.
- Which single area it belongs to.

How the code will be structured is not decided here. Neither is the cause of any problem the Task addresses. Both are found during implementation.

## Worked examples

Good:

> **add connection pooling to the order service database client**
>
> The order service opens a new PostgreSQL connection per request. Switch it to the pool provided by the PostgreSQL client library already in use, with a minimum of two and a maximum of ten connections, and read those limits from the service configuration with those values as defaults.
>
> - [ ] Under a sustained load of one hundred requests per second, the number of open database connections stays at or below ten.
> - [ ] The pool limits can be changed through the service configuration without a code change.
> - [ ] Existing order service tests pass unchanged.

Every decision is made, every item is verifiable, and nothing names a file.

Not ready:

> **set up database connection**
>
> Connect the service to a database. We should figure out whether to use PostgreSQL or MySQL and pick a client library.

Which database, which client library, where the connection details come from, and what pooling behavior is expected are all decisions, so this issue cannot be created. Corrected: ask those questions, get answers, then write a Task like the good one above.
