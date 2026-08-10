#  Setup GitHub Copilot

> **Repository:** DevOps Git Notes — Section 7
>
> Getting AI-assisted code completion set up in your editor — useful for scripts, IaC, and everyday coding.

---

##  What is GitHub Copilot?

GitHub Copilot is an AI pair-programmer built into your code editor. It suggests whole lines or blocks of code as you type, based on the surrounding context — comments, function names, existing code — and can also answer coding questions through a chat interface.

---

##  Step 1 — Get Access

1. Go to **https://github.com/features/copilot**.
2. Sign in with your GitHub account.
3. Choose a plan:
   - **Copilot Free** — limited monthly completions/chat requests, no cost.
   - **Copilot Pro** — paid, unlimited completions, more chat models. Free for verified students/teachers and popular open-source maintainers.
4. Click **Enable Copilot** (or complete the checkout for Pro) from your GitHub account settings under **Settings → Copilot**.

---

##  Step 2 — Install the Extension in Your Editor

### VS Code

```
1. Open VS Code
2. Go to Extensions (Ctrl+Shift+X)
3. Search "GitHub Copilot"
4. Click Install
5. Also install "GitHub Copilot Chat" for the chat interface
```

### JetBrains IDEs (IntelliJ, PyCharm, etc.)

```
1. Settings → Plugins → Marketplace
2. Search "GitHub Copilot"
3. Click Install → Restart IDE
```

### Neovim

```
1. Install via your plugin manager, e.g. with vim-plug:
   Plug 'github/copilot.vim'
2. Run :PlugInstall
```

---

##  Step 3 — Authenticate

After installing, VS Code (or your IDE) will prompt you to sign in:

```
1. Click "Sign in to GitHub" when prompted (or run the command
   "GitHub Copilot: Sign In" from the Command Palette)
2. A browser window opens — authorize the extension
3. Return to your editor — you should see "Copilot: Ready" in the status bar
```

**Verify from the terminal (optional, if using the CLI extension):**

```bash
abdullah@DevOps:~$ gh auth status
✓ Logged in to github.com as Abdullah
```

---

##  Step 4 — Basic Usage

- Start typing code or a comment describing what you want — Copilot suggests completions in gray/ghost text.
- Press `Tab` to accept a suggestion, `Esc` to dismiss it.
- Use `Alt + ]` / `Alt + [` (Windows/Linux) to cycle through alternative suggestions.
- Open **Copilot Chat** (`Ctrl+Shift+I` in VS Code) to ask questions, request explanations, or generate code from a natural-language prompt.

**Example — writing a comment to trigger a suggestion:**

```python
# Function to check if a number is prime
```
Copilot will typically suggest the full function body below the comment.

---

##  Useful Copilot Features for DevOps Work

| Feature | Use Case |
|---|---|
| Inline completions | Writing Bash scripts, Terraform, Ansible playbooks faster |
| Copilot Chat | "Explain this error", "write a Dockerfile for a Node app" |
| Copilot in the CLI (`gh copilot`) | Suggests/explains terminal commands you're unsure about |

**Copilot CLI example:**

```bash
abdullah@DevOps:~$ gh copilot suggest "find all files larger than 100MB"
```

---

##  Quick Reference

| Action | Shortcut / Command |
|---|---|
| Accept suggestion | `Tab` |
| Dismiss suggestion | `Esc` |
| Next/previous suggestion | `Alt + ]` / `Alt + [` |
| Open Copilot Chat | `Ctrl + Shift + I` (VS Code) |
| Sign in | Command Palette → "GitHub Copilot: Sign In" |
| Check CLI auth status | `gh auth status` |

---

##  Key Takeaways

- Copilot requires a GitHub account plus an active plan (Free or Pro) enabled from GitHub account settings.
- It works as an editor extension (VS Code, JetBrains, Neovim, and more) — install it, then authenticate through the browser.
- `Tab` accepts a suggestion, `Esc` dismisses it — the core interaction loop.
- Copilot Chat is separate from inline completions — useful for asking questions or generating whole files/functions from a prompt.
- For DevOps specifically, it's genuinely useful for scaffolding Bash scripts, Dockerfiles, Terraform/Ansible configs, and explaining unfamiliar commands via `gh copilot suggest`.

---

##  Topics Covered in This Repository (GIT Section)

- [x] Introduction
- [x] Versioning
- [x] Branches & More
- [x] Rollback
- [x] Git SSH Login
- [x] Git Tags, Semantic Versioning & More
- [x] Setup GitHub Copilot
- [ ] Git Commands

---

*Course: DecodingDevOps by Imran Teli (Udemy) | Status: ✅ Completed*
