---
description: Implement a Task or Bug from its GitHub issue, verify the work, and report honestly. Never implements a Story directly.
argument-hint: <issue number>
---

Work on GitHub issue $ARGUMENTS.

1. Fetch the issue and read the standards:

   ```shell
   gh issue view $ARGUMENTS --json number,title,body,labels,parent,subIssues,blockedBy
   ```

   Then read `.claude/skills/implementation-standards/SKILL.md` in full.
2. Read the type from the labels: `type:story`, `type:task`, or `type:bug`. If the issue has no type label, add the right one after confirming it with the user. If the issue is a Story, do not implement it. List its sub-issues from the `subIssues` field and ask which one to work on. If it has none, offer to create the missing Tasks with `/create-issue`.
3. If the issue is a Task that clearly spans more than one area, say so and offer to split it with `/split-task` before starting.
4. If the issue leaves a decision unmade, such as a question, an either-or choice, or an unstated expected behavior, stop and ask rather than choosing silently. Once answered, update the issue body with the answer using `gh issue edit $ARGUMENTS --body-file`, so the decision is recorded where the work is.
5. If required information is missing, or the problem in a Bug cannot be reproduced, apply the label with `gh issue edit $ARGUMENTS --add-label needs-information`, explain what is missing with `gh issue comment $ARGUMENTS --body`, and stop. Create the label first if it does not exist, using the commands in `.claude/skills/issue-conventions/SKILL.md`.
6. Implement the change. Then write tests for our own behavior only, as the standards describe. Then verify the code works by actually running or exercising it, and note how.
7. Delegate to the `implementation-verifier` agent with the issue number and a summary of the change. Report its findings honestly, including anything that did not pass or could not be verified.
8. Summarize what changed, how it was verified, and the state of each definition of done item. Do not commit, push, or open a pull request unless asked.
