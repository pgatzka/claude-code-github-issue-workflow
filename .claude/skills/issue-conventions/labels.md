# Labels

The label set below is closed. No label outside it may ever be created or applied. Labels are created on demand, never all at once: before applying a label, check whether it exists in the repository and create it if it does not, using the commands in `SKILL.md`. Give every label the color and description from this file when creating it. Each prefix family has its own color range so the label list stays scannable.

## Priority, red range

| Label | Color | Description |
| --- | --- | --- |
| priority:low | fbe3e0 | Can wait; nobody is waiting on it |
| priority:medium | f7b3ab | Normal ordering |
| priority:high | ef6b5f | Should be worked on before other open issues |
| priority:urgent | b60205 | Drop other work; users are affected now |

## Size, blue range

| Label | Color | Description |
| --- | --- | --- |
| size:small | c2e0ff | A few hours of work |
| size:medium | 7fbaf5 | A day or two of work |
| size:large | 1d76db | Several days of work; consider splitting |

## Area, green

Every area label uses color `0e8a16`. The allowed list for this repository:

| Label | Description |
| --- | --- |
| area:issue-forms | The issue forms under .github/ISSUE_TEMPLATE |
| area:skills | The skills under .claude/skills |
| area:agents | The agents under .claude/agents |
| area:commands | The commands under .claude/commands |

This list is the one part of the copied setup meant to be edited per project. Replace it when installing this setup, keep it under ten entries, and map each entry to a real part of the codebase. When an issue needs an area that is not listed, do not invent one silently: propose it, get explicit confirmation, then add it here in the same change that creates the label.

## Status, yellow and gray

| Label | Color | Description |
| --- | --- | --- |
| needs-triage | fbca04 | Applied on creation; removed once priority, size, and area are set |
| needs-information | f4d35e | Information found to be missing after the issue was created |
| blocked | 6c757d | Cannot proceed until a blocking issue is resolved |

needs-information means information discovered to be missing after the issue was created, such as a Bug that turns out not to be reproducible. It is not a way to file an issue with unresolved decisions and sort it out later. Unresolved decisions are settled before creation, not labeled after it.

blocked is applied alongside a native blocked-by relationship, never instead of one.

## Nature, purple range

| Label | Color | Description |
| --- | --- | --- |
| regression | d4c5f9 | Behavior that used to work and no longer does |
| security | 5319e7 | Touches authentication, authorization, secrets, or data exposure |
| technical-debt | 9c7ede | Pays down a shortcut taken earlier |
| breaking-change | 7057ff | Changes a contract that existing users or callers depend on |
