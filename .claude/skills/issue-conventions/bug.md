# Bug

## When to use this type

Use a Bug when behavior is unexpected and should be fixed. Anyone who can reproduce the problem can file one. Diagnosis is not required.

## What belongs and what does not

Belongs:

- What is wrong, steps to reproduce, expected behavior, actual behavior, and environment.
- Logs or a stack trace, pasted unedited, when there are any.
- A suspected cause, clearly a non-binding hypothesis, when there is one.

Does not belong:

- A diagnosis or a prescribed fix. Where the problem lives and how to fix it are found during implementation.
- A list of files or functions to look at.
- Any question, open decision, or relationship written as text. See `SKILL.md`.

## Reproduction steps

Good steps start from a known state and end at the first wrong observation. Each step is one action a reader can perform without guessing: which page or command, which input, which account or role. Include the data that matters, such as the exact value that triggers the problem, and leave out anything that does not change the outcome.

For an intermittent problem, say so, and give what is known: how often it happens out of how many attempts, under what conditions it seems more likely, and what was tried that did not affect it. "Fails roughly one time in twenty, more often under load, not reproduced with a single user" is a ready Bug. Not knowing why is the normal state of a Bug at filing time.

## Cause versus expected behavior

An unknown cause never blocks filing. An unstated expected behavior always does: it is a decision about what correct looks like, and the implementer cannot make it on the filer's behalf. "The export fails and we should decide whether to retry or show an error" is not ready. "The export fails; it should retry twice and then show an error naming the failed step" is ready. See the readiness rule in `SKILL.md`.

## Body skeleton

The headings below match the field labels of the Bug issue form in `.github/ISSUE_TEMPLATE/bug.yml` exactly, so an issue created by a command and an issue filed through the browser are indistinguishable. Keep them identical when editing either. Write `_No response_` under an optional heading you have nothing to put under, which is what the form writes. When there are logs, put them under their heading in a fenced block marked `shell`, which is what the form produces.

```markdown
### What is wrong

### Steps to reproduce

1.
2.
3.

### Expected behavior

### Actual behavior

### Environment

### Logs or stack trace

_No response_

### Suspected cause

_No response_
```

## Readiness

Before a Bug can be written, these must be decided:

- The expected behavior, stated concretely.
- The environment in which it was observed.

Nothing else needs deciding. The cause, the location, and the fix are discovered during implementation.

## Worked examples

Good:

> **invoice total shows the wrong currency after switching accounts**
>
> What is wrong: after switching from a euro account to a dollar account, the invoice page keeps showing amounts with the euro symbol.
>
> Steps to reproduce: 1. Sign in as a user with access to both accounts. 2. Open the invoice page on the euro account. 3. Switch to the dollar account using the account menu. 4. Open any invoice.
>
> Expected behavior: amounts show the dollar symbol and the dollar total. Actual behavior: the euro symbol is shown next to the dollar figure. Environment: 2.3.0, main at 3f9c2a1, staging.

The steps can be followed by anyone, the expected behavior is concrete, and no cause is claimed.

Should have been a different type:

> **invoices should support pounds**
>
> Actual behavior: only euro and dollar are available. Expected behavior: pounds are available too.

Nothing is broken; the software does what it was built to do. Corrected: a Story with acceptance criteria for selecting and displaying the new currency, and one Task per area for the work.
