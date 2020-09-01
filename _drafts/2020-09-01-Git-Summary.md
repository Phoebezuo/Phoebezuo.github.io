---
layout:     post
title:      Git Summary
date:       2020-09-01
summary:    Summary notes for Git commands
categories: Programming Git VCS
---

## Git: three states

-   commited - stored in local database
-   modified - file changed but not commited to database
-   staged - modified file is marked to go into the next commit snapshot

![epGD8svhYdcWT5Q](https://i.loli.net/2020/09/01/epGD8svhYdcWT5Q.png)

## Setup

```java
git config --global user.name "Name Surname"
git config --global user.email name.surname@gmail.com
```

## Init

```java
git init // intialize an existing directory as a git repository
git clone [url] // retireve
```

## Recording changes to repository

```java
git add . // start tracking all changed/new files
git commit -m 'Commit message' // save changes to the local repository
git status // check status of your project
git diff // what changed but not yet staged
git log // view the commit history
```

![ABdRfJFbDi9HpgZ](https://i.loli.net/2020/09/01/ABdRfJFbDi9HpgZ.png)

## Working with remotes

```java
git fetch // fetch all info not have in remote repository, no automatical merging
git merge // automatically merge data from remote
git pull // fetch and merge automatically
git push origin master // push your version to the server
```

*note:* pull = fetch + merge
