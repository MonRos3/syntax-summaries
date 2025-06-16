# GIT COMMANDS

## SETTING UP YOUR GIT METADATA

```bash
git config --global credential.helper store
git config --global push.default simple
git config --global user.name <Your Name>
git config --global user.email <Your Email>
git config --global core.eol lf
git config --global core.autocrlf input
```

## GETTING STARTED

Initialize git repo to track existing project:

```bash
git init
```

Connect local repo to remote origin:

```bash
git branch —set-upstream-to=origin/<branch> <branch>git branch
```

## CHECKING OUT THE FILE STRUCTURE

List files and folders, including HIDDEN:

```bash
ls -a
```

List contents of .git [if you want to check it]:

```bash
ls .git
```

## CHECKING YOUR BRANCH AND FILE STATUSES

```bash
git status
git fetch --all
git branch -a
git checkout -b branch origin/branch
```

## ADDING AND COMMITTING FILES

```bash
git add <file>
git commit -m “update message here”
```

Also valid commit message:

```bash
git commit -m “update title" -m "update description"
```

To add a tag [for significant commit]:

```bash
git tag “v1.0”
```
