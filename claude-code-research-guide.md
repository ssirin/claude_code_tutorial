# Claude Code for Research
## A Comprehensive Implementation Guide
### For Energy Economics & Quantitative Research
**Selahattin Murat Sirin | Riyadh,  2025–2026**
#### Disclaimer: Use of this website and its information is strictly at your own risk.
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

- Treat Claude Code as a senior research assistant that needs clear context and goals at the start of each session.
- Use short, focused sessions rather than long, sprawling conversations — context degrades over time.
- Always version-control your work: Claude Code and Git are inseparable in a professional workflow.
- Separate concerns into folders: `data/`, `code/`, `outputs/`, `review/`, and `latex/`.
- Persist decisions in files (`plan.md`, `progress.md`, `CLAUDE.md`) rather than relying on session memory.

### 1.2 The Research Stack This Guide Covers

This guide covers a full researcher's software stack, from writing environment to knowledge management to agentic coding:

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

Visual Studio Code (VSCode) is a free, open-source code editor by Microsoft and is the recommended environment for working with Claude Code. It provides a terminal, file explorer, Git integration, and an extensions marketplace — all in one place.

### 2.1 System Requirements

| Platform | Minimum Requirement |
|---|---|
| Windows | Windows 10 or later (64-bit) |
| macOS | macOS 10.15 (Catalina) or later |
| Linux | Ubuntu 18.04, Debian 10, Fedora 34, or equivalent |
| RAM | 4 GB minimum; 8 GB recommended |
| Disk | 500 MB free space |

### 2.2 Download and Install

**Step 1 — Download the installer.**

Visit the official VSCode download page: [https://code.visualstudio.com/download](https://code.visualstudio.com/download)

Select the installer for your operating system. Always download from the official site to avoid third-party distributions.

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

> **TIP:** After installation, open a new terminal (Command Prompt, PowerShell, or Git Bash) and type `code --version` to verify VSCode is on your PATH.

#### macOS

1. Open the downloaded `.zip` archive. This extracts `Visual Studio Code.app`.
2. Drag `Visual Studio Code.app` to your **Applications** folder.
3. Open VSCode from Applications.
4. To add the `code` command to your terminal PATH: open VSCode, press `Cmd+Shift+P`, type **Shell Command: Install 'code' command in PATH**, and press Enter. This allows you to type `code .` in any terminal to open a folder in VSCode.

> **TIP:** If macOS blocks the app ("unidentified developer"), go to System Settings → Privacy & Security → scroll to the bottom and click **Open Anyway**.

#### Linux (Ubuntu/Debian)

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

Verify the installation: `code --version`

### 2.3 Essential VSCode Settings for Research

Once VSCode is open, configure the following settings to make it research-friendly. Open the Settings editor with `Ctrl+,` (Windows/Linux) or `Cmd+,` (macOS), or press `Ctrl+Shift+P` → **Preferences: Open Settings (JSON)** to edit the JSON directly.

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

> **TIP:** Setting `"terminal.integrated.defaultProfile.windows": "Git Bash"` is critical on Windows. Claude Code requires a Unix-compatible shell. If Git Bash is not installed, download it from [gitforwindows.org](https://gitforwindows.org/) before proceeding.

### 2.4 Recommended Extensions for Researchers

Install these from the VSCode Extensions panel (`Ctrl+Shift+X`):

| Extension | Purpose |
|---|---|
| **Claude Code** (by Anthropic) | The AI coding agent — the core of this guide |
| **Python** (by Microsoft) | Python language support, linting, Jupyter integration |
| **Jupyter** (by Microsoft) | Run `.ipynb` notebooks inside VSCode |
| **GitLens** | Advanced Git history and blame annotations |
| **Markdown All in One** | Preview, shortcuts, and TOC for `.md` files |
| **LaTeX Workshop** | Compile and preview LaTeX directly in VSCode |
| **Rainbow CSV** | Highlight and query `.csv` files by column |

To install any extension: click the Extensions icon in the left sidebar → search by name → click **Install**.

### 2.5 Opening a Research Project in VSCode

The correct way to open a project in VSCode is to open the **folder**, not individual files. This gives VSCode (and Claude Code) full access to all project files, the terminal, and Git.

```bash
# Option 1: from any terminal
cd /path/to/your/project
code .

# Option 2: from VSCode
# File → Open Folder → navigate to your project folder → OK
```

> **WARNING:** Never open VSCode by double-clicking individual `.py` or `.md` files. Always open the project folder. Claude Code cannot read your project structure if only a single file is open.

---

## 3. Authentication & Initial Setup for Claude Code

### 3.1 Prerequisites

Before installing Claude Code, you need:

1. **Node.js** (version 18 or higher). Download from [nodejs.org](https://nodejs.org/). Verify with `node --version`.
2. **npm** (comes bundled with Node.js). Verify with `npm --version`.
3. An **Anthropic account** at [claude.ai](https://claude.ai) or an API key from [console.anthropic.com](https://console.anthropic.com).

### 3.2 Installation

Install Claude Code globally via npm:

```bash
npm install -g @anthropic-ai/claude-code
claude --version    # verify installation
```

#### Installing the VSCode Extension

1. Open VSCode. Go to the Extensions panel (`Ctrl+Shift+X`).
2. Search for **Claude Code** and install the extension by Anthropic.
3. Open the Claude Code panel: `Ctrl+Shift+P` → *Claude Code: Open*.

> **TIP:** On Windows, set Git Bash or WSL as the default terminal in VSCode (Settings → Terminal → Default Profile) before opening Claude Code. The extension requires a Unix-compatible shell.

### 3.3 Authentication

```bash
claude auth login     # opens browser for OAuth
claude auth status    # confirm session is active
```

> **INFO:** For CI/CD or remote servers, use an API key via the `ANTHROPIC_API_KEY` environment variable instead of browser-based login.

### 3.4 Monitoring API Usage & Costs

| Command | Purpose |
|---|---|
| `/usage` | Show total token usage for the current session |
| `ccusage` | Extended usage report across sessions |
| `session/cost` | Estimate monetary cost of the current session |

> **WARNING:** Large context loads can consume tokens quickly. Always check `/usage` before and after major operations, and use `/compact` to summarise history when context grows long.

---

## 4. Project Folder Structure

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

```bash
claude /init    # generates CLAUDE.md and scaffolds project
```

### 4.2 Example CLAUDE.md for Research

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

| File | Location & Purpose |
|---|---|
| `CLAUDE.md` | Project root — auto-read by Claude Code every session. Must not be moved. |
| `plan.md` | Project root — referenced in session prompts. |
| `progress.md` | Project root — running audit trail. |
| `.claude/settings.json` | Auto-created by Claude Code — permissions and MCP config. |
| `.claude/settings.local.json` | Machine-specific overrides — add to `.gitignore`. |

> **WARNING:** `CLAUDE.md` must stay in the project root. Claude Code's automatic project-context loading only works from there. A misplaced `CLAUDE.md` means every session starts without project context.

---

## 5. Git & GitHub Integration

### 5.1 Connecting to GitHub

```bash
git init
git remote add origin https://github.com/yourusername/your-project.git
git branch -M main
git push -u origin main
git pull origin main   # run at start of every session
```

### 5.2 Git Workflow for Research Sessions

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

Overleaf supports two-way GitHub sync. Set it up once, then maintain with a pull/push rhythm each session.

#### Step 1: Create GitHub Repo from Overleaf

In Overleaf: *Menu* → *GitHub* → *Create a GitHub repository*.

#### Step 2: Add as Git Subtree

```bash
git remote add overleaf https://github.com/yourusername/paper-repo.git
git subtree add --prefix=latex overleaf main --squash
```

#### Session Rhythm with Overleaf

| # | Step | Command |
|---|---|---|
| 1 | Pull paper from Overleaf | `git subtree pull --prefix=latex overleaf main --squash` |
| 2 | Pull project from GitHub | `git pull origin main` |
| 3 | Run Claude Code session | `claude` |
| 4 | Commit all changes | `git add -A && git commit` |
| 5 | Push project to GitHub | `git push origin main` |
| 6 | Push paper to Overleaf | `git subtree push --prefix=latex overleaf main` |

> **WARNING:** Always pull from Overleaf before pushing back. Never push without pulling first.

---

## 6. Settings Architecture & Permissions

### 6.1 Settings Hierarchy

| Level | File & Scope |
|---|---|
| Organization | Managed by Anthropic / enterprise admin |
| User | `~/.claude/settings.json` |
| Project | `.claude/settings.json` (committed to repo) |
| Local | `.claude/settings.local.json` (NOT committed) |

### 6.2 Tool-Based Access Controls

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

MCP (Model Context Protocol) servers extend Claude Code's capabilities by giving it access to external tools and services. Think of each MCP server as a plugin that lets Claude talk to a different system.

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

| Transport | Configuration |
|---|---|
| URL / SSE (remote) | Provide `url` field only |
| npx (npm package) | Use `command: npx` with `args: ["-y", "@pkg/name"]` |
| Python / uvx | Use `command: uvx` or `python -m package` |

> **WARNING:** Before installing any third-party MCP server: check recent commits, verify tool scope in the README, and never grant broader permissions than the server needs.

---

## 7. Context Engineering

### 7.1 The 5–10 Turn Session Rule

Limit each session to a single, well-defined task. Never run data cleaning, simulation, and LaTeX tasks in the same conversation — context contamination degrades all three.

### 7.2 Compacting Context

```
/compact
```

Run proactively after completing a major task, not reactively when context is already overloaded.

### 7.3 plan.md and progress.md — Your External Memory

#### plan.md — The Session Blueprint

Five required components:

| Component | What to Write and Why |
|---|---|
| Date and session title | Cross-reference with progress.md and Git commits |
| Single clear goal | One sentence. If you cannot state it in one sentence, split the session. |
| Numbered steps | Exact sequence of actions for Claude |
| Do NOT list | Files not to touch, analyses not to run |
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

```
Please read CLAUDE.md, plan.md, and progress.md in that order.
Then confirm your understanding of today's goal and begin Step 1.
```

#### progress.md — The Persistent Audit Trail

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

### 10.1 The Data Download Script Pattern

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

> **TIP:** Always save raw data with a timestamp in the filename (e.g., `primary_data_20250115.csv`). This lets you trace which data vintage was used in each paper version.

---

## 11. Publication-Quality Figures: Healy Style Guide

| Principle | Application |
|---|---|
| Show the data | Plot observations, not just means |
| Data-ink ratio | Remove non-informative gridlines and borders |
| Intentional colour | Reserve colour for categorical distinctions |
| Label directly | Annotate lines/bars; avoid legends where possible |
| Consistent typography | One sans-serif font throughout all figures |
| Honest scales | Never truncate y-axes |
| Declarative titles | "Group B pays 38% above cost" not "Figure 3: Shares" |

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

A subagent is a pre-configured, narrowly scoped AI assistant that runs in its own isolated context window. The main session only receives the final summary — all intermediate work stays inside the subagent and never pollutes the main context.

### 12.1 Built-in Subagents

| Agent | Purpose |
|---|---|
| Explore | Read-only codebase search. Activated automatically when Claude needs to scan files. |
| Plan | Research agent for plan mode. Gathers codebase context before presenting a plan. |
| General-purpose | Multi-step tasks requiring both exploration and action. |

### 12.2 The .claude/agents/ Folder

| Location | Scope |
|---|---|
| `.claude/agents/*.md` | Project-level, committed to Git, shared with team |
| `~/.claude/agents/*.md` | User-level, available across all projects |

### 12.3 Subagent File Format

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

1. **Interactive:** type `/agents` inside a session → Create new agent.
2. **Manual file:** create `.claude/agents/your-agent.md` with the format above.
3. **Inline (temporary):** pass `--agents '{...}'` when launching `claude`.

### 12.5 Invoking Agents

```
# Explicit invocation (recommended for important tasks)
Use the data-auditor agent to verify data/raw/source_data.csv

# Background execution
Ctrl+B   ← send agent to background, keep typing
```

### 12.6 Ready-to-Use Research Agent: Literature Reviewer

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

| Principle | Guidance |
|---|---|
| Single responsibility | One agent, one task. Never mix research and modification. |
| Structured output | Specify exact format: JSON, markdown table, named sections. |
| Least-privilege tools | Grant only what the agent genuinely needs. |
| Clear description | Use `PROACTIVELY` for auto-delegation. Be specific about trigger. |

> **WARNING:** Subagents cannot spawn other subagents. Do not instruct an agent to "call the X agent." Orchestrate multi-agent workflows from the main session only.

---

## 13. Installing Third-Party Agents

### 13.1 Finding Community Agents

- **github.com/VoltAgent/awesome-claude-code-subagents** — 100+ curated agents
- GitHub search: `claude code subagents` or `.claude/agents`
- **glama.ai/mcp/servers** — rated registry with install instructions

### 13.2 Installation Methods

#### Method A: Manual Copy

```bash
# Project scope
touch .claude/agents/research-analyst.md
# paste contents from GitHub Raw view

# User scope (all projects)
touch ~/.claude/agents/research-analyst.md
```

#### Method B: Git Clone and Copy

```bash
git clone https://github.com/VoltAgent/awesome-claude-code-subagents.git
ls awesome-claude-code-subagents/agents/
cp agents/research-analyst.md .claude/agents/
cp agents/data-researcher.md  .claude/agents/
```

#### Method C: Install Script

```bash
curl -sO https://raw.githubusercontent.com/VoltAgent/\
awesome-claude-code-subagents/main/install-agents.sh
chmod +x install-agents.sh && ./install-agents.sh
```

### 13.3 Evaluation Checklist Before Installing

1. **Tool permissions:** read the `tools:` field. Research agents should not need `Write` or `Bash`.
2. **System prompt clarity:** specific, bounded, with a defined output format.
3. **Description trigger:** will not activate unexpectedly on unrelated tasks.
4. **Repository activity:** committed within the last 12 months.

> **WARNING:** Never install a `Bash`-enabled agent from an untrusted source without reading every line of the system prompt.

### 13.4 Verifying Installation

```
/agents    ← list all loaded agents
/status    ← confirm agent appears in session state

Use the research-analyst agent to give me a two-sentence
overview of [your research topic].
```

> **TIP:** If an agent fails to load, paste the YAML frontmatter into [yamllint.com](https://yamllint.com). Common errors: missing closing `---`, tab characters, colons in unquoted strings.

---

## 14. The Knowledge Management Stack: Zotero, Obsidian, NotebookLM & Claude Code

This section describes a powerful, integrated workflow for managing research knowledge across multiple papers and topics over time. It combines four tools — Zotero, Obsidian, NotebookLM, and Claude Code — each doing what it does best.

The core idea comes from Andrej Karpathy (former OpenAI, Tesla AI Director), who described shifting a large fraction of his LLM usage from writing code to **manipulating knowledge stored as markdown files**. The mental shift is simple but profound: instead of using Claude as a chatbot you ask questions and forget, you use it as a **compiler and librarian** that builds a persistent, compounding knowledge base on your behalf. Moreover, 
Alexandra Phelan's ideas have been helpful in preparing this section [https://medium.com/@alexandraphelan/an-updated-academic-workflow-zotero-obsidian-cffef080addd](https://medium.com/@alexandraphelan)

### 14.1 Why This Approach Matters for Researchers

Most researchers' experience with AI follows a frustrating pattern: you ask a question, get a good answer, close the tab, and lose everything. The next week you start from scratch. Nothing accumulates.

The approach described here is different. It is **stateful and compounding**:

- Today's answer becomes tomorrow's context.
- Every paper you read adds a permanent, cross-referenced entry to your wiki.
- Your own analyses and queries file back into the knowledge base and improve future queries.
- Six months of work results in a private corpus your LLM can read in a single context window.

For energy economics researchers, this means your knowledge about electricity market mechanisms, capacity auction designs, renewable integration challenges, and empirical findings across regions never disappears — it compounds.

### 14.2 The Four Layers

The stack has four distinct layers, each with a specific role:

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

Zotero is your primary reference manager. It stores all paper metadata, PDFs, and annotations, and generates consistent citation keys for use in manuscripts.

#### Step 1 — Install Zotero

Download from [zotero.org](https://www.zotero.org/). It is free and works on Windows, macOS, and Linux. Install the browser connector (available for Chrome, Firefox, Edge) — this allows you to save any academic paper or web article to your Zotero library with one click.

#### Step 2 — Install the BetterBibTeX Plugin

BetterBibTeX (BBT) is essential. It creates consistent, predictable citation keys (called citekeys) in the format `Author_YYYY` (e.g., `Borenstein_2002`, `Joskow_2019`). These same citekeys are used when you cite papers in Obsidian and LaTeX.

1. Download the latest `.xpi` file from [retorque.re/zotero-better-bibtex](https://retorque.re/zotero-better-bibtex/).
2. In Zotero: *Tools* → *Add-ons* → gear icon → *Install Add-on From File* → select the `.xpi`.
3. Restart Zotero. Go to *Edit* → *Preferences* → *Better BibTeX* to configure the citekey format.

Recommended citekey format: `[auth:lower]_[year]` (produces `borenstein_2002`).

#### Step 3 — Export Your Library as a .bib File

This `.bib` file is what Obsidian (via Pandoc) and Claude Code use to resolve citations.

In Zotero: *File* → *Export Library* → Format: **Better BibTeX** → check **Keep Updated** → save to a stable path such as `~/Documents/MyLibrary.bib`.

The "Keep Updated" option ensures the file refreshes automatically as you add new papers.

#### Step 4 — Annotate PDFs Inside Zotero

Since Zotero 6, you can read and annotate PDFs directly inside the app. Use a colour coding system to communicate different annotation types:

| Colour | Meaning (suggested) |
|---|---|
| 🟡 Yellow | Interesting point or key finding |
| 🔴 Red | Critical claim / point of disagreement |
| 🟢 Green | Methodology note |
| 🔵 Blue | Relevant to your specific research question |

These annotations are later pulled into Obsidian Literature Notes automatically.

### 14.4 Setting Up Obsidian

Obsidian is where your knowledge actually lives. Think of it not as a note-taking app, but as a **knowledge IDE** — a place where you can browse, navigate, and visualise everything you know about a topic.

#### Step 1 — Install Obsidian

Download from [obsidian.md](https://obsidian.md/). It is free for personal use, runs entirely on your local machine, and stores all data as plain `.md` files (so nothing is locked into a proprietary format).

#### Step 2 — Create Your Vault with the Research Folder Structure

A "vault" is just a folder on your computer. Create it with this structure:

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

> **TIP:** In Obsidian Settings → Files and links, set the **Attachment folder path** to `raw/assets/`. Then bind a hotkey to "Download attachments for current file" (Settings → Hotkeys, search "Download"). After clipping an article, press the hotkey to save all images locally so Claude can reference them.

#### Step 3 — Install the Obsidian Web Clipper

Install the [Obsidian Web Clipper](https://obsidian.md/clipper) browser extension. When you find an article or report online, click the extension to save a clean `.md` version — with URL, title, date, and tags — directly into your vault's `raw/` folder. This is the primary way you get content into the system.

#### Step 4 — Install Essential Obsidian Plugins

Go to Settings → Community Plugins → Browse. Install and enable these:

| Plugin | Purpose |
|---|---|
| **Zotero Integration** | Pulls Zotero paper metadata and PDF annotations into Literature Notes |
| **Pandoc Reference List** | Shows a formatted reference list for citekeys in the current document |
| **Dataview** | Queries your notes like a database; used to build summary tables |
| **Pandoc** | Exports manuscripts to `.docx` with processed citations |

#### Step 5 — Configure Zotero Integration

In Obsidian Settings → Zotero Integration:

1. Set the **Citation format** to Pandoc (produces `[@Author_Year]` citekeys).
2. Point **BibTeX path** to the `.bib` file you exported from Zotero.
3. Create a Literature Note template (see Section 14.6 below).

#### Step 6 — Enable Graph View

Obsidian's graph view (accessible from the ribbon on the left) shows all your notes as nodes, with bidirectional links as edges. As your wiki grows, you will start to see clusters of knowledge form — and you can identify isolated nodes (gaps in your knowledge) at a glance. Use this regularly to guide your research.

### 14.5 Setting Up NotebookLM

NotebookLM (by Google) is a synthesis engine. While Claude Code is ideal for one-at-a-time, carefully curated ingestion of sources, NotebookLM is useful when you need to process a large batch of materials at once — for example, at the start of a new research project when you have 20+ papers to review.

#### What NotebookLM Does Best

- Ingests many sources simultaneously (PDFs, URLs, Google Docs, YouTube transcripts).
- Produces a **Writing Standards Manual** or structured narrative summary of all sources combined.
- Generates audio overviews (podcast-style dialogue) for quick orientation.
- Answers questions grounded in your specific sources, with citations.

#### How to Use It in Your Workflow

1. Go to [notebooklm.google.com](https://notebooklm.google.com/) and create a new notebook.
2. Add your sources: paste URLs of journal articles, upload PDFs, or add YouTube lecture URLs.
3. In the Studio panel, ask NotebookLM to produce a **comprehensive synthesis document** covering the key themes, findings, and debates across all sources.
4. Save the output as a `.md` file and place it in your `raw/` folder.
5. From there, instruct Claude Code to ingest it into your wiki as a high-level overview article.

> **TIP:** NotebookLM is particularly useful at the **start of a new sub-topic** within your research. Use it to get oriented quickly across 20–40 sources. Use Claude Code for the ongoing, incremental maintenance of your wiki from that point forward.

#### Connecting NotebookLM Output to Claude Code

Once NotebookLM has produced a synthesis document, you can feed it directly to Claude Code:

```bash
claude -p "I've added a new synthesis document to /raw/notebooklm-synthesis-capacity-markets.md.
Read it, identify the 5-10 most important concepts it covers, and create or update
concept pages in /wiki/concepts/ for each. Update /wiki/index.md accordingly.
Show me every file you touched." --allowedTools Bash,Write,Read
```

### 14.6 Creating Zotero Literature Notes in Obsidian

A Literature Note is a single Obsidian note for each paper in your Zotero library. It contains the full metadata, a link back to Zotero, and all your PDF annotations automatically imported.

#### The Literature Note Template

Create a new note in Obsidian at `literature-notes/_template.md` with the following content. (Note: copy-paste into a plain text editor first to strip any hidden formatting.)

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

In Zotero Integration settings, click **Add Import Format** → set the template path to the file above.

#### Creating a Literature Note

Press `Cmd+P` (macOS) or `Ctrl+P` (Windows/Linux) to open the Obsidian command palette → type **Zotero Integration: Create Literature Note** → search for your paper. The note is generated automatically with all metadata and annotations.

#### Citation Convention

The setup creates a clean distinction between a citation and a link to the Literature Note, using the same citekey:

- `[@Borenstein_2002]` — inline Pandoc citation (used in manuscript text)
- `[[@Borenstein_2002]]` — Obsidian internal link to the Literature Note

This means every paper you cite in a manuscript has a corresponding Literature Note you can navigate to directly from the text.

### 14.7 Setting Up the Claude Code + Obsidian Connection via MCP

You can connect Claude Code directly to your Obsidian vault using an MCP server, allowing Claude to read and write notes in real time without any copy-paste.

The most reliable option is **mcp-obsidian**, which works via the Obsidian Local REST API plugin.

#### Step 1 — Install the Local REST API Plugin in Obsidian

In Obsidian: Settings → Community Plugins → Browse → search **Local REST API** → Install and Enable. Copy the API key shown in the plugin's settings panel.

#### Step 2 — Add the MCP Server Configuration

Open the Claude Desktop config file:

- **macOS:** `~/Library/Application Support/Claude/claude_desktop_config.json`
- **Windows:** `%APPDATA%/Claude/claude_desktop_config.json`

Add this block (replace `<your_api_key_here>` with the key from Step 1):

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

Restart Claude Desktop.

> **WARNING:** Obsidian must be open and running while you use this MCP connection. The Local REST API plugin only operates while the vault is active.

#### Step 3 — Verify the Connection

In a Claude chat window, type: `Use Obsidian to list files in my vault.` If the connection works, Claude will return a list of your vault's files.

#### What Claude Can Do with Your Vault via MCP

| Operation | Example Prompt |
|---|---|
| Browse vault structure | "List all files in my wiki/ folder" |
| Read a specific note | "Read the file wiki/concepts/capacity-markets.md" |
| Search across notes | "Find all notes mentioning 'merit order effect'" |
| Add content under a heading | "Add this summary under the #Findings heading in my note on Joskow_2019" |
| Append to a note | "Append today's reading notes to raw/notes-2026-04-15.md" |
| Create new wiki pages | "Create a new wiki page for the concept of 'scarcity pricing'" |

### 14.8 The Daily Workflow: Putting It All Together

Here is what an integrated research day looks like with this stack operating smoothly:

**Morning — Capture**

1. Browse journals, X/Twitter, or news. Use the Obsidian Web Clipper to save anything interesting directly to `raw/`. Do not organise — just capture.
2. For new academic papers, add them to Zotero via the browser connector. Generate Literature Notes for the ones you read.

**During Reading — Annotate**

3. Read PDFs inside Zotero, using colour-coded highlights. Add notes in the margin for key ideas.
4. After reading, run "Zotero Integration: Create Literature Note" in Obsidian to pull all annotations in.

**Processing — Compile the Wiki**

5. Open Claude Code in VSCode, pointing at your vault folder. Run an ingest command:

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

6. Ask complex questions against your wiki:

```bash
claude -p "Using only my wiki in /wiki/, write a 500-word synthesis of
what I know about the relationship between renewable energy penetration
and electricity price volatility. Save the output to /reports/synthesis-renewables-volatility.md
and link it from the relevant concept pages." --allowedTools Bash,Write,Read
```

**Weekly — Lint the Wiki**

7. Once a week, run a health check:

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

The most important file in your vault is `CLAUDE.md` — placed at the vault root. This file is the **operating manual** for Claude. It tells Claude exactly how your wiki is structured, what the conventions are, and what to do when ingesting a new source or answering a query.

Without this file, every Claude session starts cold. With a well-maintained `CLAUDE.md`, every session begins with full understanding of your knowledge base.

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

To make this concrete, here is what the setup looks like for a researcher studying capacity market design in the Gulf.

After setting up the vault and running the stack for one month, the `wiki/concepts/` folder might contain files such as:

- `capacity-market-design.md` — synthesis of 12 papers on auction mechanisms
- `scarcity-pricing.md` — definition, examples from ERCOT, Texas literature
- `merit-order-effect.md` — empirical evidence across 8 country studies
- `renewable-curtailment.md` — causes, measurement, mitigation strategies
- `voll-estimation.md` — methodological notes from three empirical papers

When you then ask: *"What does my research say about the relationship between capacity adequacy metrics and renewable curtailment in markets with high solar penetration?"*, Claude reads the relevant pages and synthesises an answer that draws on everything you have read — in seconds, with full citations — and saves the report to `reports/` for reuse.

---

## 15. AI Paradigms for Research (Korinek, 2025)

*Based on: Korinek, A. (2025). AI Agents for Economic Research. NBER Working Paper No. 34202. Online resources: [GenAIforEcon.org](https://www.GenAIforEcon.org).*

| Paradigm | Best For |
|---|---|
| Traditional LLMs | Drafting, summarising, editing, LaTeX formatting |
| Reasoning Models | Mathematical derivations, formal proofs, complex code debugging |
| Agentic Chatbots | End-to-end workflows: data download → analysis → figures → narrative |

### 15.1 Tool Budget

$20/month is enough to start. $200/month unlocks meaningfully faster iteration — treat it as a human-capital investment.

---

## 16. Critical Limitations & Responsible Oversight

| Failure Mode | Mitigation |
|---|---|
| Hallucinations | Verify every citation; trace every statistic to its source |
| Cascading errors | Human checkpoints between pipeline stages |
| Prompt brittleness | Version prompts in CLAUDE.md and plan.md |
| Economic reasoning errors | Expert review of all theoretical content; use agent for structure, not intellectual core |
| Cost escalation | Monitor `/usage`; prefer focused single-agent sessions |
| Wiki drift | Run the weekly lint pass; do not let the knowledge base grow unchecked |
| Stale knowledge | The LLM's training has a cutoff; always check dates on claims about recent market events |

> **TIP:** Mental model: treat Claude Code like a team of capable research assistants who require clear instructions, oversight during execution, and careful vetting of outputs. An LLM that is uncertain does not say so — it hallucinates confidently. Your domain expertise is the final quality gate.

---

## 17. Best Practices Summary

| Practice | Why It Matters |
|---|---|
| Always pull before starting | Avoids stale code and merge conflicts |
| Write CLAUDE.md thoroughly | Eliminates re-explaining project context |
| Use plan.md + progress.md | Creates external memory across sessions |
| 5–10 turn focused sessions | Preserves context quality |
| Commit after every session | Provides rollback points and audit trail |
| Save figures as PDF + PNG | PDF for LaTeX, PNG for quick preview |
| Run /compact proactively | Prevents context overflow |
| Timestamp all raw data files | Enables reproducibility and version tracing |
| Plan before coding | Reveals wrong assumptions early |
| One task per session | Prevents context contamination |
| Keep vault CLAUDE.md current | Every session starts with full context |
| Run weekly wiki lint | Prevents knowledge base from drifting |
| File query outputs back into wiki | Insights compound; nothing is lost to chat history |
| Use NotebookLM for batch ingestion | Efficient for large reading lists; use Claude Code for incremental maintenance |

---

## 18. Troubleshooting

| Issue | Resolution |
|---|---|
| Claude ignores CLAUDE.md | Explicitly reference: "Please read CLAUDE.md before starting" |
| Context quality degrades | Run `/compact` or start fresh session with summary |
| MCP server not responding | Check `/status`; verify URL and API key in settings.json |
| Agent fails to load | Validate YAML frontmatter at yamllint.com |
| Git merge conflicts | Commit before each session; one branch per session |
| Token costs spike | Avoid loading large files directly; sample or summarise first |
| Web fetch blocked | Add domain to allow list in settings.json |
| PowerShell execution error | `Set-ExecutionPolicy -Scope CurrentUser RemoteSigned` |
| Obsidian MCP not connecting | Check that Obsidian is open; verify Local REST API plugin is enabled and API key matches |
| Zotero Integration parse error | Copy template into Notepad first to remove hidden formatting, then paste into Obsidian |
| `code` command not found (macOS) | Run Shell Command: Install 'code' command in PATH from VSCode command palette |
| `uvx` not found for MCP | Run `which uvx` in terminal; paste the full path into the `command` field in claude_desktop_config.json |
| Claude writes to raw/ folder | Review and tighten the vault CLAUDE.md schema — specify that raw/ is read-only |

---

*End of Implementation Guide*

*SMS | Claude Code for Research*
*Based on Korinek (2025) NBER WP 34202, Karpathy (2026) LLM Knowledge Bases, Phelan (2023) Zotero & Obsidian Workflow, and AI MBA Webinar Series*
