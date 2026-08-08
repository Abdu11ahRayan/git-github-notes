#  Git SSH Login

> **Repository:** DevOps Git Notes — Section 5
>
> Setting up SSH authentication so you can push/pull to GitHub without typing a username and password every time.

---

##  Why SSH Instead of HTTPS?

| | HTTPS | SSH |
|---|---|---|
| Authentication | Username + Personal Access Token (password auth is deprecated) | SSH key pair |
| Setup | Simple, but you re-enter credentials or a token often | One-time key setup, then seamless |
| Speed for repeated use | Slower, more prompts | Fast — no repeated prompts |
| Best for | Quick one-off clones | Daily development work |

> 💡 GitHub deprecated password authentication over HTTPS entirely — with HTTPS you now need a Personal Access Token. SSH avoids that friction completely once it's set up.

---

##  Step 1 — Check for Existing SSH Keys

```bash
abdullah@DevOps:~$ ls -al ~/.ssh
id_ed25519      id_ed25519.pub      known_hosts
```

If you see `id_ed25519.pub` or `id_rsa.pub` already, you may already have a key pair — otherwise, generate a new one.

---

##  Step 2 — Generate a New SSH Key

```bash
abdullah@DevOps:~$ ssh-keygen -t ed25519 -C "abdullah@example.com"
Generating public/private ed25519 key pair.
Enter file in which to save the key (/home/abdullah/.ssh/id_ed25519):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/abdullah/.ssh/id_ed25519
Your public key has been saved in /home/abdullah/.ssh/id_ed25519.pub
```

| Flag | Meaning |
|---|---|
| `-t ed25519` | Key type — `ed25519` is the modern, recommended algorithm |
| `-C "email"` | Comment/label attached to the key (usually your email) |

> 💡 If your system is older and doesn't support `ed25519`, use `-t rsa -b 4096` instead.

This creates **two** files:

- `id_ed25519` — your **private** key. Never share this, ever.
- `id_ed25519.pub` — your **public** key. This is safe to share (e.g. paste into GitHub).

---

##  Step 3 — Start the SSH Agent & Add Your Key

```bash
abdullah@DevOps:~$ eval "$(ssh-agent -s)"
Agent pid 12345

abdullah@DevOps:~$ ssh-add ~/.ssh/id_ed25519
Identity added: /home/abdullah/.ssh/id_ed25519 (abdullah@example.com)
```

The SSH agent caches your unlocked key so you're not re-typing your passphrase on every push/pull.

---

##  Step 4 — Copy the Public Key

```bash
abdullah@DevOps:~$ cat ~/.ssh/id_ed25519.pub
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAI... abdullah@example.com
```

Copy the **entire** output, starting with `ssh-ed25519`.

---

##  Step 5 — Add the Key to GitHub

1. Go to **GitHub → Settings → SSH and GPG keys → New SSH key**.
2. Give it a descriptive title (e.g. "Abdullah - DevOps laptop").
3. Paste the public key you copied.
4. Click **Add SSH key**.

---

##  Step 6 — Test the Connection

```bash
abdullah@DevOps:~$ ssh -T git@github.com
Hi Abdullah! You've successfully authenticated, but GitHub does not provide shell access.
```

That message confirms your key is working — GitHub intentionally refuses a shell session, so this "error" is actually success.

---

##  Step 7 — Clone / Switch a Repo to Use SSH

**Cloning fresh with SSH:**

```bash
abdullah@DevOps:~$ git clone git@github.com:abdullah/my-project.git
```

**Switching an existing repo from HTTPS to SSH:**

```bash
abdullah@DevOps:~/my-project$ git remote set-url origin git@github.com:abdullah/my-project.git
abdullah@DevOps:~/my-project$ git remote -v
origin  git@github.com:abdullah/my-project.git (fetch)
origin  git@github.com:abdullah/my-project.git (push)
```

---

##  Quick Reference

| Command | Purpose |
|---|---|
| `ssh-keygen -t ed25519 -C "email"` | Generate a new SSH key pair |
| `eval "$(ssh-agent -s)"` | Start the SSH agent |
| `ssh-add ~/.ssh/id_ed25519` | Add your key to the agent |
| `cat ~/.ssh/id_ed25519.pub` | Print your public key to copy |
| `ssh -T git@github.com` | Test your SSH connection to GitHub |
| `git clone git@github.com:user/repo.git` | Clone using SSH |
| `git remote set-url origin <ssh-url>` | Switch an existing repo from HTTPS to SSH |

---

##  Key Takeaways

- SSH keys come in pairs: **private** (never shared, stays on your machine) and **public** (safe to paste into GitHub).
- `ed25519` is the modern recommended key type; `rsa -b 4096` is the fallback for older systems.
- `ssh -T git@github.com` is the standard way to verify your setup — the "no shell access" message means success, not failure.
- Once SSH is configured, `git clone`/`push`/`pull` never prompt for a username or token again.
- An existing HTTPS-cloned repo can be switched to SSH with `git remote set-url` — no need to re-clone.

---

##  Topics Covered in This Repository (GIT Section)

- [x] Introduction
- [x] Versioning
- [x] Branches & More
- [x] Rollback
- [x] Git SSH Login
- [ ] Git Tags, Semantic Versioning & More
- [ ] Setup GitHub Copilot
- [ ] Git Commands

---

*Course: DecodingDevOps by Imran Teli (Udemy) | Status: ✅ Completed*
