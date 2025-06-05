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
