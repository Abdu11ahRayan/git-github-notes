#  Versioning

> **Repository:** DevOps Git Notes — Section 2
>
> The core Git workflow — staging, committing, and inspecting history. This is the loop you'll run hundreds of times a day.

---

##  The Basic Git Workflow

```
edit files  →  git add  →  git commit  →  git push
   (working dir)   (staging)     (local repo)   (remote repo)
```

---

##  Staging Changes — `git add`

```bash
abdullah@DevOps:~/my-project$ touch index.html
abdullah@DevOps:~/my-project$ git status
Untracked files:
  index.html

abdullah@DevOps:~/my-project$ git add index.html
abdullah@DevOps:~/my-project$ git status
Changes to be committed:
  new file:   index.html
```

| Command | Purpose |
|---|---|
| `git add <file>` | Stage a specific file |
| `git add .` | Stage all changed/new files in the current directory |
| `git add -A` | Stage all changes across the whole repo (including deletions) |
| `git add -p` | Interactively stage specific chunks (hunks) of a file |

---

##  Committing Changes — `git commit`

A commit is a permanent snapshot of your staged changes, with a message describing what changed.

```bash
abdullah@DevOps:~/my-project$ git commit -m "Add initial index.html"
[main (root-commit) a1b2c3d] Add initial index.html
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 index.html
```

| Command | Purpose |
|---|---|
| `git commit -m "message"` | Commit staged changes with an inline message |
| `git commit -am "message"` | Stage **and** commit all tracked, modified files in one step (skips new/untracked files) |
| `git commit --amend` | Edit the most recent commit (message and/or content) |

> ⚠️ `git commit -am` only works on files Git is **already tracking** — brand-new files still need `git add` first.

---

##  Viewing History — `git log`

```bash
abdullah@DevOps:~/my-project$ git log
commit a1b2c3d4e5f6...
Author: Abdullah <abdullah@example.com>
Date:   Wed Aug 5 10:00:00 2026 +0500

    Add initial index.html
```

| Command | Purpose |
|---|---|
| `git log` | Full commit history |
| `git log --oneline` | One line per commit — compact view |
| `git log --oneline --graph --all` | Visual branch/commit graph |
| `git log -p` | Show the actual diff for each commit |
| `git log -n 5` | Show only the last 5 commits |
| `git show <commit-hash>` | Show details + diff of a specific commit |

---

##  Comparing Changes — `git diff`

```bash
abdullah@DevOps:~/my-project$ git diff
```

| Command | Purpose |
|---|---|
| `git diff` | Compare working directory vs staging area (unstaged changes) |
| `git diff --staged` | Compare staging area vs last commit (staged changes) |
| `git diff <commit1> <commit2>` | Compare two commits |
| `git diff <branch1> <branch2>` | Compare two branches |

---

##  Ignoring Files — `.gitignore`

Some files should never be committed — build artifacts, secrets, dependency folders, OS junk files.

```bash
abdullah@DevOps:~/my-project$ vim .gitignore
```

```gitignore
node_modules/
*.log
.env
__pycache__/
.DS_Store
```

Git will skip anything matching these patterns when you run `git add .` or `git status`.

---

##  Quick Reference

| Command | Purpose |
|---|---|
| `git add <file>` | Stage a file |
| `git add .` | Stage everything in the current directory |
| `git commit -m "msg"` | Commit staged changes |
| `git commit -am "msg"` | Stage + commit tracked file changes |
| `git commit --amend` | Modify the last commit |
| `git log` | View commit history |
| `git log --oneline` | Compact history view |
| `git diff` | Show unstaged changes |
| `git diff --staged` | Show staged changes |
| `.gitignore` | File listing patterns Git should never track |

---

##  Key Takeaways

- The core loop is: **edit → `git add` → `git commit`** — repeated constantly.
- `git add` moves changes into the staging area; `git commit` permanently records what's staged.
- `git commit -am` is a shortcut, but only for files Git already tracks — new files always need `git add` first.
- `git log --oneline --graph --all` is the fastest way to visualize project history and branches at a glance.
- A `.gitignore` file keeps junk (secrets, build output, dependencies) out of your repo from the start — set it up before your first commit whenever possible.

---

##  Topics Covered in This Repository (GIT Section)

- [x] Introduction
- [x] Versioning
- [ ] Branches & More
- [ ] Rollback
- [ ] Git SSH Login
- [ ] Git Tags, Semantic Versioning & More
- [ ] Setup GitHub Copilot
- [ ] Git Commands

---

*Course: DecodingDevOps by Imran Teli (Udemy) | Status: ✅ Completed*
