# Introduction

- Git provides many ways to do the same thing

- what works depends on how your project uses Git

- however it doesn't hurt to know what alternatives are out there so you're not
  totally shocked if some other project does something different

- if you want to learn what any particular command does `git help` will get you
  started with that

# Know what goes into commit

- `git status` is a good starting point to know what what goes into commit

- examine the output carefully, it's actually very helpful and gives you
  instructions about what to do

## Untracked files

- there are two kinds of red lines, first you are going to encounter in a fresh
  repository are untracked files

- pay close attention to untracked files you have, if there's anything there
  that you won't want to add into repository, consider using `.gitignore` in
  order to hide them

- if you remove an untracked file, Git won't be able to restore it

- using `git add` will add them straight to stagin area

## Changes to be commited

- second red lines that you are going to encounter are under header changes not
  staged for commit 

- these changes are shown if you run `git diff` without any parameters

- if you want to remove changes made into a file, you can use `git restore <file>`

- `git add <file>` will move the files to staging area

## Staging area

- green lines indicate what's included in so called staging area and are going
  to be included in commit

- `git diff --cached` can be used to diff between staging area and last commit

- if you made a commit, you can review it by running `git show`

## Formatting commit messages properly

- Git commits can be e-mailed, which is why there are certain formatting rules
  that should be followed

- good editors and IDE:s will helpfully show errors in formatting

- first line should be short 50 characters or less summary of the change

- second line must be always left empty, some tools will get very confused if
  it's not empty

# Writing good commit messages

- good commit message describes the change clearly enough that it can be used
  as is in a pull request

- first line should describe what is being done, rest of the lines should tell
  why and context about the chance

- if commit is a fix, describe what was broken and what you did in order to fix it

- if it's an enhancement, describe what it improves

- some day, good commit message will save your commit from a revert

- also make sure that commit message and diff agree

http://turnoff.us/geek/commit-messages/
http://turnoff.us/geek/when-ai-meets-git/
https://xkcd.com/1296/

# Working on multiple things at the same time

- when you need to work on multiple things at the same time, branches are handy
  way to accomplish that

- branches work bit like tree branches as they branch from the trunk, but
  what's really different that they quite often eventually merge back to the
  trunk, which makes situation look more like metrolines than a tree

# Remotes

- getting most out of remotes is bit of an advanced concept, but they're still
  part of daily workflow, even if you don't notice them

- remote is mechanism is used to tell where the remote repository is

- when you clone a repository, you'll get automatically remote called origin

- when you refer to branch named master, you are referring to your local master
  branch, which can be quite different compared to remote one

- origin/master on the other hand is last known version of the branch on the
  remote side

- when you do `git pull` or `git fetch`, you will get updated versions of the
  branches on the remote side (latter command leaves your local branches alone)

# Merge VS rebase

- common debate is when to use merge and when to use rebase

- both have their uses and even heavy rebase user might have occasional use for
  merge now and then

- merge is pretty much only option if history has to be preserved accurately

- rebase on the other hand by definition rewrites history and repository with
  only rebase users has history as one straight line with no metrolines

# Keeping your branch up to date

- when working on a feature branch for long time, it will slowly drift apart
  from other development

- further it drifts away from master (or branch it's supposed to merged into),
  the eventual merge conflict is going to get harder and harder

- start always with `git fetch` as that will refresh remote branches 

- upstream merge branch is usually origin/master

- with merge process is to do `git merge <upstream merge branch>`

- that will result in messy, but very accurate history, but that's usual with
  merge

- with rebase, `git rebase <upstream merge branch>` will do the same thing, but
  will keep the history cleaner

# Getting back to where you started

- there are situations where you want to just start over

- if you want to reset the situation to any commit, you can use 
  `git reset --hard commit`

- `git reset` doesn't care what branch commit belongs to

- there are to handy shortcuts, `HEAD` will refer to latest commit in the
  current branch, `origin/master` is last known state of master branch in the
  default remote

# Recovering from accidents

- most of the necessary building blocks were already mentioned

- `git log -g` shows low level log of the repository, so if you accidentally
  got rid of commit, you can still see it there and can use `git reset` to get
  that back

- if you get into merge conflict, you can get out of that using `--abort`
  command line option

- `--abort` works with several other commands, remember to use it with same
  command that caused the conflict

# Handling merge conflicts

- eventually you'll get into merge conflict that you just can't abort

- it's perfectly doable to resolve merge conflict by hand without external
  tool, though external tools (or IDE integration) can have more user friendly
  experience

- high level overview is that what you are trying to do is to merge two sides
  of the conflict into result that still makes sense after the conflict is
  resolved

- `git status` and `git diff` will give good overview of the situation

-  if you know that only other side is "right", you can use `git restore --ours
   <file>` or `git restore --theirs <file>` to get file from either side of the
   conflict (just remember that with rebase, the roles are reversed)

- when resolving conflict by hand, note the `<<<`, `===` and `>>>` lines as
  those are added by Git (they are used to indicate both sides of the conflict)

# Code review without Github, Gitlab etc. services

- sending patches for review doesn't necessarily need intermediary like Github
  in between

- most old fashioned way to share patches is mail them (it's still pretty
  common in Linux kernel mailing list)

- bit easier way to do that is share you repository with a file share, SSH, web
  server or whatever seems most convenient

- reviewer can add that location as remote and after start pulling changes

- if reviewee also adds reviewers repository as remote, it's also possible to
  pull suggestions

# Backups

- Git already works bit like versioned backup systems do, making remote backups
  is actually pretty common part of Git workflow

- keep in mind that Git can't get changes back that it doesn't know about

- getting commits back is doable though (`git log -g`)

- when about to do something stupid, you can tag the current commit (just make
  sure you don't push the tag), make new branch out of it or just copy the
  commit hash to somewhere safe

- usually bit overkill, but if you must make local backup, you use git do 
  `git clone` of you current repository in other directory

