#  Git Introduction

> **Repository:** DevOps Git Notes — Section 1
>
> Structured notes on Git — the version control system every DevOps engineer, developer, and CI/CD pipeline depends on.

---

##  What is Git?

Git is a free and open-source **Distributed Version Control System (DVCS)** created by **Linus Torvalds** in 2005 (the same person who created the Linux kernel) to manage the Linux kernel's source code.

Git tracks changes to files over time, so you can:

- See the full history of every change
- Revert to any previous version
- Work on multiple features in parallel (branches)
- Collaborate with a team without overwriting each other's work

---

##  Version Control: Centralized vs Distributed

| | **Centralized VCS** (e.g. SVN) | **Distributed VCS** (Git) |
|---|---|---|
| History location | One central server only | Every clone has the **full** history |
| Working offline | Requires network access | Works fully offline — commit, branch, view history locally |
| Single point of failure | Yes — if the server dies, history is lost | No — every developer's clone is a full backup |
| Speed | Slower (network round-trips) | Fast — most operations are local |

> 💡 In Git, when you `clone` a repository, you get **the entire project history** on your machine — not just the latest snapshot.

---

##  Why Git for DevOps?

- Every CI/CD pipeline (Jenkins, GitLab CI, GitHub Actions) is triggered by Git events (push, merge, tag).
- Infrastructure as Code (Terraform, Ansible) is version-controlled in Git, just like application code.
- Git enables safe collaboration — multiple engineers can work on infra/app changes without stepping on each other.
- Rollbacks, audits, and change history are all built on Git's log.

---

##  Installing Git

```bash
# Ubuntu/Debian
abdullah@DevOps:~$ sudo apt update
abdullah@DevOps:~$ sudo apt install git -y

# CentOS/RHEL
[abdullah@DevOps ~]$ sudo yum install git -y
```

**Verify installation:**

```bash
abdullah@DevOps:~$ git --version
git version 2.43.0
```

---

##  First-Time Configuration

Before your first commit, Git needs to know who you are — this info gets attached to every commit you make.

```bash
abdullah@DevOps:~$ git config --global user.name "Abdullah"
abdullah@DevOps:~$ git config --global user.email "abdullah@example.com"
```

**Check your configuration:**

```bash
abdullah@DevOps:~$ git config --list
user.name=Abdullah
user.email=abdullah@example.com
```

| Flag | Scope |
|---|---|
| `--global` | Applies to all repos for your user account |
| `--local` | Applies only to the current repo (default if no flag is given) |
| `--system` | Applies to every user on the machine |

---

##  The Three States of a Git File

Git tracks files across three main areas:

```
Working Directory  --(git add)-->  Staging Area  --(git commit)-->  Repository (.git)
```

| Area | Description |
|---|---|
| **Working Directory** | Your actual project files on disk, as you edit them |
| **Staging Area (Index)** | Files marked/ready to be included in the next commit |
| **Repository (`.git`)** | The permanent, committed history of the project |

---

##  Creating a Repository

```bash
abdullah@DevOps:~$ mkdir my-project
abdullah@DevOps:~$ cd my-project
abdullah@DevOps:~/my-project$ git init
Initialized empty Git repository in /home/abdullah/my-project/.git/
```

`git init` creates a hidden `.git` folder — this **is** the repository; it stores all history, branches, and configuration.

---

##  Checking Status

```bash
abdullah@DevOps:~/my-project$ git status
On branch main
No commits yet
nothing to commit (create/copy files and use "git add" to track)
```

`git status` is the command you'll run constantly — it shows what's changed, what's staged, and what's not tracked yet.

---

##  Quick Reference

| Command | Purpose |
|---|---|
| `git --version` | Check installed Git version |
| `git config --global user.name "..."` | Set your commit author name |
| `git config --global user.email "..."` | Set your commit author email |
| `git config --list` | View current configuration |
| `git init` | Initialize a new Git repository |
| `git status` | Show current state of the working directory/staging area |

---

##  Key Takeaways

- Git is a **distributed** version control system — every clone has the full project history, not just the latest files.
- Set `user.name` and `user.email` before your first commit — this identifies who made each change.
- Every Git project has three areas: **working directory** → **staging area** → **repository**.
- `git init` turns any folder into a Git repository by creating a `.git` directory.
- `git status` is your most-used command — always check it before committing.

---

##  Topics Covered in This Repository (GIT Section)

- [x] Introduction
- [ ] Versioning
- [ ] Branches & More
- [ ] Rollback
- [ ] Git SSH Login
- [ ] Git Tags, Semantic Versioning & More
- [ ] Setup GitHub Copilot
- [ ] Git Commands

---

*Course: DecodingDevOps by Imran Teli (Udemy) | Status: ✅ Completed*
