---
name: implementation-standards
description: Use when implementing a Task or Bug, or finishing work on an issue. Defines what complete means; working code you have run, tests for our own behavior only, an honest definition of done, and stopping to ask when the issue left a decision unmade.
---

# Implementation standards

Work on an issue is complete only when every section below holds.

## The code works, demonstrably

Write the code, then run it or exercise it the way it will actually be used: start the service and send the request, run the command, open the page, execute the migration against a scratch database. State how you verified it: the command you ran, the input you gave, the output you saw. "It should work" is not verification.

## Tests cover the behavior you wrote

Write tests for the behavior you added or changed, at the level where that behavior is visible: the function, the endpoint, the command, or the generated output. Each test should fail if your change were reverted.

## Tests do not cover framework, library, or third-party behavior

Do not write tests that assert a dependency behaves as documented. Such a test proves nothing about your work and breaks when the dependency changes for reasons unrelated to your code.

Worked example: if you set up a Prometheus container, you do not test that Prometheus scrapes targets or stores time series. You test the code you wrote around it: that your configuration generation produces the scrape targets you expect, and that your metrics endpoint exposes the counters you added with the values you set.

## When there is nothing of your own to test

If a change genuinely has nothing of your own to test, such as bumping a dependency version or changing a deployment value, say so explicitly and explain why, rather than writing a test that asserts a dependency behaves as documented.

## The definition of done is honest

Check off an item only when it is actually true and you have seen it be true. An item you could not verify stays unchecked, and you say why. For a Bug, the expected behavior in the issue is the definition of done.

## Commits, when you are asked to commit

Commit only when asked. When you are, follow `.claude/skills/commit-conventions/SKILL.md`: several small commits, one per logical change, with lowercase subjects.

## Review ready

The outcome of implementing an issue is a pull request that is ready to merge after review. That means: every section above holds, the verifier reports no failure, the commits follow `.claude/skills/commit-conventions/SKILL.md`, the branch is up to date with the default branch and merges cleanly, continuous integration passes if the repository has it, and the pull request is not a draft. Anything unverifiable is stated in the pull request description. Nothing is left for the reviewer to finish.

## When the issue left a decision unmade

If implementation reveals a decision the issue failed to make, stop and ask rather than choosing silently. The issue was not ready. Once the answer is given, update the issue body with it so the decision is recorded where the work is, then continue. The readiness rule is in `.claude/skills/issue-conventions/SKILL.md`.
