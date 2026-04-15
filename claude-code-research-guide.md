# Claude Code for Research - Implementation Guide
### Energy Economics & Quantitative Research
**SMS | Riyadh,  2026**

*Based on: Korinek, A. (2025). AI Agents for Economic Research. NBER Working Paper No. 34202.
AI MBA Webinar Series on Claude Code for Economists (Panjwani, 2025).
Karpathy, A. (2026). LLM Knowledge Bases. 
Phelan, A. (2023). An Updated Academic Workflow: Zotero & Obsidian. Medium.*

---

## Table of Contents

1. [Overview & Philosophy](#1-overview--philosophy)
2. [Installing VSCode](#2-installing-vscode)
3. [Authentication & Initial Setup for Claude Code](#3-authentication--initial-setup-for-claude-code)
4. [Project Folder Structure](#4-project-folder-structure)
5. [Git & GitHub Integration](#5-git--github-integration)
6. [Settings Architecture & Permissions](#6-settings-architecture--permissions)
7. [Context Engineering](#7-context-engineering)
8. [Key Commands Quick Reference](#8-key-commands-quick-reference)
9. [Plan Mode for Complex Research Tasks](#9-plan-mode-for-complex-research-tasks)
10. [Reproducible Data Management](#10-reproducible-data-management)
11. [Publication-Quality Figures: Healy Style Guide](#11-publication-quality-figures-healy-style-guide)
12. [Subagents: Specialised AI Teammates](#12-subagents-specialised-ai-teammates)
13. [Installing Third-Party Agents](#13-installing-third-party-agents)
14. [The Knowledge Management Stack: Zotero, Obsidian, NotebookLM & Claude Code](#14-the-knowledge-management-stack-zotero-obsidian-notebooklm--claude-code)
15. [AI Paradigms for Research (Korinek, 2025)](#15-ai-paradigms-for-research-korinek-2025)
16. [Critical Limitations & Responsible Oversight](#16-critical-limitations--responsible-oversight)
17. [Best Practices Summary](#17-best-practices-summary)
18. [Troubleshooting](#18-troubleshooting)

---

## 1. Overview & Philosophy

Claude Code is Anthropic's agentic coding interface, designed to operate as a genuine research collaborator — not just a code generator. When used well, it can manage your entire project lifecycle: from project scaffolding and literature data ingestion, to running simulations, producing publication-quality figures, and drafting LaTeX. This guide translates hands-on experience into structured workflows specifically tuned for energy economics research.

> **INFO:** The single most important habit: start every session with a plan, keep sessions short and focused (5–10 turns), and commit progress frequently to Git.

### 1.1 Core Operational Principles

The way most researchers interact with AI — asking a one-off question, reading the answer, and closing the tab — captures only a fraction of what is possible. Claude Code is fundamentally different because it operates inside your actual file system. It can read your data, write and execute code, navigate your project folder, and produce outputs that persist between sessions. To take full advantage of this, a small number of habits matter enormously. Internalising these principles early will prevent the most common failure modes — sessions that drift off-task, outputs that cannot be reproduced, and projects where nobody (human or AI) knows what was decided and why.

- Treat Claude Code as a senior research assistant that needs clear context and goals at the start of each session.
- Use short, focused sessions rather than long, sprawling conversations — context degrades over time.
- Always version-control your work: Claude Code and Git are inseparable in a professional workflow.
- Separate concerns into folders: `data/`, `code/`, `outputs/`, `review/`, and `latex/`.
- Persist decisions in files (`plan.md`, `progress.md`, `CLAUDE.md`) rather than relying on session memory.

### 1.2 The Research Stack This Guide Covers

This guide covers a full researcher's software stack, from writing environment to knowledge management to agentic coding. Each tool in the stack serves a distinct role, and they are designed to work together. You do not need to adopt all of them at once — most researchers start with VSCode and Claude Code, then add Git, then gradually build the knowledge management layer as their needs grow.

| Tool | Role in the Stack |
|---|---|
| **VSCode** | Primary development environment — where you write code, run terminals, and use the Claude Code extension |
| **Claude Code** | Agentic AI collaborator — reads/writes files, runs code, manages your project |
| **Zotero** | Reference manager — collects papers, generates citekeys, stores PDF annotations |
| **Obsidian** | Knowledge IDE — markdown vault where your wiki lives, viewed as a graph |
| **NotebookLM** | Synthesis engine — ingests many sources at once, produces structured summaries |
| **Git / GitHub** | Version control and collaboration backbone |
| **Overleaf** | LaTeX paper writing, synced back via Git |

---

## 2. Installing VSCode

Visual Studio Code (VSCode) is a free, open-source code editor built by Microsoft. It serves as the recommended environment for working with Claude Code because it combines a code editor, an integrated terminal, a file explorer, and a Git interface all in one window. For researchers, this means you can write Python scripts, inspect data files, run Claude Code sessions, and commit your work to GitHub without switching between applications. VSCode is also highly extensible — a large ecosystem of plugins covers everything from Python linting to LaTeX compilation to Jupyter notebooks.

### 2.1 System Requirements

Before downloading, verify that your machine meets the minimum requirements. VSCode is lightweight and runs on almost any modern computer, but the integrated terminal and extensions do benefit from adequate memory — especially when running Python data analysis or LaTeX compilation alongside the Claude Code session.

| Platform | Minimum Requirement |
|---|---|
| Windows | Windows 10 or later (64-bit) |
| macOS | macOS 10.15 (Catalina) or later |
| Linux | Ubuntu 18.04, Debian 10, Fedora 34, or equivalent |
| RAM | 4 GB minimum; 8 GB recommended |
| Disk | 500 MB free space |

### 2.2 Download and Install

**Step 1 — Download the installer.**

Visit the official VSCode download page: [https://code.visualstudio.com/download](https://code.visualstudio.com/download). Always download from the official Microsoft site to ensure you receive the genuine, unmodified package. Select the installer for your operating system.

**Step 2 — Run the installer.**

Follow the platform-specific instructions below.

#### Windows

1. Run the downloaded `.exe` installer (e.g., `VSCodeUserSetup-x64-1.xx.x.exe`).
2. Accept the license agreement.
3. On the "Select Additional Tasks" screen, check the following options for a better experience:
   - ✅ Add "Open with Code" action to Windows Explorer file context menu
   - ✅ Add "Open with Code" action to Windows Explorer directory context menu
   - ✅ Add to PATH (important — required for Claude Code's terminal integration)
4. Click **Install**, then **Finish**. VSCode will open automatically.

> **TIP:** After installation, open a new terminal (Command Prompt, PowerShell, or Git Bash) and type `code --version` to verify VSCode is on your PATH. If the command is not found, you will need to restart your computer for the PATH change to take effect.

#### macOS

1. Open the downloaded `.zip` archive. This extracts `Visual Studio Code.app`.
2. Drag `Visual Studio Code.app` to your **Applications** folder.
3. Open VSCode from Applications.
4. To add the `code` command to your terminal PATH: open VSCode, press `Cmd+Shift+P`, type **Shell Command: Install 'code' command in PATH**, and press Enter. This allows you to type `code .` in any terminal to open the current folder directly in VSCode — a habit that becomes very useful when working with Claude Code.

> **TIP:** If macOS blocks the app with an "unidentified developer" warning, go to System Settings → Privacy & Security → scroll to the bottom and click **Open Anyway**.

#### Linux (Ubuntu/Debian)

On Linux, the cleanest installation method uses the official Microsoft package repository, which also enables automatic updates via `apt`.

```bash
# Import Microsoft's GPG key
wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg
sudo install -D -o root -g root -m 644 packages.microsoft.gpg /etc/apt/keyrings/packages.microsoft.gpg

# Add the VSCode repository
sudo sh -c 'echo "deb [arch=amd64,arm64,armhf signed-by=/etc/apt/keyrings/packages.microsoft.gpg] \
  https://packages.microsoft.com/repos/code stable main" > /etc/apt/sources.list.d/vscode.list'

# Install VSCode
sudo apt-get update
sudo apt-get install code
```

Verify the installation by running `code --version` in your terminal.

### 2.3 Essential VSCode Settings for Research

Out of the box, VSCode works well, but a few configuration changes make it significantly better suited for research work. The most important of these is setting Git Bash as the default terminal on Windows — without this, Claude Code will fail to run because it requires a Unix-compatible shell. The other settings improve the editing experience: word wrap prevents long markdown lines from disappearing off-screen, and auto-save means you never lose work if Claude Code runs a script that modifies a file you have open.

Open the Settings editor with `Ctrl+,` (Windows/Linux) or `Cmd+,` (macOS), or press `Ctrl+Shift+P` → **Preferences: Open Settings (JSON)** to edit the JSON file directly.

```json
{
  "editor.wordWrap": "on",
  "editor.lineNumbers": "on",
  "editor.renderWhitespace": "boundary",
  "files.autoSave": "afterDelay",
  "files.autoSaveDelay": 1000,
  "terminal.integrated.defaultProfile.windows": "Git Bash",
  "terminal.integrated.defaultProfile.osx": "zsh",
  "git.autofetch": true,
  "git.confirmSync": false,
  "workbench.editor.enablePreview": false
}
```

> **TIP:** If Git Bash is not installed on Windows, download it from [gitforwindows.org](https://gitforwindows.org/) before proceeding. Git Bash provides the Unix-style terminal that Claude Code, npm, and other tools require.

### 2.4 Recommended Extensions for Researchers

VSCode's extension marketplace is one of its greatest strengths. Extensions add language support, preview capabilities, and tool integrations that would otherwise require separate applications. For an energy economics researcher, the most valuable extensions cover Python (your main analysis language), Jupyter notebooks, Git history visualisation, markdown editing, and LaTeX. The Claude Code extension is the most critical — it embeds the Claude Code interface directly inside VSCode so you never need to switch to a separate terminal window.

Install extensions from the Extensions panel (`Ctrl+Shift+X`): click the Extensions icon in the left sidebar, search by name, and click **Install**.

| Extension | Purpose |
|---|---|
| **Claude Code** (by Anthropic) | Embeds the Claude Code agentic assistant directly inside VSCode |
| **Python** (by Microsoft) | Python language support, linting, debugging, and Jupyter integration |
| **Jupyter** (by Microsoft) | Run and edit `.ipynb` notebooks directly inside VSCode |
| **GitLens** | Visualises Git history, blame annotations, and branch comparisons inline in the editor |
| **Markdown All in One** | Live preview, keyboard shortcuts, and automatic TOC generation for `.md` files |
| **LaTeX Workshop** | Compile and preview LaTeX documents without leaving VSCode |
| **Rainbow CSV** | Colour-highlights `.csv` columns and allows SQL-style queries — invaluable when inspecting data |

### 2.5 Opening a Research Project in VSCode

This step is simple but often misunderstood by new users. The correct way to open a project is to open the **folder**, not an individual file. When VSCode opens a folder, it sees the entire project structure — the same view that Claude Code needs to navigate your files, read your CLAUDE.md, and execute scripts correctly. Opening only a single `.py` or `.md` file gives Claude Code no visibility into your project layout and will break many workflows.

```bash
# Option 1: from any terminal (recommended)
cd /path/to/your/project
code .

# Option 2: from within VSCode
# File → Open Folder → navigate to your project folder → OK
```

> **WARNING:** Never open VSCode by double-clicking individual files from File Explorer or Finder. Always open the project folder. Claude Code cannot read your project structure if only a single file is open.

---

## 3. Authentication & Initial Setup for Claude Code

With VSCode installed, the next step is to install and authenticate Claude Code itself. Claude Code runs as a command-line tool that you interact with through the integrated terminal in VSCode. Authentication connects Claude Code to your Anthropic account, which provides access to the underlying language model and tracks your API usage. This section walks through installation, authentication, and the cost-monitoring commands you should use from day one.

### 3.1 Prerequisites

Claude Code is distributed as an npm package, which means it requires Node.js to run. Node.js is a JavaScript runtime that many development tools use as their execution environment. If you have never used npm before, think of it as an app store for command-line developer tools. You will also need an Anthropic account to authenticate.

Before installing Claude Code, ensure you have:

1. **Node.js** (version 18 or higher). Download from [nodejs.org](https://nodejs.org/). After installation, verify with `node --version`.
2. **npm** (comes bundled with Node.js). Verify with `npm --version`.
3. An **Anthropic account** at [claude.ai](https://claude.ai), or an API key from [console.anthropic.com](https://console.anthropic.com).

### 3.2 Installation

Installing Claude Code globally via npm makes the `claude` command available in any terminal on your computer, regardless of which project folder you are in. The `--version` command after installation confirms that the tool is correctly on your PATH.

```bash
npm install -g @anthropic-ai/claude-code
claude --version    # verify installation
```

#### Installing the VSCode Extension

The VSCode extension is a companion interface that lets you run Claude Code sessions directly inside the editor, without switching to a separate terminal window. It also provides a cleaner display for long responses and makes it easier to review Claude's file edits before accepting them.

1. Open VSCode. Go to the Extensions panel (`Ctrl+Shift+X`).
2. Search for **Claude Code** and install the extension by Anthropic.
3. Open the Claude Code panel: `Ctrl+Shift+P` → *Claude Code: Open*.

> **TIP:** On Windows, set Git Bash or WSL as the default terminal in VSCode (Settings → Terminal → Default Profile) before opening Claude Code. The extension requires a Unix-compatible shell.

### 3.3 Authentication

Authentication links your Claude Code installation to your Anthropic account. The `auth login` command opens a browser window where you authorise the connection using the same credentials you use on claude.ai. Once authenticated, your session persists until you explicitly log out. The `auth status` command is useful for confirming that your session is still active at the start of a new working day.

```bash
claude auth login     # opens browser for OAuth
claude auth status    # confirm session is active
```

> **INFO:** For CI/CD pipelines or remote servers (e.g., a university HPC cluster), browser-based login is not possible. In those environments, create an API key at console.anthropic.com and set it as the environment variable `ANTHROPIC_API_KEY`. Claude Code will detect it automatically.

### 3.4 Monitoring API Usage & Costs

Because Claude Code bills by the token — roughly corresponding to words processed — it is easy to inadvertently run up a large bill during long or data-heavy sessions. Monitoring usage is not just a cost concern: it also helps you understand which operations consume the most context, which in turn helps you design more efficient workflows. The commands below should become a routine part of your session management.

| Command | Purpose |
|---|---|
| `/usage` | Show total token usage for the current session |
| `ccusage` | Extended usage report across sessions |
| `session/cost` | Estimate monetary cost of the current session |

> **WARNING:** Loading large files directly into context (e.g., a 10 MB CSV) can consume tokens extremely quickly. Always check `/usage` before and after major operations, and use `/compact` to summarise the conversation history when the context grows long.

---

## 4. Project Folder Structure

One of the most consequential decisions you make when starting a research project with Claude Code is how you organise your files. A well-designed folder structure serves two purposes simultaneously: it keeps your project legible to collaborators and future-you, and it gives Claude Code a consistent, predictable layout to navigate. When Claude knows that all raw data lives in `data/raw/` and all figure scripts live in `code/figures/`, it can find and modify the right files without lengthy instructions every session. The structure below reflects common practice in computational economics research and is designed to separate the concerns of data, code, outputs, and writing into distinct, non-overlapping areas.

```
my-project/
├── CLAUDE.md              ← Project instructions for Claude
├── plan.md               ← Session planning document
├── progress.md           ← Running log of completed tasks
├── .gitignore
├── .claude/
│   ├── settings.json     ← Claude Code permissions & MCP
│   ├── settings.local.json  ← Local overrides (gitignored)
│   └── agents/           ← Custom subagent definitions
│       ├── data-auditor.md
│       ├── lit-reviewer.md
│       └── data-fetcher.md
├── data/
│   ├── raw/              ← Downloaded, never modified
│   ├── processed/        ← Cleaned and transformed
│   └── download_data.py  ← Reproducible data fetching
├── code/
│   ├── simulation/       ← Main model code
│   ├── analysis/         ← Post-processing and statistics
│   └── figures/          ← Figure generation scripts
├── outputs/
│   ├── figures/          ← Final figures (.pdf, .svg)
│   └── tables/           ← LaTeX tables
├── review/               ← Peer review notes, responses
└── latex/                ← Paper source (Overleaf sync)
```

### 4.1 Initialising a New Project

Rather than creating this folder structure manually, you can ask Claude Code to scaffold it for you with the `/init` command. This command reads your current directory, generates a `CLAUDE.md` file pre-populated with basic project information, and creates the standard folder layout. Running it at the very start of a project ensures that Claude has a proper context file from session one.

```bash
claude /init    # generates CLAUDE.md and scaffolds project
```

### 4.2 Example CLAUDE.md for Research

`CLAUDE.md` is arguably the most important file in your project. It is the document that Claude Code reads at the start of every session to understand who you are, what the project is about, what files exist, and what work is in progress. Think of it as a standing briefing document for a research assistant who starts each day with no memory of the previous one. The more clearly and specifically you write it, the less time you spend re-explaining context at the start of each session. Update it whenever you make a significant structural decision — new data source, change of model specification, shift in target journal — because these are exactly the things Claude Code needs to know to give you useful help.

```markdown
# Project: [Your Paper Title]

## Objective
Analyse [research question] targeting [target journal]

## Key Files
- code/simulation/main_model.py  ← Main simulation
- data/raw/source_data.csv       ← Primary data source
- latex/main.tex                 ← Paper source

## Data Sources
- [Primary source]: [description]
- [Secondary source]: [description]

## Current Status
- [Key model assumption] formalised
- Simulation: [N]-run calibration complete
- Pending: [Next task]

## Co-Authors
- [Co-author A]: [area of responsibility]
- [Co-author B]: [area of responsibility]
```

### 4.3 Where to Put CLAUDE.md, plan.md, and progress.md

These three files work together as Claude Code's external memory system. `CLAUDE.md` provides stable project context that changes infrequently. `plan.md` provides session-by-session instructions that tell Claude exactly what to do in the current session. `progress.md` provides a running history of what has been done, what was discovered, and what remains — the equivalent of a lab notebook. Placing them correctly is essential: Claude Code's automatic file-loading only works from the project root.

| File | Location & Purpose |
|---|---|
| `CLAUDE.md` | Project root — auto-read by Claude Code every session. Provides stable project context. |
| `plan.md` | Project root — referenced at session start. Contains today's specific goals and steps. |
| `progress.md` | Project root — running audit trail. Updated at the end of every session. |
| `.claude/settings.json` | Auto-created by Claude Code — permissions and MCP server configuration. |
| `.claude/settings.local.json` | Machine-specific overrides — must be added to `.gitignore`. |

> **WARNING:** `CLAUDE.md` must stay in the project root. Claude Code's automatic project-context loading only searches for it there. A misplaced `CLAUDE.md` means every session starts without project context, and you will end up re-explaining the same background repeatedly.

---

## 5. Git & GitHub Integration

Version control is not optional when working with Claude Code — it is a safety net. Because Claude Code can read, write, and delete files autonomously across a session, the only reliable way to undo an unexpected change is to roll back to a previous Git commit. Beyond safety, Git provides a precise audit trail of every analytical decision: when a model specification changed, when a data source was added, when a figure was revised. For collaborative research, it also allows co-authors to work on the same codebase without overwriting each other's work. If you have never used Git before, the workflow described here is the minimum you need for safe use of Claude Code.

### 5.1 Connecting to GitHub

The initial setup links your local project folder to a remote repository on GitHub. The remote acts as both a backup and a collaboration point. Running `git pull origin main` at the start of every session ensures you are always working from the latest version, which is especially important if you work across multiple computers or with co-authors.

```bash
git init
git remote add origin https://github.com/yourusername/your-project.git
git branch -M main
git push -u origin main
git pull origin main   # run at start of every session
```

### 5.2 Git Workflow for Research Sessions

The discipline of committing after every Claude Code session — rather than at the end of the week — pays dividends when something goes wrong. A focused, well-described commit message also serves as documentation: reading through your commit history should tell the story of how the paper developed. The prefixes in the table below are borrowed from software engineering conventions and make it easy to scan which type of work happened in each commit.

```bash
git add -A
git commit -m "feat: calibrate simulation parameters to source data"
git push origin main
```

| Prefix | Use Case |
|---|---|
| `feat:` | New analysis component |
| `fix:` | Correcting a bug or model error |
| `data:` | Adding or updating data files |
| `fig:` | New or revised figure |
| `latex:` | Changes to paper source files |
| `docs:` | Updates to CLAUDE.md, plan.md, README |

### 5.3 Overleaf Integration: Connecting Your Paper

Overleaf is the standard LaTeX writing environment for academic collaboration, but its interface is separate from your code and data. Connecting Overleaf to GitHub via a Git subtree closes this gap: you can push Claude Code's LaTeX edits directly to Overleaf and pull co-author changes back into your local repository. The subtree approach keeps the LaTeX files nested under a `latex/` subfolder in your main project repository, so everything — data, code, and paper — lives in one version-controlled place.

Set it up once, then maintain it with a consistent pull/push rhythm each session.

#### Step 1: Create GitHub Repo from Overleaf

In Overleaf: *Menu* → *GitHub* → *Create a GitHub repository*. This creates a dedicated GitHub repository that Overleaf will sync with.

#### Step 2: Add as Git Subtree

```bash
git remote add overleaf https://github.com/yourusername/paper-repo.git
git subtree add --prefix=latex overleaf main --squash
```

#### Session Rhythm with Overleaf

The key discipline here is always pulling before pushing. If a co-author made changes in Overleaf since your last session and you push without pulling first, you will create a merge conflict that is tedious to resolve.

| # | Step | Command |
|---|---|---|
| 1 | Pull paper from Overleaf | `git subtree pull --prefix=latex overleaf main --squash` |
| 2 | Pull project from GitHub | `git pull origin main` |
| 3 | Run Claude Code session | `claude` |
| 4 | Commit all changes | `git add -A && git commit` |
| 5 | Push project to GitHub | `git push origin main` |
| 6 | Push paper to Overleaf | `git subtree push --prefix=latex overleaf main` |

> **WARNING:** Always pull from Overleaf before pushing back. Never push without pulling first — doing so with co-author edits pending will cause a merge conflict.

---

## 6. Settings Architecture & Permissions

Claude Code is a powerful tool with the ability to run shell commands, modify files, and connect to external services. The settings system exists to give you fine-grained control over what Claude is and is not allowed to do in your project. This matters for two reasons: security (you do not want Claude deleting important files without confirmation) and reproducibility (you want the same permissions to apply whether you are working on your laptop, a co-author's machine, or a remote server). The hierarchical settings system allows you to set broad rules at the user level and narrow, project-specific rules at the project level.

### 6.1 Settings Hierarchy

Settings are layered, with lower levels overriding higher ones. Organisation-level settings (relevant for enterprise users) cascade down to user settings, which cascade to project settings, which cascade to local settings. For most individual researchers, only the user and project levels matter.

| Level | File & Scope |
|---|---|
| Organization | Managed by Anthropic / enterprise admin |
| User | `~/.claude/settings.json` — applies across all your projects |
| Project | `.claude/settings.json` — committed to Git and shared with collaborators |
| Local | `.claude/settings.local.json` — machine-specific overrides, never committed |

### 5.2 Tool-Based Access Controls

The permissions block in your settings file is where you define what Claude Code is allowed to do without asking, what it should ask confirmation for, and what it must never do. For a research project, a sensible default is to allow routine operations (running Python scripts, using Git, fetching data from approved sources) and to require confirmation for anything irreversible (deleting files, running arbitrary network requests). The example below is calibrated for energy economics data workflows, where fetching data from EIA or national regulators is routine but unrestricted `sudo` commands would be dangerous.

```json
{
  "permissions": {
    "allow": [
      "Bash(git:*)",
      "Bash(python:*)",
      "WebFetch(domain:eia.gov)",
      "WebFetch(domain:your-data-portal.gov)",
      "mcp__scholargateway__*"
    ],
    "ask": ["Bash(rm:*)", "Bash(curl:*)"],
    "deny": ["Bash(sudo:*)", "WebFetch(domain:*)"]
  }
}
```

### 6.3 MCP Server Configuration

MCP (Model Context Protocol) servers extend Claude Code's capabilities beyond the local file system by giving it access to external tools and services. Each MCP server is effectively a plugin: once configured, Claude Code can call it just as it would call a local shell command. For researchers, the most valuable MCP integrations connect Claude directly to the tools you already use — Zotero for references, Scholar Gateway for paper search, GitHub for repository management, and Overleaf for LaTeX. Rather than copying and pasting between applications, you instruct Claude Code to query or update them directly as part of a larger workflow.

| MCP Server | Capability for Research |
|---|---|
| Scholar Gateway | Academic paper search, abstract retrieval |
| Zotero | Reference management from within Claude |
| Overleaf | Read and write LaTeX files directly |
| NotebookLM | Research notebooks from session outputs |
| Gmail / Calendar | Referee response emails, revision deadlines |
| GitHub | Branches, PRs, issues without leaving terminal |

```json
"mcpServers": {
  "scholargateway": {
    "url": "https://connector.scholargateway.ai/mcp"
  },
  "zotero": {
    "command": "npx",
    "args": ["-y", "@zotero/mcp-server"],
    "env": { "ZOTERO_API_KEY": "${ZOTERO_KEY}" }
  }
}
```

### 6.4 Installing Third-Party MCP Servers

MCP servers are published by third-party developers and installed in the same way as other software packages. The transport method depends on how the server is distributed. Remote URL-based servers require only a URL — Claude Code connects to them over the network. npm-based servers run locally via the `npx` command. Python-based servers use `uvx` or a similar Python runner. Before installing any MCP server from an unfamiliar source, it is worth reading its README carefully to understand exactly what permissions it requests and what operations it will perform on your behalf.

| Transport | Configuration |
|---|---|
| URL / SSE (remote) | Provide `url` field only |
| npx (npm package) | Use `command: npx` with `args: ["-y", "@pkg/name"]` |
| Python / uvx | Use `command: uvx` or `python -m package` |

> **WARNING:** Before installing any third-party MCP server: check recent commits to verify the project is actively maintained, read the README to understand the tool scope, and never grant broader permissions than the server actually needs. A server that can run Bash commands has significant access to your system.

---

## 7. Context Engineering

Context engineering is one of the most underappreciated skills in working with AI tools. Every Claude Code session operates within a fixed context window — a limit on how much text (instructions, file contents, conversation history, and outputs) can be held in memory at once. As a session grows longer, older content is pushed out of the window, which means Claude may "forget" decisions made earlier in the conversation. Understanding how to manage this window deliberately — keeping it focused, compacting it when it fills up, and persisting important decisions in files rather than relying on the conversation — is what separates researchers who get consistent, high-quality results from those who get increasingly confused responses as a session progresses.

### 7.1 The 5–10 Turn Session Rule

The most effective way to maintain context quality is simply to keep sessions short and tightly scoped. Each session should have one goal — not five. If you start a session intending to clean the data and also update the figures and also revise the introduction, you will likely end up with a degraded conversation where Claude has lost track of constraints established early on. A short, focused session with a clear goal, executed well, is far more productive than a long session that tries to do everything at once. When a session reaches around ten meaningful exchanges, consider whether a new session would serve you better.

Limit each session to a single, well-defined task. Never run data cleaning, simulation, and LaTeX tasks in the same conversation — context contamination degrades all three.

### 7.2 Compacting Context

The `/compact` command instructs Claude Code to summarise the conversation history up to the current point and replace it with a compressed version, freeing up space in the context window for further work. This is useful when a session has been running for a while and you want to continue working without starting over. The key discipline is to run it *proactively* — after completing a major task but while the session is still coherent — rather than waiting until the context is already overloaded and responses have started to degrade.

```
/compact
```

Run proactively after completing a major task, not reactively when context is already overloaded.

### 7.3 plan.md and progress.md — Your External Memory

Because Claude Code starts each session without memory of previous sessions, you need a system for carrying important information forward. The `plan.md` and `progress.md` files serve this purpose. Rather than re-explaining your project at the start of every session, you write the context into these files once and reference them in your opening prompt. Over time, this pair of files becomes an invaluable research journal: a record of every analytical decision, every unexpected finding, and every task that remains.

#### plan.md — The Session Blueprint

The plan.md file is written *before* each session and read by Claude at the start. Its purpose is to eliminate ambiguity about what the session is for. A well-written plan means Claude can start working productively immediately, without needing to ask clarifying questions. The table below describes the five components that every plan should include.

| Component | What to Write and Why |
|---|---|
| Date and session title | Cross-reference with progress.md and Git commits |
| Single clear goal | One sentence. If you cannot state it in one sentence, split the session. |
| Numbered steps | Exact sequence of actions for Claude |
| Do NOT list | Files not to touch, analyses not to run — prevents accidental scope creep |
| Success criteria | Specific output files, tests, or benchmarks that signal completion |

#### plan.md Template

```markdown
# Session Plan: YYYY-MM-DD - [Session title]

## Goal
[Single sentence: what does success look like?]

## Context
[1-3 sentences: what happened last session?]

## Steps
1. [First concrete action with file paths]
2. [Second action]
3. [...]

## Do NOT
- [File not to touch]
- [Do not commit until: condition]

## Success Criteria
- [ ] [Specific output exists at specific path]
- [ ] progress.md updated and committed
```

#### Opening a Session

Use this standard opening prompt at the start of every session. Asking Claude to explicitly confirm its understanding before beginning ensures it has actually read all three files and has a coherent picture of the project state.

```
Please read CLAUDE.md, plan.md, and progress.md in that order.
Then confirm your understanding of today's goal and begin Step 1.
```

#### progress.md — The Persistent Audit Trail

The progress.md file is written *after* each session, summarising what was accomplished, what was discovered, and what remains. It serves two audiences: future-you, who will read it at the start of the next session to get back up to speed quickly, and Claude, who reads it as part of its opening context. A well-maintained progress log also serves as a research journal that can inform a methods section or a response to referees. Rather than writing it manually, ask Claude to draft a progress.md entry before closing each session — then review, edit, and commit.

```markdown
# Progress Log

---

## YYYY-MM-DD - [Session title]

### Completed
- [Step with specific numbers, file paths, test results]

### Discoveries and Decisions
- [Unexpected finding]
- [Decision made and brief rationale]

### Pending
- [Step not completed and why]

### Files Changed
- [file path] - [what changed]

### Git Commit
[commit message]
```

> **TIP:** Ask Claude to draft the progress.md entry before closing: *"Before we finish: please draft a progress.md entry for today's session."* Review, edit, append, and commit.

---

## 8. Key Commands Quick Reference

Claude Code has a set of slash commands and keyboard shortcuts that control the session itself — distinct from the natural language instructions you give it as prompts. Knowing these commands well helps you manage long or complex sessions efficiently. The most important in practice are `/compact` (to free up context window space), `/status` (to check the health of your MCP connections), and `/agents` (to manage your custom subagents). The keyboard shortcuts `Ctrl+B` (background) and `Ctrl+O` (show tool calls) are particularly useful during long-running agentic tasks.

| Command | Description |
|---|---|
| `/init` | Generate CLAUDE.md and scaffold the project |
| `/usage` | Token usage for current session |
| `/status` | Session state, context window, MCP connections |
| `/compact` | Summarise and compress conversation history |
| `/clear` | Clear conversation history (fresh start) |
| `/export` | Export conversation to file |
| `/agents` | Manage and create subagents |
| `/btw` | Ask a parallel question without losing main context |
| `/voice` | Enable voice input |
| `Ctrl+C` | Quit the current Claude Code process |
| `Ctrl+O` | Show recent actions and tool calls |
| `Ctrl+B` | Send current agent to background |

---

## 9. Plan Mode for Complex Research Tasks

For straightforward tasks — run this script, fix this bug, generate this figure — you can simply describe what you want and Claude Code will proceed. For complex, multi-step research tasks, however, jumping straight to execution without a shared understanding of the plan is a common source of expensive mistakes. Plan Mode is the practice of asking Claude to think through a task and produce a detailed execution plan *before* writing a single line of code. Reviewing the plan gives you the opportunity to catch misunderstood requirements, incorrect assumptions about data formats, or steps in the wrong order — when the cost of correction is a few words of feedback, not an hour of debugging.

1. Open a fresh session and describe the task at a high level.
2. Ask Claude to produce a step-by-step plan *without executing* any steps yet.
3. Review the plan, correct misconceptions, add constraints.
4. Save the agreed plan to `plan.md`.
5. Start a new focused session referencing `plan.md` to execute.

```
I need to build a [model type] for [research question].
Before writing any code, produce a detailed execution plan
covering: data sources, model structure, parameter calibration,
and output format. Do not write code yet -- just the plan.
```

---

## 10. Reproducible Data Management

Reproducibility is a fundamental requirement of scientific research — and it is also one of the most common sources of failure in computational economics projects. The problem typically looks like this: a paper is under revision, a referee asks you to extend the sample, and you realise you cannot remember exactly which version of the data you used, from which source, downloaded on which date. The solution is to never work directly with raw data files, and to always manage data acquisition through a script that records the source URL, the download timestamp, and the exact parameters of the query. Claude Code can both write and execute these scripts, and because they live under version control, every historical version of your data is traceable.

### 10.1 The Data Download Script Pattern

The pattern below separates the act of downloading data from the act of processing it. The `data/raw/` folder contains only unmodified source files, each timestamped at download. Nothing in `data/raw/` is ever modified directly — all processing happens in scripts that write to `data/processed/`. This means you can always regenerate the processed data from scratch by re-running the pipeline, and you can verify exactly what the raw data looked like on any given date.

```python
# data/download_data.py
"""
Reproducible data downloader for [Project Name].
Run to refresh all raw data from authoritative sources.
"""
import requests, pandas as pd, logging
from datetime import datetime
from pathlib import Path

RAW_DIR = Path('data/raw')
RAW_DIR.mkdir(parents=True, exist_ok=True)
TIMESTAMP = datetime.now().strftime('%Y%m%d')

def download_primary_data():
    """Download primary dataset from source API."""
    url = 'https://api.your-primary-source.gov/v1/data'
    r = requests.get(url, params={'year': 2024}, timeout=30)
    r.raise_for_status()
    df = pd.DataFrame(r.json()['data'])
    path = RAW_DIR / f'primary_data_{TIMESTAMP}.csv'
    df.to_csv(path, index=False)
    return df

if __name__ == '__main__':
    download_primary_data()
```

> **TIP:** Always save raw data with a timestamp in the filename (e.g., `primary_data_20250115.csv`). This lets you trace exactly which data vintage was used in each version of the paper — a detail that reviewers and journal editors increasingly request.

---

## 11. Publication-Quality Figures: Healy Style Guide

Figures in academic papers are often underinvested. The standard workflow — matplotlib defaults, legend in the corner, axis title says "Figure 3" — produces charts that are technically correct but visually unpersuasive. Reviewers and readers form their first impression of your empirical work from the figures, and poor figures signal careless analysis even when the underlying work is rigorous. The principles in this section are adapted from Kieran Healy's *Data Visualization: A Practical Introduction*, which is the standard reference for social science figure design. Claude Code can apply these principles automatically if you instruct it to load the `figure_theme.py` module before generating any chart.

| Principle | Application |
|---|---|
| Show the data | Plot observations, not just means |
| Data-ink ratio | Remove non-informative gridlines and borders |
| Intentional colour | Reserve colour for categorical distinctions |
| Label directly | Annotate lines/bars; avoid legends where possible |
| Consistent typography | One sans-serif font throughout all figures |
| Honest scales | Never truncate y-axes |
| Declarative titles | "Group B pays 38% above cost" not "Figure 3: Shares" |

The `set_healy_theme()` function below encodes these principles as matplotlib rcParams, so every figure generated in the same session automatically inherits the correct styling. Save it in `code/figures/figure_theme.py` and instruct Claude Code to import it at the top of every figure generation script.

```python
# code/figures/figure_theme.py
import matplotlib as mpl

def set_healy_theme():
    mpl.rcParams.update({
        'font.family': 'sans-serif',
        'font.sans-serif': ['Source Sans Pro', 'DejaVu Sans'],
        'font.size': 11,
        'axes.spines.top': False,
        'axes.spines.right': False,
        'axes.grid': False,
        'legend.frameon': False,
        'figure.dpi': 300,
        'savefig.format': 'pdf',
    })
```

---

## 12. Subagents: Specialised AI Teammates

As research workflows grow in complexity, a single Claude Code session handling everything — literature review, data cleaning, model estimation, figure generation — becomes difficult to manage. Subagents solve this problem by allowing you to create narrowly scoped AI assistants, each focused on one type of task and each operating in its own isolated context window. Because a subagent's context is separate from the main session, its intermediate work does not pollute the main conversation. The main session receives only the final structured output — a table, a JSON object, a summary — and can use that to drive the next step of the workflow.

For researchers, the most immediately valuable subagents are a literature reviewer (queries Scholar Gateway and returns a formatted table of papers), a data auditor (checks a dataset for anomalies and missing values), and a data fetcher (downloads files from approved sources with reproducible parameters). You define each of these once and reuse them across every project.

### 12.1 Built-in Subagents

Claude Code ships with three built-in subagents that activate automatically based on what the main session needs. Understanding when each one activates helps you predict Claude Code's behaviour during complex tasks.

| Agent | Purpose |
|---|---|
| Explore | Read-only codebase search. Activated automatically when Claude needs to scan files before making changes. |
| Plan | Research agent for plan mode. Gathers codebase context before presenting a plan to you. |
| General-purpose | Multi-step tasks requiring both exploration and action — the default workhorse. |

### 12.2 The .claude/agents/ Folder

Custom subagents are defined as markdown files and stored in the `.claude/agents/` folder. The location of this folder determines the scope of the agent: project-level agents (in `.claude/agents/` inside your project) are committed to Git and available to all collaborators; user-level agents (in `~/.claude/agents/` in your home directory) are available across all your projects on that machine. For research-specific agents like a literature reviewer, the user-level location is usually the right choice.

| Location | Scope |
|---|---|
| `.claude/agents/*.md` | Project-level, committed to Git, shared with the team |
| `~/.claude/agents/*.md` | User-level, available across all your projects |

### 12.3 Subagent File Format

Each subagent is defined by a markdown file with a YAML header (the "frontmatter") followed by the agent's instructions. The YAML header specifies the agent's name (used to invoke it), a description (used to trigger it automatically), the tools it is allowed to use, and the model to run on. The description field is particularly important: if it begins with "Use PROACTIVELY when...", Claude Code will activate the agent automatically whenever that condition is met, without explicit invocation.

```markdown
---
name: agent-name-lowercase
description: >
  Use PROACTIVELY when [trigger condition].
  [One more sentence of context.]
tools: Read, Grep, Glob, Bash
model: sonnet
---

You are a [role description].

When invoked:
1. [First action]
2. [Second action]
3. Return: [output format -- JSON / markdown table]
```

### 12.4 Creating Agents

There are three ways to create a subagent, depending on whether you prefer a guided interface, direct file editing, or a quick one-off agent for a specific task. For permanent agents you plan to reuse, the manual file method gives you the most control over the exact wording of the description and instructions.

1. **Interactive:** type `/agents` inside a session → Create new agent. Claude Code will prompt you for the required fields.
2. **Manual file:** create `.claude/agents/your-agent.md` with the format above. This is the most explicit and reproducible method.
3. **Inline (temporary):** pass `--agents '{...}'` when launching `claude`. Useful for one-off sessions.

### 12.5 Invoking Agents

Agents can be invoked explicitly (by naming the agent in your prompt) or implicitly (by the main session detecting that the task matches the agent's description). For important research tasks, explicit invocation is preferable because it ensures you are controlling exactly which agent runs and on what data.

```
# Explicit invocation (recommended for important tasks)
Use the data-auditor agent to verify data/raw/source_data.csv

# Background execution
Ctrl+B   ← send agent to background, keep typing in the main session
```

### 12.6 Ready-to-Use Research Agent: Literature Reviewer

The literature reviewer agent below is ready to copy directly into your `~/.claude/agents/` folder. It searches Scholar Gateway for papers on any topic, retrieves metadata for each result, and returns a structured markdown table sorted by year. This is useful both for initial literature reviews at the start of a project and for checking whether new papers on your topic have appeared before submission.

```markdown
---
name: lit-reviewer
description: >
  Use PROACTIVELY when asked to find or summarise academic
  papers on any research topic.
tools: Read, Grep, Glob
model: sonnet
---

You are a systematic literature reviewer.
When invoked with a research topic:
1. Search Scholar Gateway for papers (last 5 years)
2. For each paper: title, authors, year, journal, DOI,
   key contribution, methodology, country studied
3. Return a markdown table sorted by year (newest first)
```

### 12.7 Agent Design Principles

The quality of a subagent depends almost entirely on the clarity of its definition. Vague descriptions produce inconsistent behaviour; overly broad tool permissions create security risks; unspecified output formats require extra processing before the output can be used. The four principles below capture the most important design decisions.

| Principle | Guidance |
|---|---|
| Single responsibility | One agent, one task. An agent that does research and modifies files will do both poorly. |
| Structured output | Specify the exact format: JSON, markdown table, named sections. This allows the main session to process the output programmatically. |
| Least-privilege tools | Grant only the tools the agent genuinely needs. A literature reviewer should have `Read` and `Grep` but not `Write` or `Bash`. |
| Clear description | Use `PROACTIVELY` for auto-delegation. Be specific about the exact trigger condition. |

> **WARNING:** Subagents cannot spawn other subagents. Do not instruct an agent to "call the X agent." All multi-agent orchestration must happen from the main session.

---

## 13. Installing Third-Party Agents

The community of Claude Code users has published a growing library of pre-built subagents for common research and development tasks. Rather than writing every agent from scratch, you can browse these repositories, evaluate the agents against the checklist in this section, and install the ones that suit your workflow. This section also applies to MCP server installation, which follows the same principle: download from a trusted source, review the permissions, verify the installation before relying on it.

### 13.1 Finding Community Agents

The most curated and reliable source for community agents is the VoltAgent repository on GitHub. Before installing from any community source, it is worth reading the agent's system prompt in full — the system prompt defines exactly what the agent will do, and a well-written one should be clear, bounded, and specific.

- **github.com/VoltAgent/awesome-claude-code-subagents** — 100+ curated, reviewed agents across research, development, and data tasks
- GitHub search: `claude code subagents` or `.claude/agents` — finds individual agents published by users
- **glama.ai/mcp/servers** — a rated registry of MCP servers with install instructions and community reviews

### 13.2 Installation Methods

There are three ways to install a community agent, depending on how many you want and how much you want to customise them. Manual copy (Method A) is best when you want to review and possibly edit the agent before installing. Git clone and copy (Method B) is efficient when you want to install several agents from the same repository. The install script (Method C) is the fastest but the least transparent — use it only for repositories you fully trust.

#### Method A: Manual Copy

This is the recommended approach for individual agents. Copy the raw file from GitHub and paste it into a new agent file in your agents folder. You can review and edit the contents before saving.

```bash
# Project scope
touch .claude/agents/research-analyst.md
# paste contents from GitHub Raw view

# User scope (all projects)
touch ~/.claude/agents/research-analyst.md
```

#### Method B: Git Clone and Copy

This method is efficient for installing multiple agents from a single repository at once.

```bash
git clone https://github.com/VoltAgent/awesome-claude-code-subagents.git
ls awesome-claude-code-subagents/agents/
cp agents/research-analyst.md .claude/agents/
cp agents/data-researcher.md  .claude/agents/
```

#### Method C: Install Script

The fastest method, but the least transparent. Only use this for repositories you have already reviewed.

```bash
curl -sO https://raw.githubusercontent.com/VoltAgent/\
awesome-claude-code-subagents/main/install-agents.sh
chmod +x install-agents.sh && ./install-agents.sh
```

### 13.3 Evaluation Checklist Before Installing

Before adding any community agent to your setup, work through this checklist. The `tools:` field in the YAML frontmatter is the most important thing to check — it tells you exactly what the agent is allowed to do on your system. A literature reviewer needs only `Read`; any agent requesting `Bash` on an untrusted source is a potential security risk.

1. **Tool permissions:** read the `tools:` field. Research agents should not need `Write` or `Bash` unless explicitly required by their function.
2. **System prompt clarity:** the instructions should be specific, bounded, and specify a clear output format.
3. **Description trigger:** the description should not be so broad that the agent activates unexpectedly on unrelated tasks.
4. **Repository activity:** check the last commit date. An unmaintained agent may behave incorrectly with the current Claude Code version.

> **WARNING:** Never install a `Bash`-enabled agent from an untrusted source without reading every line of the system prompt. A malicious agent with Bash access could read, modify, or delete files on your computer.

### 13.4 Verifying Installation

After installing an agent, verify that it has loaded correctly before relying on it for real work. The `/agents` command lists all loaded agents; `/status` shows the current session state including which agents are available. A quick test prompt confirms that the agent activates and returns output in the expected format.

```
/agents    ← list all loaded agents and their descriptions
/status    ← confirm agent appears in session state

Use the research-analyst agent to give me a two-sentence
overview of [your research topic].
```

> **TIP:** If an agent fails to load, paste the YAML frontmatter into [yamllint.com](https://yamllint.com). The most common errors are a missing closing `---`, tab characters (YAML requires spaces), and colons inside unquoted strings.

---

## 14. The Knowledge Management Stack: Zotero, Obsidian, NotebookLM & Claude Code

This section describes a powerful, integrated workflow for managing research knowledge across multiple papers and topics over time. It combines four tools — Zotero, Obsidian, NotebookLM, and Claude Code — each doing what it does best.

The core idea comes from Andrej Karpathy (former OpenAI, Tesla AI Director), who described shifting a large fraction of his LLM usage from writing code to **manipulating knowledge stored as markdown files**. The mental shift is simple but profound: instead of using Claude as a chatbot you ask questions and forget, you use it as a **compiler and librarian** that builds a persistent, compounding knowledge base on your behalf. Alexandra Phelan's detailed workflow guide for combining Zotero and Obsidian has also been influential in shaping the approach described here ([source](https://medium.com/@alexandraphelan/an-updated-academic-workflow-zotero-obsidian-cffef080addd)).

### 14.1 Why This Approach Matters for Researchers

Most researchers' experience with AI follows a frustrating pattern: you ask a question, get a good answer, close the tab, and lose everything. The next week you start from scratch. Nothing accumulates.

The approach described here is different. It is **stateful and compounding**:

- Today's answer becomes tomorrow's context.
- Every paper you read adds a permanent, cross-referenced entry to your wiki.
- Your own analyses and queries file back into the knowledge base and improve future queries.
- Six months of work results in a private corpus your LLM can read in a single context window.

For energy economics researchers, this means your knowledge about electricity market mechanisms, capacity auction designs, renewable integration challenges, and empirical findings across regions never disappears — it compounds.

### 14.2 The Four Layers

The stack has four distinct layers, each with a specific role. Understanding the boundary between layers is important: Claude Code reads from the raw layer but never modifies it; you read from the wiki but rarely write to it directly. Keeping these roles clean ensures the system remains organised as it scales.

```
┌─────────────────────────────────────────────────────────────┐
│  LAYER 1: SOURCE COLLECTION — Zotero + Web Clipper          │
│  PDFs, papers, articles, datasets, notes                    │
│  Lives in: Zotero library + raw/ folder                     │
├─────────────────────────────────────────────────────────────┤
│  LAYER 2: SYNTHESIS — NotebookLM                            │
│  Batch-ingests sources, produces structured summaries       │
│  Use for: large reading lists, initial domain overview      │
├─────────────────────────────────────────────────────────────┤
│  LAYER 3: WIKI / KNOWLEDGE BASE — Obsidian                  │
│  LLM-maintained markdown wiki in wiki/ folder               │
│  You read; Claude writes                                    │
├─────────────────────────────────────────────────────────────┤
│  LAYER 4: OPERATIONS — Claude Code                          │
│  Ingests sources, compiles wiki, answers queries,           │
│  lints wiki, generates reports in reports/                  │
└─────────────────────────────────────────────────────────────┘
```

### 14.3 Setting Up Zotero

Zotero is your primary reference manager. It stores all paper metadata, PDFs, and annotations, and generates consistent citation keys for use in manuscripts. Its role in this stack is to act as the trusted, authoritative source for all bibliographic information — every paper that enters your research pipeline goes through Zotero first.

#### Step 1 — Install Zotero

Download from [zotero.org](https://www.zotero.org/). It is free and works on Windows, macOS, and Linux. After installation, install the browser connector (available for Chrome, Firefox, Edge) — this one-click tool saves any academic paper or web article to your Zotero library with full metadata automatically populated.

#### Step 2 — Install the BetterBibTeX Plugin

BetterBibTeX (BBT) is essential because it generates consistent, human-readable citation keys — called citekeys — in the format `Author_YYYY` (e.g., `Borenstein_2002`, `Joskow_2019`). These citekeys are the bridge between Zotero and Obsidian: the same key used in Obsidian's Literature Notes can be used as a Pandoc citation in your manuscript, ensuring that references are consistent across your knowledge base and your papers.

1. Download the latest `.xpi` file from [retorque.re/zotero-better-bibtex](https://retorque.re/zotero-better-bibtex/).
2. In Zotero: *Tools* → *Add-ons* → gear icon → *Install Add-on From File* → select the `.xpi`.
3. Restart Zotero. Go to *Edit* → *Preferences* → *Better BibTeX* to configure the citekey format.

Recommended citekey format: `[auth:lower]_[year]` (produces `borenstein_2002`).

#### Step 3 — Export Your Library as a .bib File

The `.bib` file is the machine-readable version of your Zotero library. Obsidian's Pandoc Reference List plugin reads it to display formatted citations alongside your manuscript draft. Claude Code can also read it to look up paper metadata during a wiki-building session. The "Keep Updated" option is important — it means the `.bib` file refreshes automatically whenever you add a new paper to Zotero, so your downstream tools always have current information.

In Zotero: *File* → *Export Library* → Format: **Better BibTeX** → check **Keep Updated** → save to a stable path such as `~/Documents/MyLibrary.bib`.

#### Step 4 — Annotate PDFs Inside Zotero

Since Zotero 6, you can read and annotate PDFs directly inside the app. A colour-coding system turns annotations into structured, reusable data: when Obsidian's Zotero Integration plugin imports a Literature Note, it groups annotations by colour, so you can instantly see all your methodology notes together, all your critical claims together, and so on. Establish a personal colour convention and use it consistently across all papers.

| Colour | Meaning (suggested) |
|---|---|
| 🟡 Yellow | Interesting point or key finding |
| 🔴 Red | Critical claim / point of disagreement |
| 🟢 Green | Methodology note |
| 🔵 Blue | Relevant to your specific research question |

### 14.4 Setting Up Obsidian

Obsidian is where your knowledge actually lives. Think of it not as a note-taking app, but as a **knowledge IDE** — a place where you can browse, navigate, and visualise everything you know about a topic. Because it stores all data as plain `.md` files on your local machine, it integrates seamlessly with Claude Code: any file Claude Code writes in your vault is immediately visible in Obsidian, and vice versa.

#### Step 1 — Install Obsidian

Download from [obsidian.md](https://obsidian.md/). It is free for personal use and works on all platforms. Because Obsidian stores data as plain markdown, your notes are never locked into a proprietary format — you can open them in any text editor, commit them to Git, or process them with scripts.

#### Step 2 — Create Your Vault with the Research Folder Structure

A "vault" is simply a folder on your computer that Obsidian treats as its database. Create one with the structure below. The division between `raw/`, `wiki/`, `reports/`, and `literature-notes/` mirrors the four layers described in Section 14.2, making it easy for both you and Claude Code to know where everything should go.

```
my-research-vault/
├── raw/                  ← Source material (articles saved via Web Clipper)
├── wiki/                 ← LLM-compiled knowledge base (Claude writes this)
│   ├── concepts/         ← One .md file per key concept
│   ├── entities/         ← Papers, authors, institutions, datasets
│   ├── index.md          ← Master index of all wiki pages
│   └── log.md            ← Append-only log of all operations
├── reports/              ← Output files from complex queries
├── literature-notes/     ← One .md per paper (generated by Zotero Integration)
└── CLAUDE.md             ← Schema file: tells Claude how the wiki works
```

> **TIP:** In Obsidian Settings → Files and links, set the **Attachment folder path** to `raw/assets/`. Then bind a hotkey to "Download attachments for current file" (Settings → Hotkeys, search "Download"). After clipping an article, press the hotkey to save all images locally so Claude can reference them without hitting broken external URLs.

#### Step 3 — Install the Obsidian Web Clipper

The [Obsidian Web Clipper](https://obsidian.md/clipper) is a browser extension that converts any web page into a clean `.md` file and saves it directly to your vault's `raw/` folder — with URL, title, publication date, and tags automatically populated. This is the primary capture tool for the system. Whenever you encounter a useful article, report, or blog post, one click saves a permanent local copy in your vault. Do not organise or rename the clipped files — just capture, and let Claude Code handle the organisation when it ingests them into the wiki.

#### Step 4 — Install Essential Obsidian Plugins

These four plugins transform Obsidian from a markdown editor into a research-grade knowledge management system. All are available from Settings → Community Plugins → Browse.

| Plugin | Purpose |
|---|---|
| **Zotero Integration** | Pulls Zotero paper metadata and PDF annotations automatically into Literature Notes |
| **Pandoc Reference List** | Displays a formatted, copy-pasteable reference list for all citekeys in the current document |
| **Dataview** | Queries your notes like a database, enabling summary tables of all Literature Notes or wiki pages |
| **Pandoc** | Exports markdown manuscripts to `.docx` with fully processed citations in any citation style |

#### Step 5 — Configure Zotero Integration

In Obsidian Settings → Zotero Integration: set the **Citation format** to Pandoc (which produces `[@Author_Year]` citekeys compatible with LaTeX and Word exports), and point **BibTeX path** to the `.bib` file you exported from Zotero in Section 14.3. Then create a Literature Note template (Section 14.6) so that every imported paper follows a consistent structure.

#### Step 6 — Enable Graph View

Obsidian's graph view shows all your notes as nodes with bidirectional links as edges. As your wiki grows, knowledge clusters become visible: a dense cluster around "capacity market design" that links to papers, methodology notes, and reports. Isolated nodes — notes with no inbound links — indicate gaps: concepts you have mentioned but not fully developed. Use the graph view at least weekly to guide what to read next and what wiki pages need more attention.

### 14.5 Setting Up NotebookLM

NotebookLM is a Google tool that excels at one specific task: rapidly synthesising a large batch of sources into a coherent narrative document. While Claude Code is better suited to the careful, one-at-a-time incremental maintenance of your wiki, NotebookLM is the right tool when you are starting a new research sub-topic and have 20–40 papers to review. Think of it as the batched initialisation step — you use NotebookLM to get oriented across a literature quickly, then hand that synthesis to Claude Code for integration into your persistent knowledge base.

#### What NotebookLM Does Best

NotebookLM can ingest PDFs, URLs, Google Docs, and YouTube transcripts simultaneously. This makes it particularly useful for reviewing a complete conference proceedings session, a special journal issue, or a set of policy reports on a specific topic. Its Studio panel can produce audio overviews that you can listen to while commuting — a surprisingly efficient way to survey a literature before reading in depth.

- Ingests many sources simultaneously (PDFs, URLs, Google Docs, YouTube transcripts).
- Produces a comprehensive synthesis document covering key themes, findings, and debates.
- Generates audio overviews (podcast-style dialogue) for quick orientation.
- Answers questions grounded in your specific sources, with inline citations.

#### How to Use It in Your Workflow

1. Go to [notebooklm.google.com](https://notebooklm.google.com/) and create a new notebook for your topic.
2. Add your sources: paste URLs of journal articles, upload PDFs, or add YouTube lecture URLs.
3. In the Studio panel, ask NotebookLM to produce a **comprehensive synthesis document** covering the key themes, findings, methodologies, and open debates across all sources.
4. Save the output as a `.md` file and place it in your vault's `raw/` folder.
5. Instruct Claude Code to ingest it into your wiki as a high-level overview article.

> **TIP:** Use NotebookLM at the **start of a new sub-topic** to get oriented quickly. Once you have the synthesis document and have populated the initial wiki pages, switch to Claude Code for the ongoing, incremental maintenance of your wiki from that point forward.

#### Connecting NotebookLM Output to Claude Code

Once NotebookLM has produced a synthesis document, feed it to Claude Code using a prompt like this. Claude Code will read the synthesis, identify the key concepts it covers, and build out the corresponding wiki pages automatically.

```bash
claude -p "I've added a new synthesis document to /raw/notebooklm-synthesis-capacity-markets.md.
Read it, identify the 5-10 most important concepts it covers, and create or update
concept pages in /wiki/concepts/ for each. Update /wiki/index.md accordingly.
Show me every file you touched." --allowedTools Bash,Write,Read
```

### 14.6 Creating Zotero Literature Notes in Obsidian

A Literature Note is a single Obsidian page for each paper in your Zotero library. It is generated automatically by the Zotero Integration plugin and contains the full metadata, an abstract, a direct link back to the Zotero record, and all your PDF annotations grouped by colour. Rather than scattered highlights that live only inside the PDF, your annotations become searchable, linkable markdown text — part of the same knowledge graph as your wiki pages and your manuscript drafts.

#### The Literature Note Template

Save this template as `literature-notes/_template.md` in your vault. (Copy-paste into a plain text editor first to remove any hidden formatting before pasting into Obsidian.)

```
---
category: literaturenote
tags: {% if allTags %}{{allTags}}{% endif %}
citekey: {{citekey}}
status: unread
dateread:
---

> [!Cite]
> {{bibliography}}

>[!Synth]
>**Contribution**::
>
>**Related**:: {% for relation in relations | selectattr("citekey") %} [[@{{relation.citekey}}]]{% endfor %}

>[!md]
{% for type, creators in creators | groupby("creatorType") -%}
{%- for creator in creators -%}
> **{{"First" if loop.first}}{{type | capitalize}}**::
{%- if creator.name %} {{creator.name}}
{%- else %} {{creator.lastName}}, {{creator.firstName}}
{%- endif %}
{% endfor %}~
{%- endfor %}
> **Title**:: {{title}}
> **Year**:: {{date | format("YYYY")}}
> **Citekey**:: {{citekey}}
> **Journal**:: *{{publicationTitle}}*

> [!Abstract]
> {{abstractNote}}

# Notes

# Annotations
{% persist "annotations" %}
{% set newAnnotations = annotations | filterby("date", "dateafter", lastImportDate) %}
{% if newAnnotations.length > 0 %}
### Imported: {{importDate | format("YYYY-MM-DD")}}
{% for a in newAnnotations %}
> {{a.annotatedText}}
{% endfor %}
{% endif %}
{% endpersist %}
```

In Zotero Integration settings, click **Add Import Format** and set the template path to this file.

#### Creating a Literature Note

Press `Cmd+P` (macOS) or `Ctrl+P` (Windows/Linux) to open the Obsidian command palette → type **Zotero Integration: Create Literature Note** → search for your paper. The note is generated instantly with all metadata and annotations.

#### Citation Convention

The setup creates a clean, unambiguous distinction between citing a paper and linking to its Literature Note, using the same citekey in both cases:

- `[@Borenstein_2002]` — inline Pandoc citation, used in manuscript text and processed by Pandoc on export
- `[[@Borenstein_2002]]` — Obsidian bidirectional link, opens the Literature Note directly

This means every paper you cite in a manuscript draft has a corresponding Literature Note you can navigate to in one click, and every Literature Note automatically appears in Obsidian's graph view as a connected node.

### 14.7 Setting Up the Claude Code + Obsidian Connection via MCP

While you can use Claude Code with your vault by simply pointing it at the vault folder in the terminal, an MCP connection allows Claude to interact with Obsidian's internal APIs in real time — reading notes, writing new pages, appending under specific headings, and searching across the vault — all from within a Claude chat session, without touching the terminal at all. This is useful for quick, interactive knowledge management tasks that do not warrant a full Claude Code session.

#### Step 1 — Install the Local REST API Plugin in Obsidian

In Obsidian: Settings → Community Plugins → Browse → search **Local REST API** → Install and Enable. This plugin runs a small HTTP server inside Obsidian that exposes your vault via a REST API. Copy the API key shown in the plugin's settings panel.

#### Step 2 — Add the MCP Server Configuration

Open the Claude Desktop configuration file:

- **macOS:** `~/Library/Application Support/Claude/claude_desktop_config.json`
- **Windows:** `%APPDATA%/Claude/claude_desktop_config.json`

Add the block below, replacing `<your_api_key_here>` with the key you copied from Step 1:

```json
{
  "mcp-obsidian": {
    "command": "uvx",
    "args": ["mcp-obsidian"],
    "env": {
      "OBSIDIAN_API_KEY": "<your_api_key_here>",
      "OBSIDIAN_HOST": "127.0.0.1",
      "OBSIDIAN_PORT": "27124"
    }
  }
}
```

Restart Claude Desktop for the configuration to take effect.

> **WARNING:** Obsidian must be open and running whenever you use this MCP connection. The Local REST API plugin only operates while the vault is active in Obsidian.

#### Step 3 — Verify the Connection

In a Claude chat window, type: `Use Obsidian to list files in my vault.` If the connection is working, Claude will return a list of your vault's files and folders.

#### What Claude Can Do with Your Vault via MCP

| Operation | Example Prompt |
|---|---|
| Browse vault structure | "List all files in my wiki/ folder" |
| Read a specific note | "Read the file wiki/concepts/capacity-markets.md" |
| Search across notes | "Find all notes mentioning 'merit order effect'" |
| Add content under a heading | "Add this summary under the #Findings heading in my note on Joskow_2019" |
| Append to a note | "Append today's reading notes to raw/notes-2026-04-15.md" |
| Create new wiki pages | "Create a new concept page for 'scarcity pricing' in wiki/concepts/" |

### 14.8 The Daily Workflow: Putting It All Together

A knowledge management system is only as valuable as the habits that feed it. The daily workflow below is designed to be low-friction: most of the organisational work is delegated to Claude Code, so your job is simply to capture, read, and ask good questions.

**Morning — Capture**

1. Browse journals, RSS feeds, or news. Use the Obsidian Web Clipper to save anything interesting directly to `raw/`. Do not organise — just capture. The key discipline is to clip generously and organise never: Claude Code will handle the filing.
2. For new academic papers, add them to Zotero via the browser connector. Generate Literature Notes for the papers you read that day.

**During Reading — Annotate**

3. Read PDFs inside Zotero, using colour-coded highlights. Add brief margin notes for key insights or connections to other work you know.
4. After reading, run "Zotero Integration: Create Literature Note" in Obsidian to pull all annotations in automatically.

**Processing — Compile the Wiki**

5. Open Claude Code in VSCode, pointing at your vault folder. Run an ingest command to update the wiki with the day's new material:

```bash
claude -p "I just added 3 new articles to /raw/ and created literature notes for them.
Read each literature note, extract the key ideas, and:
1. Write or update concept pages in /wiki/concepts/ for each major idea
2. Update /wiki/index.md
3. Flag any contradictions with existing wiki pages
4. Log what you did in /wiki/log.md.
Show me every file you touched." --allowedTools Bash,Write,Read
```

**Querying — Generate Reports**

6. Ask complex questions against your accumulated wiki — questions that would require synthesising multiple papers if you were working from scratch:

```bash
claude -p "Using only my wiki in /wiki/, write a 500-word synthesis of
what I know about the relationship between renewable energy penetration
and electricity price volatility. Save the output to /reports/synthesis-renewables-volatility.md
and link it from the relevant concept pages." --allowedTools Bash,Write,Read
```

**Weekly — Lint the Wiki**

7. Once a week, run a health check to keep the wiki well-organised and internally consistent:

```bash
claude -p "Read every file in /wiki/. Find:
- Contradictions between pages
- Orphan pages with no inbound links
- Concepts mentioned frequently but lacking a dedicated page
- Claims that look outdated based on newer files in /raw/
Write a health report to /wiki/lint-report.md with specific fixes."
--allowedTools Bash,Write,Read
```

### 14.9 The Schema File (CLAUDE.md in the Vault)

The `CLAUDE.md` file at the root of your vault is the operating manual for Claude's knowledge management work. Without it, Claude starts each session with no understanding of your folder conventions, citekey format, or domain context. With a well-maintained `CLAUDE.md`, Claude can navigate your vault, maintain consistent conventions, and produce outputs that integrate cleanly with everything already there. Update this file whenever you add a new section type to the wiki or change a naming convention.

```markdown
# Research Wiki Schema

## Vault Structure
- raw/        → immutable source material. Claude reads but never modifies.
- wiki/       → Claude-maintained knowledge base. Claude reads and writes.
  - concepts/ → one .md per concept (e.g., merit-order-effect.md)
  - entities/ → one .md per paper, author, dataset, or institution
  - index.md  → master index: all pages with one-line summaries
  - log.md    → append-only operation log (prefix: ## [YYYY-MM-DD] verb | title)
- reports/    → output files from queries (Claude writes; I read)
- literature-notes/ → Zotero-generated notes (Claude reads; I maintain)

## Citekey Convention
Papers are referenced as [[@Author_YYYY]] (Obsidian link) or [@Author_YYYY] (Pandoc).

## When Ingesting a New Source
1. Read the source in raw/ or the literature note in literature-notes/
2. Identify 3-10 key concepts it introduces or advances
3. Create or update a concept page in wiki/concepts/ for each
4. Update wiki/index.md
5. Append an entry to wiki/log.md

## When Answering a Query
1. Read wiki/index.md to identify relevant pages
2. Read all relevant concept and entity pages
3. Write the answer as a new .md file in reports/
4. Link the report from the relevant concept pages
5. Append to wiki/log.md

## Domain Context
This wiki covers: electricity market design, renewable energy policy,
capacity mechanisms, energy transition economics, empirical IO methods.
Primary region of focus: MENA and Gulf energy markets.
```

### 14.10 An Example: Energy Economics Research in Practice

To make this concrete, here is what the setup looks like for a researcher studying capacity market design in the Gulf. After setting up the vault and running the stack for one month, the `wiki/concepts/` folder might contain files such as:

- `capacity-market-design.md` — synthesis of 12 papers on auction mechanisms
- `scarcity-pricing.md` — definition, examples from ERCOT, Texas literature
- `merit-order-effect.md` — empirical evidence across 8 country studies
- `renewable-curtailment.md` — causes, measurement, mitigation strategies
- `voll-estimation.md` — methodological notes from three empirical papers

When you then ask: *"What does my research say about the relationship between capacity adequacy metrics and renewable curtailment in markets with high solar penetration?"*, Claude reads the relevant pages and synthesises an answer that draws on everything you have read — in seconds, with full citations — and saves the report to `reports/` for reuse in future queries and in your manuscript.

---

## 15. AI Paradigms for Research (Korinek, 2025)

Not all research tasks are suited to the same type of AI tool. Anton Korinek's NBER working paper on AI agents for economic research provides a useful taxonomy of three paradigms, each suited to different phases of the research workflow. Understanding which paradigm fits your current task helps you choose the right tool and set realistic expectations for what it can and cannot do. For most researchers, the workflow in this guide spans all three: drafting and editing uses traditional LLMs; formal derivations and debugging use reasoning models; and the agentic workflows described here use Claude Code as an agentic chatbot.

*Based on: Korinek, A. (2025). AI Agents for Economic Research. NBER Working Paper No. 34202. Online resources: [GenAIforEcon.org](https://www.GenAIforEcon.org).*

| Paradigm | Best For |
|---|---|
| Traditional LLMs | Drafting, summarising, editing, LaTeX formatting |
| Reasoning Models | Mathematical derivations, formal proofs, complex code debugging |
| Agentic Chatbots | End-to-end workflows: data download → analysis → figures → narrative |

### 15.1 Tool Budget

The question of how much to spend on AI tools is a question of how to value your time. A researcher who spends three hours on a data cleaning task that Claude Code could complete in fifteen minutes has effectively paid a high cost for something that is very cheap to delegate. The figures below are approximate as of 2025–2026 and are intended as a starting point.

$20/month provides access to Claude.ai Pro and covers moderate daily use, including complex editing and document generation tasks. $200/month provides access to higher rate limits and more powerful model variants through the API, enabling the kind of agentic workflows — multi-step sessions with large context windows — described in this guide. Treat AI tool spending as a research input, the same way you would treat a data purchase or a conference registration.

---

## 16. Critical Limitations & Responsible Oversight

AI tools are powerful research accelerators, but they introduce specific failure modes that do not arise with traditional research software. The most dangerous of these is **confident hallucination**: unlike a Python script, which either runs correctly or raises an error, a language model will produce a plausible-sounding but incorrect answer without any indication that something has gone wrong. This means that every factual claim, every citation, and every statistical result produced or referenced by Claude Code requires human verification before it appears in a manuscript. The table below catalogues the most common failure modes in research use and describes the mitigations that reduce (but do not eliminate) each risk.

| Failure Mode | Mitigation |
|---|---|
| Hallucinations | Verify every citation; trace every statistic to its primary source |
| Cascading errors | Human checkpoints between pipeline stages — do not let Claude Code run a 10-step pipeline unsupervised |
| Prompt brittleness | Version prompts in CLAUDE.md and plan.md so you can reproduce results |
| Economic reasoning errors | Expert review of all theoretical content; Claude structures arguments, but the intellectual core must be yours |
| Cost escalation | Monitor `/usage` regularly; prefer short, focused sessions over long ones |
| Wiki drift | Run the weekly lint pass to prevent the knowledge base from accumulating inconsistencies |
| Stale knowledge | Claude's training has a cutoff date; always verify claims about recent policy changes, new data releases, or current market conditions |

> **TIP:** The right mental model is to treat Claude Code as a team of capable but fallible research assistants. They work quickly, follow instructions well, and rarely refuse a task — but they also make confident mistakes and do not flag uncertainty. Your domain expertise and critical judgement remain the final quality gate on everything that enters a manuscript.

---

## 17. Best Practices Summary

The practices below distil the most important lessons from experienced Claude Code users into a single reference. They are not rules to follow rigidly, but habits to build gradually. If you are new to this workflow, the highest-return habits to start with are: writing a thorough `CLAUDE.md`, using `plan.md` to open every session, and committing after every session. The knowledge management habits — keeping the vault `CLAUDE.md` current, running weekly lint passes, filing query outputs back into the wiki — become valuable later, once the knowledge base is large enough that compounding effects start to show.

| Practice | Why It Matters |
|---|---|
| Always pull before starting | Avoids working on a stale version and creating merge conflicts with co-authors |
| Write CLAUDE.md thoroughly | Eliminates the need to re-explain project context at the start of every session |
| Use plan.md + progress.md | Creates an external memory that persists across sessions and serves as a research journal |
| 5–10 turn focused sessions | Keeps context quality high; long sprawling sessions produce degraded, inconsistent outputs |
| Commit after every session | Every commit is a rollback point — the only reliable way to undo unintended file changes |
| Save figures as PDF + PNG | PDF for high-resolution LaTeX inclusion; PNG for quick preview and presentations |
| Run /compact proactively | Prevents context overflow before it degrades response quality |
| Timestamp all raw data files | Makes it possible to trace exactly which data vintage was used in any version of the paper |
| Plan before coding | Writing the plan forces you to articulate assumptions; wrong assumptions are much cheaper to fix in text than in code |
| One task per session | Prevents context contamination between unrelated analyses |
| Keep vault CLAUDE.md current | Every knowledge management session starts with full context about your wiki's structure and conventions |
| Run weekly wiki lint | Prevents the knowledge base from drifting toward inconsistency as it grows |
| File query outputs back into wiki | Insights compound; a good synthesis written today saves you hours when you revisit the topic in six months |
| Use NotebookLM for batch ingestion | Efficient for large initial reading lists; use Claude Code for the ongoing incremental maintenance thereafter |

---

## 18. Troubleshooting

Even with a well-configured setup, things occasionally go wrong. The table below covers the most common problems encountered when using Claude Code for research and provides specific, actionable resolutions. When an issue is not on this list, the most productive debugging approach is to check `/status` first (to see the current session state), then check the relevant configuration file, then try isolating the problem by testing a simpler version of the same command. Most issues have a straightforward fix once the root cause is identified.

| Issue | Resolution |
|---|---|
| Claude ignores CLAUDE.md | Explicitly reference it: "Please read CLAUDE.md before starting." Claude Code auto-loads it but may deprioritise it in long sessions. |
| Context quality degrades mid-session | Run `/compact` to summarise history, or start a fresh session with a brief context summary. |
| MCP server not responding | Check `/status`; verify the URL and API key in settings.json; confirm the external service is running. |
| Agent fails to load | Paste the YAML frontmatter into [yamllint.com](https://yamllint.com). Common errors: missing `---`, tab characters, colons in unquoted strings. |
| Git merge conflicts | Commit before each session; if conflicts occur, resolve them manually before resuming Claude Code work. |
| Token costs spike unexpectedly | Avoid loading large files directly into context; use `head`, `sample`, or summarise-first patterns. |
| Web fetch blocked | Add the domain to the `allow` list in your `.claude/settings.json` permissions block. |
| PowerShell execution error (Windows) | Run `Set-ExecutionPolicy -Scope CurrentUser RemoteSigned` in PowerShell as Administrator. |
| Obsidian MCP not connecting | Confirm Obsidian is open; verify Local REST API plugin is enabled and the API key in your config matches the one in Obsidian's plugin settings. |
| Zotero Integration parse error | Copy the template into Notepad first to strip hidden formatting, then paste into Obsidian. |
| `code` command not found (macOS) | Run "Shell Command: Install 'code' command in PATH" from the VSCode command palette (`Cmd+Shift+P`). |
| `uvx` not found for MCP | Run `which uvx` in terminal; paste the full path into the `command` field in `claude_desktop_config.json` instead of just `"uvx"`. |
| Claude writes to raw/ folder | Review the vault CLAUDE.md schema file and explicitly state that `raw/` is immutable and Claude must never modify it. |

---

*End of Implementation Guide*

*SMS | Claude Code for Research*
*Based on Korinek (2025) NBER WP 34202, Karpathy (2026) LLM Knowledge Bases, Phelan (2023) Zotero & Obsidian Workflow, and AI MBA Webinar Series*

#### Disclaimer: Use of this guide and any associated tools is strictly at your own risk.
