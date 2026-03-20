# 💻 Git Terminal Cheat Sheet

---

## Git Setup & Info

```zsh
git --version # shows git version
git config --global user.name "Your Name" # sets commit name
git config --global user.email "you@example.com" # sets commit email
git config --list # show all git config settings
git help <command> # shows help for specified command
```

---

## Repositories

```bash
git init # creates local repo
git clone <repo-url> # copies remote repo locally
```

---

## Status & Changes

```bash
git status # shows current state (changes, staging, branch)
git diff # shows unstaged changes
git diff --staged # shows staged changes
git show # details of latest commit (or specified object)
```

---

## Staging

```bash
git add <file> # stages specific file
git add . # stages all changes
git add -p # shows details of latest commit (or specified object) *1
git restore <file> # discards changes in working directory
git restore --staged <file> # unstages specified file
```

1. Lets you stage **specific parts of a file**, not the whole file.

- Git breaks changes into chunks (“hunks”) and shows them one by one
- For each chunk, you choose what to do:
  - `y` → stage this chunk
  - `n` → skip it
  - `s` → split into smaller chunks
  - `e` → manually edit the patch

**Why it matters:**  
You can make clean, focused commits (e.g., separate a bug fix from formatting changes in the same file).

---

## Committing

```bash
git commit -m "message" # commits staged changes
git commit -am "message" # stages & commits tracked files
git commit --amend # edits last commit *2
```

2. Modifies the **most recent commit** instead of creating a new one.

- If you staged new changes → they get added to the last commit
- If no new changes → lets you edit the commit message

**Common uses:**

- Forgot to include a file → stage it, then `--amend`
- Fix a typo in commit message

**Important:**

- Rewrites history → avoid using it on commits already pushed/shared

---

## Branching

```bash
git branch # lists branches
git branch <branch-name> # creates a branch
git switch <branch-name>  # switches branch
git switch -c <branch-name> # creates & switches
git branch -d <branch-name> # deletes branch
```

---

### Merging & Rebasing

```zsh
git merge <branch> # merges branch into current
git rebase <branch> # replays commits onto another base *3
git rebase --continue # continues after conflict fix
git rebase --abort # cancels rebase
```

3. Moves your branch so it starts from another branch, **replaying your commits on top**.

**Concept:**  
Instead of merging histories, Git:

1. Takes your commits
2. Temporarily removes them
3. Reapplies them on top of `<branch>`

**Before:**

```
A---B---C  (main)
     \
      D---E  (your branch)
```

**After `git rebase main`:**

```
A---B---C---D'---E'  (your branch)

(`D'` and `E'` are rewritten versions)
```

**Why it matters:**

- Creates a **clean, linear history** (no merge commits)
- Makes it look like you started from the latest version of `<branch>`

**Risks:**

- Rewrites commit history → don’t rebase shared branches unless you know what you're doing
- Conflicts may need to be resolved commit-by-commit

---

## Remotes

```bash
git remote -v # lists remote repos
git remote add origin <url> # adds remote
git remote set-url origin <url> # changes remote url
```

---

## Push & Pull

```zsh
git pull
git pull --rebase
git push
git push -u origin <branch>
```

---

## Logs & History

```bash
git log # fetches & merges remote changes
git log --oneline --graph --all # compact visual history
git reflog # history of HEAD movements (good for recovery)
```

---

## Undo & Fix Mistakes

```zsh
git reset <file> # unstages file
git reset --soft HEAD~1 # undo commit, keep changes staged
git reset --hard HEAD~1 # delete last commit & changes
git checkout -- <file> # discard file (older syntax)
git revert <commit> # creates a new commit that undoes another
```

---

## Stashing

```zsh
git stash # temporarily saves changes
git stash push -m "message" # stash with label
git stash list # shows stashes
git stash apply # reapplies stash
git stash pop # reapplies & removes stash
```

---

## Cleaning

```zsh
git clean -n # preview files to delete
git clean -fd # deleted untracked files
```

---

## Tags (optional but common)

```zsh
git tag # lists tags
git tag <tag-name> # creates a tag
git push --tags # pushes tags to remote
```

---
