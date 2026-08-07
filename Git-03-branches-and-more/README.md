#  Branches & More

> **Repository:** DevOps Git Notes — Section 3
>
> Branches let you work on features, fixes, and experiments in isolation — without touching the stable codebase until you're ready to merge.

---

##  What is a Branch?

A branch is just a movable pointer to a commit. The default branch is usually `main` (older repos use `master`). Creating a new branch lets you make commits without affecting other branches until you explicitly merge.

```
main:      A---B---C
                    \
feature:             D---E
```

---

##  Listing Branches

```bash
abdullah@DevOps:~/my-project$ git branch
* main
```

`*` marks the branch you're currently on.

```bash
abdullah@DevOps:~/my-project$ git branch -a       # List all branches, including remote ones
abdullah@DevOps:~/my-project$ git branch -r       # List only remote branches
```

---

##  Creating a Branch

```bash
abdullah@DevOps:~/my-project$ git branch feature-login
abdullah@DevOps:~/my-project$ git branch
* main
  feature-login
```

`git branch <name>` **creates** the branch but doesn't switch to it.

---

##  Switching Branches — `checkout` / `switch`

```bash
abdullah@DevOps:~/my-project$ git checkout feature-login
Switched to branch 'feature-login'

# Newer, clearer syntax (Git 2.23+)
abdullah@DevOps:~/my-project$ git switch feature-login
```

**Create and switch in one step:**

```bash
abdullah@DevOps:~/my-project$ git checkout -b feature-signup
abdullah@DevOps:~/my-project$ git switch -c feature-signup
```

| Command | Purpose |
|---|---|
| `git branch <name>` | Create a new branch |
| `git checkout <name>` / `git switch <name>` | Switch to an existing branch |
| `git checkout -b <name>` / `git switch -c <name>` | Create and switch in one step |
| `git branch -d <name>` | Delete a branch (safe — won't delete unmerged work) |
| `git branch -D <name>` | Force-delete a branch (even if unmerged) |

---

##  Merging Branches — `git merge`

Merging brings the changes from one branch into another (usually a feature branch into `main`).

```bash
abdullah@DevOps:~/my-project$ git checkout main
abdullah@DevOps:~/my-project$ git merge feature-login
Updating a1b2c3d..e5f6g7h
Fast-forward
 login.html | 1 +
 1 file changed, 1 insertion(+)
```

### Two Types of Merges

| Type | When It Happens |
|---|---|
| **Fast-forward** | `main` hasn't moved since the branch was created — Git just moves the pointer forward, no merge commit needed |
| **Three-way merge** | Both branches have new commits — Git creates a new **merge commit** joining both histories |

---

##  Merge Conflicts

A conflict happens when the same lines were changed differently on both branches. Git pauses and marks the conflicting section:

```
<<<<<<< HEAD
This is the main branch version.
=======
This is the feature branch version.
>>>>>>> feature-login
```

**Resolving a conflict:**

1. Open the file, manually edit it to keep the correct content, and remove the `<<<<<<<`, `=======`, `>>>>>>>` markers.
2. Stage the resolved file: `git add <file>`
3. Complete the merge: `git commit`

---

##  Rebasing — `git rebase`

Rebase replays your branch's commits on top of another branch, creating a **linear** history instead of a merge commit.

```bash
abdullah@DevOps:~/my-project$ git checkout feature-login
abdullah@DevOps:~/my-project$ git rebase main
```

| | `merge` | `rebase` |
|---|---|---|
| History | Preserves branch structure, adds a merge commit | Rewrites history into a straight line |
| Safety | Safe on shared/public branches | Never rebase commits already pushed & shared with others |
| Use case | Merging finished feature branches into `main` | Cleaning up your local commits before sharing |

> ⚠️ **Golden rule:** never rebase a branch that others have already pulled/based work on — it rewrites commit history and causes conflicts for everyone else.

---

##  Quick Reference

| Command | Purpose |
|---|---|
| `git branch` | List local branches |
| `git branch -a` | List all branches (local + remote) |
| `git branch <name>` | Create a branch |
| `git checkout <name>` / `git switch <name>` | Switch branches |
| `git checkout -b <name>` / `git switch -c <name>` | Create + switch in one step |
| `git branch -d <name>` | Delete a merged branch |
| `git branch -D <name>` | Force-delete an unmerged branch |
| `git merge <name>` | Merge a branch into the current one |
| `git rebase <name>` | Replay current branch's commits on top of another |
| `git add <file>` + `git commit` | Resolve a merge conflict |

---

##  Key Takeaways

- A branch is just a lightweight, movable pointer to a commit — creating one is fast and cheap in Git.
- `git switch`/`git checkout -b` create + move you to a new branch in one step; use it for every new feature/fix.
- Merges combine histories (fast-forward when possible, otherwise a merge commit); rebase rewrites history into a straight line.
- Merge conflicts happen when the same lines change on both branches — resolve manually, then `git add` + `git commit`.
- **Never rebase shared/pushed commits** — it's safe for cleaning up your own local, unpushed work only.

---

##  Topics Covered in This Repository (GIT Section)

- [x] Introduction
- [x] Versioning
- [x] Branches & More
- [ ] Rollback
- [ ] Git SSH Login
- [ ] Git Tags, Semantic Versioning & More
- [ ] Setup GitHub Copilot
- [ ] Git Commands

---

*Course: DecodingDevOps by Imran Teli (Udemy) | Status: ✅ Completed*
