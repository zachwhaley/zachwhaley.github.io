---
layout: post
title: CVS with Git
---

I'm working on a project in CVS (What! that's ancient; I know, right?) and to say the least, it
sucks ass.

Lemme take a few words to say CVS is really annoying.

Commits are per file, so forget about your change being traceable.  Commits are not atomic!
this means if your commit includes more than one file, someone else could be updating while
you are commiting and get only half of your changes, wtf!  Renaming and/or moving files can't
be done.  Branches are expensive and hard to do; also, merging branches is just as effective
as committing a patch with a commit message like "Good luck".  Basically your history is stuck in
the old branch, so don't delete branches (even though they are a huge pain).


Alright, now how did I "fix" this?  I put Git in my CVS checkout :) because Git solves all my
source control problems.

## How to do that

### Setup

Start by checking out your CVS repository

```bash
$ cvs co [your-repo]
```

Don't compile anything, because we'll need to figure out what files are generated and which are
actually in the repo.

Go to GitHub's [gitignore repo](https://github.com/github/gitignore) and find some gitignore
files for your project, i.e.
[C.gitignore](https://github.com/github/gitignore/blob/master/C.gitignore) for C,
[Python.gitignore](https://github.com/github/gitignore/blob/master/Python.gitignore) for Python, etc.

Create a file at the base of your CVS repo named `.gitignore` and add the contents of the
gitignores you found on GitHub.  This will be used to filter out general generated files.

Create your Git repository

```bash
$ cd /path/to/your/repo/
$ git init
```

Add all pertinent code to the git repo.  Stay clear of binaries and generated files.

```bash
$ git add [files]
$ git commit -m 'Let There Be Code'
```

Now build your code.  Once the build is complete, find out what files were generated that
aren't being caught by your `.gitignore` file

```bash
# The generated files will show up as untracked files.
$ git status
```

Add those generated files to your `.gitignore` file

### Develop

While working on a feature or a bug, you'll want to segregate the code changes with Git
branches.

Make sure to commit early and often to keep your work concise and on track.

```bash
# Create and checkout a branch from master for a new feature
$ git checkout -b new-feature master
```

While developing, no doubt others will commit changes to your CVS repo and
you'll need a way to safely get those changes without breaking your work.

Use your master branch as a staging area for CVS changes.  Don't directly commit any of your
changes to master.

```bash
# Checkout and update your master branch with the latest from CVS
$ git checkout master
$ cvs up -Pd
$ git add -A [files]
$ git commit -m 'cvs update'
```

To bring these changes into your feature/bug branch, use `git rebase`

[Rebase](https://git-scm.com/book/en/v2/Git-Branching-Rebasing) will start with the branch you
give it and then replay the commits you've been making onto that branch, then save that history
onto your current branch.

```bash
# Checkout your feature branch again and replay your changes onto master's changes that it got
# from CVS
$ git checkout new-feature
$ git rebase master
```

Your changes are now up-to-date with changes from CVS.

### Commit

Once a feature/fix is complete you'll obvisouly need to commit those changes to CVS,
use `git merge` to merge your changes with the CVS changes and then commit using CVS.

[Merge](https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging) creates a
commit to tie two branches together historically.

```bash
# Make sure your master branch has the latest changes from CVS
$ git checkout master
$ cvs up -Pd
$ git add -A [files]
$ git commit -m 'cvs update'
# Then merge and commit your changes
$ git merge new-feature
$ cvs commit
```

It's a good idea to delete merged branches, since the history will not be deleted and it keeps
the list of branches to just the ones being currently worked on.

```bash
# List your branches
$ git branch
# Delete a merged branch
$ git branch -d new-feature
```
