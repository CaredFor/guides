Git Protocol
============

CaredFor uses a slightly modified approach to the [Giflow workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow).

## Repo maintenance
* Avoid including files that are specific to your machine or process.
* Do NOT include generated or compressed files.
* Do NOT include third-party libraries (ex: `vendor` or `node_modules`)

## Workflow
### Develop and Master Branches
In alignment with the Giflow workflow, our workflow is based off of two main branches: `master` and `develop`. The `develop` branch will contain the full history of the project, while the `master` branch stores the official release history.

### Feature Branches
Each new feature should reside in its own branch. If development on feature branches takes longer than one day, the branch should be pushed to the central repository for backup at the end of each day, and should be rebased from `develop` at the start of each day. 

When a feature is complete, features should be rebased from `develop` and then merged back in to `develop`. Features should never interact directly with `master`.

#### Creating a feature branch
_See the [git style guide](/style/git) for tips on how to name your branches!_

```
git checkout develop
git pull
git checkout -b <branch name>
```

Rebase frequently to pull in upstream changes.

```
git fetch origin
git rebase origin/develop
```

#### Finishing a feature branch
Before a feature is complete, you must have:
* written thorough unit tests for your feature
* tested locally to ensure your feature works
* run all unit tests with passing results

Once you have done these things and your feature is complete, prepare your branch and submit a pull request:

* Make sure commits are written with a [good commit message](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html). Example message:

```
Present-tense summary

* More information about commit
* Another helpful comment about the commit

http://project-management-system.com/ticket/123
```

* If you've created more than one commit, use git rebase interactively to squash them into cohesive commits with good messages:

```
git rebase -i origin/develop
```

* Record your changes in the `changelog` under the _Unrleased_ heading.
* Share your branch.

```
git push origin <branch name>
```

* Submit a Pull Request in GitHub to merge your branch into `develop`. 
* Ask your peers for a code review. Once merged in, delete the local and remote branches.

### Release Branches
Once `develop` has acquired enough features for a release (or a predetermined release date is approaching), create a release branch based off of `develop`. Creating this branch starts the next release cycle, so no new features can be added after this point—only bug fixes, documentation generation, and other release-oriented tasks should go in this branch.

#### Creating release branches
_See the [git style guide](/style/git) for tips on how to name your branches!_

```
git checkout develop
git pull
git checkout -b <branch_name>
```

#### Finishing feature branches
The QA team should review the release branch in the release environment. Any bug fixes and other release-oriented tasks can be done on this branch, but no new features may be added. Once the QA team has signed off and all unit tests are passing, the release branch is ready to ship.

* Update the version numbers.
* Update the `changelog`. Add the new version number, and move any of the applicable _Unreleased_ changes to the new version. Record any additional changes that have not been recorded. Commit the `changelog`.
* Merge the release branch into both `master` and `develop`.

```
git checkout master
git pull
git merge <release_branch_name>
git checkout develop
git pull
git merge <release_branch_name>
```

* Deploy to `master` and tag it with a version number using [Semantic Versioning](https://semver.org/).
* Delete the previous release branch both locally and remotely.

### Hotfix Branches
Hotfix branches are used to quickly patch production releases. Having a dedicated line of development for bug fixes lets your team address issues without interrupting the rest of the workflow or waiting for the next release cycle. You can think of maintenance branches as ad hoc release branches.

#### Creating hotfix branches
_See the [git style guide](/style/git) for tips on how to name your branches!_

Hotfix branches should be created off of the current currently deployed release branch.

```
git checkout <currently_deployed_release_branch>
git pull
git checkout -b <hotfix_branch_name>
```

Be sure to update the `changelog` with the new version number and the bugs that were fixed.

#### Finishing a hotfix branch
Once your hotfix branch has been tested locally, merge it into the currently deployed release branch. Once the QA team has tested and all unit tests pass, your hotfix is ready to push.

* Update the version number using [Semantic Versioning](https://semver.org/).
* Merge the release branch into `master` and deploy
```
git checkout master
git pull
git merge <release_branch>
```
* Merge the hotfix branch into `develop`
```
git checkout develop
git pull
git merge <hotfix_branch_name>
```
* Delete the hotfix branch
