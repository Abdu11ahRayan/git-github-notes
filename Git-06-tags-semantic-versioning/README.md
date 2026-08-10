#  Git Tags, Semantic Versioning & More

> **Repository:** DevOps Git Notes — Section 6
>
> Marking specific commits as releases — how software communicates "this is version 2.1.0" in a way tools and humans both understand.

---

##  What is a Git Tag?

A tag is a permanent, named pointer to a specific commit — usually used to mark **release points** (v1.0.0, v2.1.0, etc.). Unlike branches, tags don't move as new commits are added.

```
main:  A---B---C---D---E
                |       \
              v1.0.0    v1.1.0
```

---

##  Two Types of Tags

| Type | Command | Stores |
|---|---|---|
| **Lightweight** | `git tag v1.0.0` | Just a pointer to a commit — no extra metadata |
| **Annotated** | `git tag -a v1.0.0 -m "message"` | Full object: tagger name, email, date, and message — recommended for releases |

```bash
abdullah@DevOps:~/my-project$ git tag v1.0.0-lite                          # Lightweight tag
abdullah@DevOps:~/my-project$ git tag -a v1.0.0 -m "First stable release"  # Annotated tag (recommended)
```

> 💡 Use **annotated** tags for anything that represents a real release — they carry metadata (who tagged it, when, and why) that lightweight tags don't.

---

##  Listing & Inspecting Tags

```bash
abdullah@DevOps:~/my-project$ git tag
v1.0.0
v1.1.0

abdullah@DevOps:~/my-project$ git show v1.0.0
tag v1.0.0
Tagger: Abdullah <abdullah@example.com>
Date:   Wed Aug 5 10:00:00 2026 +0500

First stable release

commit a1b2c3d...
```

---

##  Tagging an Older Commit

```bash
abdullah@DevOps:~/my-project$ git log --oneline
a1b2c3d Fix login bug
e5f6g7h Add signup page
h9i0j1k Initial commit

abdullah@DevOps:~/my-project$ git tag -a v0.9.0 e5f6g7h -m "Beta release"
```

---

##  Pushing Tags to a Remote

Tags are **not** pushed automatically with `git push` — they need to be pushed explicitly.

```bash
abdullah@DevOps:~/my-project$ git push origin v1.0.0        # Push a single tag
abdullah@DevOps:~/my-project$ git push origin --tags        # Push all local tags
```

---

##  Deleting Tags

```bash
abdullah@DevOps:~/my-project$ git tag -d v1.0.0-lite                  # Delete a local tag
abdullah@DevOps:~/my-project$ git push origin --delete v1.0.0-lite    # Delete a tag from the remote
```

---

##  Semantic Versioning (SemVer)

The industry-standard convention for version numbers: **`MAJOR.MINOR.PATCH`** (e.g. `2.4.1`).

| Segment | Increments When | Example |
|---|---|---|
| **MAJOR** | Breaking/incompatible changes | `1.x.x → 2.0.0` |
| **MINOR** | New backward-compatible features | `2.4.x → 2.5.0` |
| **PATCH** | Backward-compatible bug fixes | `2.4.1 → 2.4.2` |

**Pre-release and build metadata (optional):**

```
1.0.0-alpha        # Pre-release
1.0.0-beta.2        # Pre-release, iteration 2
1.0.0+20260805       # Build metadata
```

> 💡 A version like `0.x.x` conventionally means the project is still in initial development — anything can change at any time.

### Why It Matters in DevOps

- Package managers (`npm`, `pip`, `apt`) rely on SemVer to resolve dependency compatibility automatically.
- CI/CD pipelines often auto-tag releases based on SemVer, then trigger deployments from that tag.
- Docker image tags frequently follow SemVer (`myapp:2.4.1`, `myapp:2.4`, `myapp:latest`).

---

##  Quick Reference

| Command | Purpose |
|---|---|
| `git tag v1.0.0` | Create a lightweight tag on the latest commit |
| `git tag -a v1.0.0 -m "msg"` | Create an annotated tag (recommended) |
| `git tag -a v1.0.0 <hash> -m "msg"` | Tag a specific older commit |
| `git tag` | List all tags |
| `git show <tag>` | Show tag details and metadata |
| `git push origin <tag>` | Push a single tag to the remote |
| `git push origin --tags` | Push all local tags to the remote |
| `git tag -d <tag>` | Delete a local tag |
| `git push origin --delete <tag>` | Delete a tag from the remote |

---

##  Key Takeaways

- Tags mark a specific commit permanently — unlike branches, they don't move.
- Annotated tags (`-a`) are the standard for real releases since they carry a message, author, and date; lightweight tags are just bare pointers.
- Tags are **not** pushed with a normal `git push` — you must push them explicitly (`--tags` or by name).
- **Semantic Versioning (MAJOR.MINOR.PATCH)** is the near-universal convention: bump MAJOR for breaking changes, MINOR for new features, PATCH for bug fixes.
- SemVer isn't just a naming convention — package managers, CI/CD pipelines, and Docker registries all depend on it to resolve compatibility automatically.

---

##  Topics Covered in This Repository (GIT Section)

- [x] Introduction
- [x] Versioning
- [x] Branches & More
- [x] Rollback
- [x] Git SSH Login
- [x] Git Tags, Semantic Versioning & More
- [ ] Setup GitHub Copilot
- [ ] Git Commands

---

*Course: DecodingDevOps by Imran Teli (Udemy) | Status: ✅ Completed*
