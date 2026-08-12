#  Git Commands

> **Repository:** DevOps Git Notes — Section 8 (Final Section)
>
> A consolidated command reference — remotes, clone/fetch/pull/push, stash, cherry-pick, plus everything from earlier sections in one place.

---

##  Remotes

A **remote** is a pointer to a hosted version of your repo (e.g. on GitHub).

```bash
abdullah@DevOps:~/my-project$ git remote -v
origin  git@github.com:abdullah/my-project.git (fetch)
origin  git@github.com:abdullah/my-project.git (push)
```

| Command | Purpose |
|---|---|
| `git remote -v` | List remotes with their URLs |
| `git remote add origin <url>` | Connect a local repo to a remote |
| `git remote set-url origin <url>` | Change a remote's URL |
| `git remote remove <name>` | Remove a remote |

---

##  Cloning — `git clone`

```bash
abdullah@DevOps:~$ git clone git@github.com:abdullah/my-project.git
abdullah@DevOps:~$ git clone git@github.com:abdullah/my-project.git my-folder-name   # Clone into a custom folder name
```

`clone` copies the **entire** repository — full history, all branches — down to your machine in one step.

---

##  Fetch vs Pull

| Command | What It Does |
|---|---|
| `git fetch` | Downloads new commits from the remote, but does **not** merge them into your current branch |
| `git pull` | `fetch` **+** `merge` (or `rebase`) in one step — updates your current branch immediately |

```bash
abdullah@DevOps:~/my-project$ git fetch origin
abdullah@DevOps:~/my-project$ git pull origin main
abdullah@DevOps:~/my-project$ git pull --rebase origin main   # Pull with rebase instead of merge
```

> 💡 `git fetch` is the "safe" option — it lets you review incoming changes (`git log origin/main`) before deciding to merge them.

---

##  Pushing — `git push`

```bash
abdullah@DevOps:~/my-project$ git push origin main
abdullah@DevOps:~/my-project$ git push -u origin feature-login   # Push + set upstream tracking (first push of a new branch)
abdullah@DevOps:~/my-project$ git push                            # After -u is set once, just "git push" works
```

| Flag | Purpose |
|---|---|
| `-u` / `--set-upstream` | Links your local branch to a remote branch — needed only on the first push of a new branch |
| `--force` / `-f` | Overwrites the remote history — ⚠️ dangerous, avoid on shared branches |
| `--force-with-lease` | Safer force-push — fails if someone else pushed since your last fetch |

---

##  Stashing — `git stash`

Temporarily shelves uncommitted changes so you can switch branches cleanly, without committing half-finished work.

```bash
abdullah@DevOps:~/my-project$ git stash                    # Stash current changes
abdullah@DevOps:~/my-project$ git stash list                # List all stashes
abdullah@DevOps:~/my-project$ git stash pop                 # Reapply the most recent stash and remove it from the list
abdullah@DevOps:~/my-project$ git stash apply                # Reapply the most recent stash but keep it in the list
abdullah@DevOps:~/my-project$ git stash drop                 # Delete the most recent stash without applying it
abdullah@DevOps:~/my-project$ git stash save "wip: login form"   # Stash with a descriptive message
```

---

##  Cherry-Pick — `git cherry-pick`

Applies **one specific commit** from another branch onto your current branch, without merging the whole branch.

```bash
abdullah@DevOps:~/my-project$ git cherry-pick a1b2c3d
```

Useful for pulling a single bug fix into `main` without dragging in an entire unfinished feature branch.

---

##  Cleaning Untracked Files — `git clean`

```bash
abdullah@DevOps:~/my-project$ git clean -n       # Dry run — show what WOULD be deleted
abdullah@DevOps:~/my-project$ git clean -f        # Actually delete untracked files
abdullah@DevOps:~/my-project$ git clean -fd       # Also delete untracked directories
```

> ⚠️ Always run `git clean -n` first — there's no undo once files are deleted.

---

##  Full Master Cheat Sheet

### Setup
| Command | Purpose |
|---|---|
| `git init` | Initialize a new repo |
| `git clone <url>` | Clone an existing repo |
| `git config --global user.name "Abdullah"` | Set commit author name |
| `git config --global user.email "..."` | Set commit author email |

### Everyday Workflow
| Command | Purpose |
|---|---|
| `git status` | Show working directory/staging state |
| `git add <file>` / `git add .` | Stage changes |
| `git commit -m "msg"` | Commit staged changes |
| `git commit -am "msg"` | Stage + commit tracked files |
| `git log --oneline --graph --all` | View history visually |
| `git diff` | Show unstaged changes |

### Branching & Merging
| Command | Purpose |
|---|---|
| `git branch` | List branches |
| `git switch -c <name>` | Create + switch to a branch |
| `git merge <name>` | Merge a branch |
| `git rebase <name>` | Replay commits on top of another branch |
| `git branch -d <name>` | Delete a merged branch |

### Undoing Things
| Command | Purpose |
|---|---|
| `git restore <file>` | Discard uncommitted changes |
| `git reset --soft/--mixed/--hard HEAD~1` | Undo last commit (varying severity) |
| `git revert <hash>` | Safely undo a pushed commit |
| `git reflog` | Recover "lost" commits |

### Remote Operations
| Command | Purpose |
|---|---|
| `git remote add origin <url>` | Link to a remote |
| `git fetch` | Download without merging |
| `git pull` | Download + merge |
| `git push` | Upload commits |
| `git push -u origin <branch>` | First push of a new branch |

### Tags & Releases
| Command | Purpose |
|---|---|
| `git tag -a v1.0.0 -m "msg"` | Create an annotated tag |
| `git push origin --tags` | Push all tags |

### Extras
| Command | Purpose |
|---|---|
| `git stash` / `git stash pop` | Shelve and restore uncommitted work |
| `git cherry-pick <hash>` | Apply one commit from another branch |
| `git clean -fd` | Delete untracked files/directories |
| `git show <hash>` | Show details of a specific commit |
| `git blame <file>` | Show who last changed each line of a file |

---

##  Key Takeaways

- `fetch` downloads without merging (safe, review-first); `pull` downloads **and** merges in one step.
- `git stash` is the go-to when you need to switch branches but aren't ready to commit — `stash` → switch → `stash pop` when you're back.
- `cherry-pick` grabs a single commit without merging an entire branch — useful for hotfixes.
- Always dry-run `git clean -n` before `git clean -f` — deleted untracked files are unrecoverable.
- `-u`/`--set-upstream` is only needed on a branch's **first** push — after that, plain `git push`/`git pull` know where to go.
- This cheat sheet, combined with the Introduction, Versioning, Branches, Rollback, SSH, and Tags notes, covers the full day-to-day Git toolkit for DevOps work.

---

##  Topics Covered in This Repository (GIT Section)

- [x] Introduction
- [x] Versioning
- [x] Branches & More
- [x] Rollback
- [x] Git SSH Login
- [x] Git Tags, Semantic Versioning & More
- [x] Setup GitHub Copilot
- [x] Git Commands

---

*Course: DecodingDevOps by Imran Teli (Udemy) | Status: ✅ GIT section complete — 8/8*
