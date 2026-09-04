---
description: Implement a Task or Bug from its GitHub issue on a linked branch and deliver a review-ready pull request. Never implements a Story directly.
argument-hint: <issue number>
---

Work on GitHub issue $ARGUMENTS. The outcome is a pull request that is ready to merge after review, as defined in the implementation standards.

1. Fetch the issue and read the standards:

   ```shell
   gh issue view $ARGUMENTS --json number,title,body,labels,parent,subIssues,blockedBy
   ```

   Then read `.claude/skills/implementation-standards/SKILL.md` and `.claude/skills/commit-conventions/SKILL.md` in full.
2. Read the type from the labels: `type:story`, `type:task`, or `type:bug`. If the issue has no type label, add the right one after confirming it with the user. If the issue is a Story, do not implement it. List its sub-issues from the `subIssues` field and ask which one to work on. If it has none, offer to create the missing Tasks with `/create-issue`.
3. If the issue is a Task that clearly spans more than one area, say so and offer to split it with `/split-task` before starting.
4. If the issue leaves a decision unmade, such as a question, an either-or choice, or an unstated expected behavior, stop and ask rather than choosing silently. Once answered, update the issue body with the answer using `gh issue edit $ARGUMENTS --body-file`, so the decision is recorded where the work is.
5. If required information is missing, or the problem in a Bug cannot be reproduced, apply the label with `gh issue edit $ARGUMENTS --add-label needs-information`, explain what is missing with `gh issue comment $ARGUMENTS --body`, and stop. Create the label first if it does not exist, using the commands in `.claude/skills/issue-conventions/SKILL.md`.
6. Create a branch linked to the issue, from the default branch. The branch name is the issue number followed by the issue title, lowercase, with every space replaced by a hyphen and no slash or type marker anywhere, such as `42-add-connection-pooling-to-the-order-service`:

   ```shell
   gh issue develop $ARGUMENTS --checkout --name 42-add-connection-pooling-to-the-order-service
   ```

7. Implement the change. Then write tests for our own behavior only, as the standards describe. Then verify the code works by actually running or exercising it, and note how.
8. Delegate to the `implementation-verifier` agent with the issue number and a summary of the change. Fix what it reports as failing and delegate again, until nothing fails. Keep what it reports as unverifiable for the pull request description.
9. Commit following the commit conventions: several small commits, one per logical change. Push the branch with `git push --set-upstream origin <branch>`.
10. Open the pull request against the default branch, with the issue title as its title and a description written as the commit conventions require, ending with the line `closes #$ARGUMENTS`:

    ```shell
    gh pr create --title "<issue title>" --body-file description.md --base <default branch>
    ```

    If the repository runs continuous integration, wait for it with `gh pr checks --watch` and fix failures before reporting.
11. Report the pull request link, how the work was verified, the verifier's findings including anything unverifiable, and the state of each definition of done item.
