Git Protocol
============

A guide for using Git version control.

## Repo maintenance
* Avoid including files that are specific to your machine or process.
* Do NOT include generated or compressed files.
* Do NOT include third-party libraries (ex: `vendor` or `node_modules`)

## Workflow
### Write a feature
Create a local feature branch based off of master (or the latest release branch).
_See the [git style guide](/style/git) for tips on how to name your branches!_

```
git checkout master
git pull
git checkout -b <branch name>
```

Rebase frequently to pull in upstream changes.

```
git fetch origin
git rebase origin/master
```

When your feature is complete and tests pass, commit them with a [good commit message](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html). Example message:

```
Present-tense summary

* More information about commit
* Another helpful comment about the commit

http://project-management-system.com/ticket/123
```

If you've created more than one commit, use git rebase interactively to squash them into cohesive commits with good messages:

```
git rebase -i origin/master
```

Share your branch.

```
git push origin <branch name>
```

Merge your feature branch into `testing` and resolve any conflicts.

```
git checkout testing
git pull
git merge <branch name>
```

Once tested by the QA team and approved, submit a GitHub pull request to merge with the latest release branch.

Ask your peers for a code review.