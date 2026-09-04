---
description: Split a Task that spans more than one area into one Task per area, linked to the same parent Story with native relationships and carrying the original's decisions.
argument-hint: <issue number>
---

Split GitHub issue $ARGUMENTS by area.

1. Read `.claude/skills/issue-conventions/SKILL.md`, then `task.md`, `titles.md`, and `labels.md` in the same directory.
2. Fetch the issue:

   ```shell
   gh issue view $ARGUMENTS --json number,title,body,labels,parent,blockedBy,blocking
   ```

   Note its parent, its labels, its relationships, and every decision its body already records. If it does not carry `type:task`, say so and stop.
3. Delegate to the `issue-splitter` agent with the issue body and its recorded decisions. It returns a plan of Tasks by area, the parts that cannot be split with reasons, and any unresolved decisions.
4. If the plan lists unresolved decisions, present them together, each with a recommended option and a one-line reason, and wait for answers. Nothing is drafted until they are resolved.
5. Delegate drafting of each new Task to the `issue-author` agent, passing the decisions already made in the original together with the newly resolved ones, so that no new Task is created unready.
6. Check every drafted issue: the title follows `titles.md`, the labels include `type:task`, and the body has no questions, unmade decisions, relationships written as text, or file lists. Show the full set with labels, together with what will happen to the original, and ask for confirmation before creating anything.
7. On confirmation, using the commands in `SKILL.md`: create any missing labels; create each new Task, passing `--parent` with the original's parent Story if it has one; record dependencies between the new Tasks with `--add-blocked-by`; and carry each of the original's own blocked-by and blocking relationships to the new Task it applies to.
8. Close the original with `gh issue close $ARGUMENTS --comment`, naming the new issue numbers in the comment. If part of the original's scope stays with it, instead update its body to the reduced scope with `gh issue edit $ARGUMENTS --body-file` and leave it open. Never leave a relationship as text in any body.
9. Report the created issue numbers and links, and the state of the original.
