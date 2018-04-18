Git Style
=========

## Branch Naming
When naming your branches, follow this format:

```
git checkout -b <prefix>/<summary>/<ticket number>
```

### Prefixes

It's common to see a development team require the author's initials in a branch name. However, Git already tells us who the author is, and this falls apart when another developer picks up on a branch. Instead, use these prefixes:

* Environments: `env`
* Features: `feat`
* Bug Fixes: `fix`
* General "task" tickets: `tkt`

### Summaries

Provide no more than five words on what this branch is for. For example, `feat/video-uploads` or `fix/hanging-spinner`.

### Ticket Numbers

Generally speaking, a branch should correspond to a single ticket. Append the ticket number so that other team members can easily know where to find more information just by looking at the branch name.

### Exception: Release Branches

Release branches should be the version number (Semver), prefixed with the letter `v`. For example, `v1.0.0`.

### Examples

```
git checkout env/testing
git checkout -b feat/video-uploads/PROJ-100
git checkout -b fix/filesize-error/PROJ-101
git checkout -b tkt/change-camera-icon/PROJ-102
git checkout -b v1.1.0
```
