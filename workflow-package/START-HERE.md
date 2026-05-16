# Start From Zero

You've never coded before. That's fine — this guide gets you from
nothing to running your first project with a workflow that keeps you
on track.

---

## What is this?

This is a set of files that tell an AI coding tool (Claude Code) how
to help you build software projects the right way. It gives you
structure: what to do first, what to do next, when to stop and
review, and how to pick up where you left off tomorrow.

Think of it like a recipe book for building software — you follow the
steps, and Claude Code does most of the heavy lifting.

---

## What you need to install (do these in order)

### 1. A terminal

A terminal is a text-based window where you type commands. Every
computer has one built in.

**Windows:** Press the Windows key, type "PowerShell", click
"Windows PowerShell". That's your terminal.

**Mac:** Press Cmd+Space, type "Terminal", hit Enter. That's your
terminal.

You'll type commands into this window for the next steps.

### 2. Git

Git tracks changes to your files — like "undo history" that never
runs out and works across sessions.

**Windows:** Download from https://git-scm.com/download/win and run
the installer. Accept all defaults.

**Mac:** Open your terminal and type `git --version`. If it asks you
to install developer tools, say yes.

**Verify it worked:** In your terminal, type:
```
git --version
```
You should see a version number. If you see an error, the install
didn't work — try again.

### 3. Claude Code

Claude Code is the AI tool that reads your workflow files and helps
you build things.

**Install it:** Open your terminal and type:
```
npm install -g @anthropic-ai/claude-code
```

If that gives an error about "npm not found", you need Node.js first:
- Download from https://nodejs.org (pick the LTS version)
- Install it, then close and reopen your terminal
- Try the `npm install` command again

**Verify it worked:** In your terminal, type:
```
claude --version
```
You should see a version number.

### 4. A code editor (optional but recommended)

You can use any text editor, but VS Code is free and works well:
- Download from https://code.visualstudio.com
- Install the Claude Code extension from the Extensions tab

---

## Setting up the workflow (one time)

Once you have Git and Claude Code installed, do this once:

### Step 1: Download the workflow files

In your terminal:

**Windows (PowerShell):**
```
git clone https://github.com/MsShawnP/claude-solo-dev-workflow.git "$env:USERPROFILE\projects\reference\claude-solo-dev-workflow"
```

**Mac/Linux:**
```
git clone https://github.com/MsShawnP/claude-solo-dev-workflow.git ~/projects/reference/claude-solo-dev-workflow
```

### Step 2: Copy the commands into Claude Code

**Windows (PowerShell):**
```
New-Item -ItemType Directory -Force "$env:USERPROFILE\.claude\commands"
Copy-Item "$env:USERPROFILE\projects\reference\claude-solo-dev-workflow\workflow-package\slash-commands\*.md" "$env:USERPROFILE\.claude\commands\"
```

**Mac/Linux:**
```
mkdir -p ~/.claude/commands
cp ~/projects/reference/claude-solo-dev-workflow/workflow-package/slash-commands/*.md ~/.claude/commands/
```

### Step 3: Verify it worked

Open your terminal, navigate to any folder, and type:
```
claude
```

Once Claude Code opens, type `/commands`. If you see a list of
workflow commands, you're set up correctly.

---

## Starting your first project

1. Create a folder for your project:

   **Windows:**
   ```
   New-Item -ItemType Directory "$env:USERPROFILE\projects\my-first-project"
   Set-Location "$env:USERPROFILE\projects\my-first-project"
   git init
   ```

   **Mac/Linux:**
   ```
   mkdir -p ~/projects/my-first-project
   cd ~/projects/my-first-project
   git init
   ```

2. Open Claude Code in that folder:
   ```
   claude
   ```

3. Type this to set up your project:
   ```
   /init My First Project | What am I building and why?
   ```

4. Claude will create your project files and tell you exactly what
   to do next. Follow the steps it gives you.

---

## The commands you'll use most

You don't need to memorize these — Claude will suggest them at the
right time. But here's what they do:

| Command | When to use it | What it does |
|---------|---------------|--------------|
| `/log` | After you finish something | Saves a checkpoint so you don't lose progress |
| `/wrap` | When you're done for the day | Captures everything so tomorrow's session starts where you left off |
| `/commands` | When you forget what's available | Shows the full list |

---

## If you get stuck

- Type `/commands` to see what's available
- Ask Claude "what should I do next?" — it reads your project files
  and will tell you
- If something breaks, tell Claude what happened. It will help you
  fix it.

---

## Glossary

Terms you'll see in this workflow:

| Term | What it means |
|------|---------------|
| **Terminal** | The text window where you type commands |
| **Repository (repo)** | A project folder tracked by git |
| **Clone** | Download a copy of a project |
| **Commit** | Save a snapshot of your changes |
| **Slash command** | A shortcut that starts with `/` — type it in Claude Code to run it |
| **Session** | One sitting of work with Claude Code (from opening it to closing it) |
| **Arc** | A chunk of work with a clear goal — bigger than a task, smaller than the whole project |
