#  Rollback

> **Repository:** DevOps Git Notes — Section 4
>
> Undoing mistakes safely — from unstaging a file to reverting a commit that's already been pushed to production.

---

##  Which "Undo" Do I Need?

| Situation | Command |
|---|---|
| Unstage a file (keep the edits) | `git restore --staged <file>` |
| Discard uncommitted changes to a file | `git restore <file>` |
| Undo the last commit, keep the changes | `git reset --soft HEAD~1` |
| Undo the last commit, unstage the changes | `git reset --mixed HEAD~1` |
| Undo the last commit, **discard** the changes entirely | `git reset --hard HEAD~1` |
| Safely undo a commit that's already **pushed/shared** | `git revert <commit-hash>` |
| Restore an old version of one file | `git checkout <commit-hash> -- <file>` |

---

##  Unstaging & Discarding — `git restore`

```bash
abdullah@DevOps:~/my-project$ git add index.html
abdullah@DevOps:~/my-project$ git restore --staged index.html    # Unstage, keep the edits
abdullah@DevOps:~/my-project$ git restore index.html             # Discard uncommitted edits entirely
```

> ⚠️ `git restore <file>` (without `--staged`) **permanently discards** your uncommitted edits — there's no undo for this one.

---

##  Undoing Commits — `git reset`

`git reset` moves your branch pointer backward. The 3 modes control what happens to your changes:

```bash
abdullah@DevOps:~/my-project$ git reset --soft HEAD~1
```

| Mode | Working Directory | Staging Area | Commit History |
|---|---|---|---|
| `--soft` | Unchanged | Changes kept staged | Commit removed |
| `--mixed` (default) | Unchanged | Changes unstaged | Commit removed |
| `--hard` | **Changes discarded** | Changes discarded | Commit removed |

```bash
abdullah@DevOps:~/my-project$ git reset --hard HEAD~1     # ⚠️ Fully discards the last commit and its changes
abdullah@DevOps:~/my-project$ git reset --hard <commit-hash>    # Reset all the way back to a specific commit
```

> ⚠️ **`git reset --hard` is destructive** — any uncommitted or now-orphaned commits can be lost. Only use it on commits **not yet pushed** to a shared remote.

---

##  Undoing a Pushed Commit — `git revert`

Unlike `reset`, `revert` doesn't rewrite history — it creates a **new commit** that undoes the changes of a previous one. This makes it safe for commits that others have already pulled.

```bash
abdullah@DevOps:~/my-project$ git revert a1b2c3d
[main f7g8h9i] Revert "Add broken login validation"
 1 file changed, 3 deletions(-)
```

| | `reset` | `revert` |
|---|---|---|
| Rewrites history | Yes | No — adds a new commit |
| Safe on pushed/shared commits |  No |  Yes |
| Use case | Cleaning up local, unpushed commits | Undoing something already deployed/shared |

---

##  Restoring an Old Version of One File

```bash
abdullah@DevOps:~/my-project$ git log --oneline index.html
abdullah@DevOps:~/my-project$ git checkout a1b2c3d -- index.html
```

This pulls just `index.html` from an old commit into your working directory, without touching anything else — the change still needs `git add` + `git commit` to take effect.

---

##  Time-Traveling Through History — `git reflog`

`reflog` records **every** movement of `HEAD` — even commits that a `reset --hard` seemingly "deleted." It's your safety net.

```bash
abdullah@DevOps:~/my-project$ git reflog
a1b2c3d HEAD@{0}: commit: Add login page
e5f6g7h HEAD@{1}: reset: moving to HEAD~1
```

```bash
abdullah@DevOps:~/my-project$ git reset --hard a1b2c3d      # Recover a commit that seemed lost
```

---

##  Quick Reference

| Command | Purpose |
|---|---|
| `git restore --staged <file>` | Unstage a file |
| `git restore <file>` | Discard uncommitted changes |
| `git reset --soft HEAD~1` | Undo last commit, keep changes staged |
| `git reset --mixed HEAD~1` | Undo last commit, keep changes unstaged |
| `git reset --hard HEAD~1` | Undo last commit, discard changes entirely |
| `git revert <hash>` | Safely undo a pushed commit via a new commit |
| `git checkout <hash> -- <file>` | Restore one file from an old commit |
| `git reflog` | View history of `HEAD` movements (recovery safety net) |

---

##  Key Takeaways

- `git restore` handles the working directory/staging area; `git reset` and `git revert` handle commit history.
- `reset --soft`/`--mixed`/`--hard` differ in how much they discard — `--hard` is the most destructive and should never touch pushed/shared commits.
- `git revert` is the **safe** way to undo something already shared — it adds a new commit instead of rewriting history.
- `git reflog` is your safety net — even a "lost" commit after `reset --hard` can usually be recovered from it.
- **Golden rule:** `reset` for local, unpushed mistakes; `revert` for anything already pushed or deployed.

---

##  Topics Covered in This Repository (GIT Section)

- [x] Introduction
- [x] Versioning
- [x] Branches & More
- [x] Rollback
- [ ] Git SSH Login
- [ ] Git Tags, Semantic Versioning & More
- [ ] Setup GitHub Copilot
- [ ] Git Commands

---

*Course: DecodingDevOps by Imran Teli (Udemy) | Status: ✅ Completed*
