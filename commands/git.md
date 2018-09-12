Git Commands
===

## Everyday commands
- View the current status of local git: modified files, deleted fileds, unstage files...

```
$ git status
```

- Add all currently changes in stage for commit.
```
$ git add .
```

- Unstage a file after add.

```
$ git reset [file_url]
```

- Commit and push on branch `develop` (remote: `origin`).

```
$ git commit -m "This is a message."
$ git push origin develop
```

- Save the currently changes in stash.
```
$ git stash
```

- Get the previously changes in stash.
```
$ git stash pop
```

- Pull changes on current branch `develop`.

```
$ git pull origin develop
```

- Merge changes from the branch `feature/newUI` into the currently working branch.

```
$ git pull origin feature/newUI
```

- Checkout a new branch named `hotfix/fixUI` from remote `orgin`.

```
$ git fetch origin && git checkout hotfix/fixUI
```

## Other stuffs
- Cherry pick a specified commit.

```
$ git cherry-pick [commit]
```

- View info about the currently remotes in local git.

```
$ git remote -v
```

- Add a remote

```
$ git remote add [remote-name] [remote-url]
```

- View info about email of current account.
```
$ git config user.email
```

- Config account info of local git

```
$ git config user.name [your-name]
$ git config user.email [your-git-email]
```

- Git commit for using the default message after manual fix conflicts

```
$ git commit --no-edit
```