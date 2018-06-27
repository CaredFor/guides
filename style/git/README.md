Git Style
=========

## Branch Naming
When naming your branches, follow this format:

```
git checkout -b <prefix>/<summary>/<ticket number>
```

### Prefixes

It's common to see a development team require the author's initials in a branch name. However, Git already tells us who the author is, and this falls apart when another developer picks up on a branch. Instead, use these prefixes:

* Releases: `release`
* Features: `feature`
* Bug Fixes: `hotfix`

### Ticket Numbers

Generally speaking, a branch should correspond to a single ticket. Append the ticket number so that other team members can easily know where to find more information just by looking at the branch name.

### Summaries

Provide no more than five words on what this branch is for. For example, `feature/video-uploads` or `hotfix/hanging-spinner`.

### Exception: Release Branches

Release branches should be the version number (major/minor only). Do not include the patch number. `v1.0`.

### Examples

```
git checkout -b feature/tkt-100/video-uploads
git checkout -b hotfix/tkt-101/filesize-error
git checkout -b release/v1.1
```
