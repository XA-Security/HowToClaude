# How to Build with Claude — Get Set Up

> Getting started

This is the plain-English checklist of the accounts to create and the tools to install before you sit down with Claude in a terminal window — whatever you're building. No coding experience assumed. Work top to bottom — about 30–40 minutes.

> [!NOTE]
> **The big picture.** You'll talk to Claude in a terminal; it writes and runs the code for you. Five accounts give that work somewhere to live: GitHub stores the project, Anthropic & OpenAI are the AI brains, Vercel puts the app on the web, and Cloudflare handles your domain. Create them in this order — later steps reuse the earlier logins.

---

## Part 1 · The accounts to create

Sign up for these five with the same email. Save every password in a password manager — you'll be asked for them again.

### GitHub

**Free**

**Where your project's code is stored and version-tracked — the 'Google Drive' for the build.**

1. Sign up at [github.com/signup](https://github.com/signup)
2. Verify your email
3. Turn on 2FA via authenticator app: Settings → Password and authentication

> [!CAUTION]
> **Why first:** Vercel and Claude both connect to GitHub, so it needs to exist before the others.

---

### Anthropic API

**Required · Pay-as-you-go**

**This is Claude's brain. The terminal tool bills against this account by usage.**

1. Sign up at [console.anthropic.com](https://console.anthropic.com)
2. Add a credit card in Billing
3. Load $20 starting balance
4. Create an API key named `my-build`
5. Copy the `sk-ant-` key to your password manager **immediately**

> [!CAUTION]
> Treat the key like a credit-card number. Never paste it into an email, a chat, or a webpage. You'll give it to the terminal tool once, privately, in Part 3.

**Why:** Pay per use, cents at a time; set a monthly spend limit.

---

### OpenAI API

**Required · Pay-as-you-go**

**A second AI brain. Some features (images, certain models) work best here — good to have both.**

1. Sign up at [platform.openai.com](https://platform.openai.com)
2. Add a credit card in Billing
3. Load $10–$20 and set a monthly limit
4. Create an API key named `my-build`
5. Copy the `sk-` key to your password manager

> [!CAUTION]
> Same rule: Key is a secret, only typed into project setup.

---

### Vercel

**Free to start**

**Puts your app on the internet at a real web address, automatically, every time you save.**

1. Sign up at [vercel.com/signup](https://vercel.com/signup)
2. Choose "Continue with GitHub" to link accounts
3. Pick Hobby (free) plan

**Why GitHub login:** Vercel watches your GitHub project and re-publishes the site whenever Claude saves a change.

---

### Cloudflare

**When you have a domain**

**Manages your custom web address (e.g. `app.example.com`) and keeps it fast and secure.**

1. Sign up at [dash.cloudflare.com/sign-up](https://dash.cloudflare.com/sign-up)
2. Add a domain if you have one, otherwise skip
3. Connect to Vercel later

**Not urgent:** You only need this once you want a branded address. Everything works on Vercel's free address until then.

---

## Part 2 · Install the tools

### macOS

Four installs. For the first one you'll use the built-in Terminal app — press <kbd>⌘</kbd> <kbd>Space</kbd>, type Terminal, hit Return. After you install VS Code (step 4), you'll do everything from its built-in terminal instead — that's where you'll live from then on. Copy each block below, paste it in, press Return, and wait for it to finish before the next.

#### Install 1 — Homebrew

**Free**

The installer that puts the other tools on your Mac. Paste this, press Return, enter your Mac password if asked.

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

> [!NOTE]
> When it finishes it may print two lines starting with `echo`. Copy and run those too — they let your Mac find Homebrew.

---

#### Install 2 — Node.js

**Free**

The engine modern web apps run on. Claude needs it to build and preview your app.

```bash
brew install node git
```

> [!NOTE]
> This also installs Git, the tool that talks to your GitHub account.

---

#### Install 3 — Claude Code

**The tool itself**

Claude, living in your terminal — it reads, writes, and runs the project for you.

```bash
npm install -g @anthropic-ai/claude-code
```

> [!NOTE]
> The `-g` means 'everywhere on this Mac,' so you can start Claude from any folder.

---

#### Install 4 — VS Code

**Free**

Your workbench — a free editor from Microsoft with a terminal built in. This is where you'll see the project files and talk to Claude, all in one window.

1. Download from [code.visualstudio.com](https://code.visualstudio.com) and drag to Applications
2. Open it and run `Shell Command: Install 'code' command in PATH` via <kbd>⌘</kbd> <kbd>⇧</kbd> <kbd>P</kbd>
3. Open terminal with <kbd>Ctrl</kbd> <kbd>`</kbd> or Terminal → New Terminal

**Why over plain Terminal:** You see your files, your code, and the Claude conversation side by side — far less intimidating than a bare terminal window. Everything in Part 3 happens in VS Code's terminal.

---

### Windows

Four installs. For the first one you'll use Windows Terminal (the modern Windows command line). Open the Start menu, type "Terminal", and hit Return. After you install VS Code (step 4), you'll do everything from its built-in terminal instead — that's where you'll live from then on. Copy each block below, paste it in, press Return, and wait for it to finish before the next.

#### Install 1 — Scoop

**Free**

The installer that puts the other tools on your Windows PC. Paste this into Windows Terminal and press Return.

```powershell
iwr -useb get.scoop.sh | iex
```

> [!NOTE]
> If you see an error about execution policy, run this first:
> ```powershell
> Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
> ```
> Then run the Scoop install command again.

---

#### Install 2 — Node.js

**Free**

The engine modern web apps run on. Claude needs it to build and preview your app.

```powershell
scoop install node git
```

> [!NOTE]
> This also installs Git, the tool that talks to your GitHub account.

---

#### Install 3 — Claude Code

**The tool itself**

Claude, living in your terminal — it reads, writes, and runs the project for you.

```powershell
npm install -g @anthropic-ai/claude-code
```

> [!NOTE]
> The `-g` means 'everywhere on this PC,' so you can start Claude from any folder.

---

#### Install 4 — VS Code

**Free**

Your workbench — a free editor from Microsoft with a terminal built in. This is where you'll see the project files and talk to Claude, all in one window.

1. Download from [code.visualstudio.com](https://code.visualstudio.com) and run the installer
2. Open VS Code and run `Terminal: Create New Terminal` via <kbd>Ctrl</kbd> <kbd>⇧</kbd> <kbd>`</kbd>

**Why over plain PowerShell:** You see your files, your code, and the Claude conversation side by side — far less intimidating than a bare terminal window. Everything in Part 3 happens in VS Code's terminal.

---

## Part 3 · Your first 10 minutes

Tools installed, accounts ready. Everything below happens inside VS Code — open it, then open its terminal with <kbd>Ctrl</kbd> <kbd>`</kbd>.

### Step 1 — Make a home for the project & open it in VS Code

In the VS Code terminal (Terminal → New Terminal), paste these one at a time. This creates a folder and reopens VS Code focused on it.

```bash
# a folder on your Desktop for the build
mkdir -p ~/Desktop/my-project
cd ~/Desktop/my-project
# open this folder in VS Code
code .
```

A fresh VS Code window opens on the project. Open its terminal again with <kbd>Ctrl</kbd> <kbd>`</kbd> — it's already pointed at the right folder.

---

### Step 2 — Start Claude

```bash
claude
```

The first time, it asks how to sign in. Choose the Anthropic API key option and paste the `sk-ant-` key from your password manager. You only do this once — it's stored securely on your Mac.

---

### Step 3 — Give the other keys to the project

Once Claude is open, just tell it in plain English — it will set things up safely for you. For example, type:

```
Create a .env.local file for my OpenAI key and help me
connect this folder to a new GitHub repo and to Vercel.
```

> [!CAUTION]
> **Where keys live:** Secret keys go in a file called `.env.local` that stays on your Mac and is never uploaded. Claude knows this rule — if you ever paste a key in the wrong place, ask it to fix that.

---

### Step 4 — Describe what you want to build

This is the 'vibe' part. Talk to Claude like you'd brief a teammate — what it's for, who uses it, what it should do. The more context, the better the result. For example:

```
Build me a web app for [what it does]. The people using
it are [who]. It should let them [the main things].
Start with a clean dashboard. Walk me through it as you
go since I'm new to this.
```

Claude will build it, show you a live preview, and you refine from there — one plain-English request at a time.

> [!TIP]
> **Two habits that'll save you.**
> 1. When something works, tell Claude 'commit this' — that's a save point you can always return to.
> 2. When you're unsure, just ask: 'what does this do?' or 'is this safe?'. Claude is there to explain, not just execute.

---

## Quick checklist

- [ ] GitHub account created, 2FA on
- [ ] Anthropic API key made + balance loaded + spend limit set
- [ ] OpenAI API key made + balance loaded + spend limit set
- [ ] Vercel signed in via GitHub
- [ ] Cloudflare account (only if you have a domain)
- [ ] Homebrew, Node + Git, and Claude Code installed
- [ ] All keys saved in a password manager — never in email or chat
