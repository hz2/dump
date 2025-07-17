# Git

## `log`

```bash
git log --oneline
git log --graph --oneline --decorate --all
```

## `reset`

```bash
git reset --soft <commit_hash> # reworking changes
git reset --hard <commit_hash> # discard all changes
git reset --hard origin/<branch of remote> # hard reset from a remote branch
```

## `rebase`

```bash
git checkout <branch>
git fetch origin
git rebase origin/master

# if already merged master into branch
git reset --hard HEAD~1
git rebase origin/master
```

## `config`

```bash
git config --global http.postBuffer 524288000 # increase buffer size
git config --local --list # within local repo
git config --list --show-origin # local, global, system

git config --local user.name "Your Name"
git config --local user.email "you@example.com"
```

```bash
git -c user.name=name -c user.email=you@example.com commit -m "msg"
```

## `stash`

- works like a stack, saving changes temporarily

```bash
git stash # save changes
git stash list # list stashes
git stash apply # apply latest stash
git stash apply stash@{n} # apply specific stash
git stash drop stash@{n} # delete specific stash
git stash pop # apply and delete latest stash
```

## `remote`

```bash
git remote -v
git remote show origin
```

## hotfix

```bash
git checkout tags/<version> -b hotfix/<branch> # create a new branch from a tag
git push --set-upstream origin hotfix/<branch> # push the new branch to remote

git fetch
git checkout hotfix/<branch> # switch to the hotfix branch
git checkout -b repair/<branch> # create a new branch for repairs

# make changes, e.g. cherry-pick commits
git cherry-pick <commit_hash> # apply specific commit to current branch
# if conflicts or want to include all the changes with the conflicts
git diff --name-only --diff-filter=U | xargs -I{} git checkout --theirs {}
git add . # to stage all changes
git push --set-upstream origin repair/<branch> # push the repair branch to remote
```
