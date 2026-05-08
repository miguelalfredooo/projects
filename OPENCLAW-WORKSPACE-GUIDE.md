# OpenClaw Workspace & Agent Information Guide

This guide ensures all agent workspaces and project repositories follow OpenClaw conventions for consistency, portability, and proper configuration management.

## Quick Reference

| Type | Location | Purpose | Git? |
|------|----------|---------|------|
| **Agent Workspace** | `~/.openclaw/workspace-*` | Agent's home, memory, instructions | ✅ Private repo |
| **Project Repository** | `/Users/blackmachete/projects/*` | Code, docs, deliverables | ✅ Standard repo |
| **Config/Secrets** | `~/.openclaw/` (not in projects) | Auth, credentials, sessions | ❌ Never commit |

---

## Agent Workspaces

**Location:** `~/.openclaw/workspace-<name>`

Workspaces are the agent's home directory. They contain:

### Required Files
```
AGENTS.md        # Operating instructions for this agent
SOUL.md          # Persona, tone, values
USER.md          # User/stakeholder context
IDENTITY.md      # Name, vibe, emoji
TOOLS.md         # Local tool conventions
HEARTBEAT.md     # Latest status and updates
```

### Optional but Recommended
```
BOOT.md          # Startup checklist
BOOTSTRAP.md     # First-run ritual
MEMORY.md        # Curated long-term memory index
memory/          # Daily memory logs (YYYY-MM-DD.md)
skills/          # Workspace-specific skills
canvas/          # Canvas UI files
```

### What NOT to Put Here
- Config files (openclaw.json)
- Credentials or API keys
- Session transcripts
- Anything under ~/.openclaw/ structure

### Git Setup for Workspaces
Treat as **private repository** for backup:

```bash
cd ~/.openclaw/workspace-<name>
git init
git add AGENTS.md SOUL.md USER.md IDENTITY.md TOOLS.md HEARTBEAT.md memory/
git commit -m "Initialize workspace"
git remote add origin <private-repo-url>
git push -u origin main
```

---

## Project Repositories

**Location:** `/Users/blackmachete/projects/<project-name>`

Project repos contain code, configuration, and deliverables—NOT agent workspaces.

### Current Projects
- `openclaw-mission-control/` - OpenClaw infrastructure
- `patched-editorial/` - Bulletin-board project (contains nested bulletin-board git repo)
- `patched-editorial/projects/bulletin-board/` - Bulletin-board codebase

### Project Structure
```
projects/
├── project-name/
│   ├── README.md
│   ├── CLAUDE.md          # Project-specific instructions
│   ├── .gitignore
│   ├── .git/              # Standard git repo
│   └── [code, docs, deliverables]
```

### What Project Repos Can Contain
- ✅ Code and configuration
- ✅ Project documentation
- ✅ CLAUDE.md (per-project instructions)
- ✅ Nested git repositories (as submodules or full repos)
- ✅ Build/deployment artifacts

### What NOT to Put in Project Repos
- ❌ Agent workspace files (AGENTS.md, SOUL.md, etc.)
- ❌ Config files like openclaw.json
- ❌ Credentials, API keys, passwords
- ❌ ~/.openclaw/ structure or contents

---

## Workflow: Workspace ↔ Project Sync

### Updating Agent Instructions from Project
When project (e.g., bulletin-board) needs agent updates:

1. **Edit** project files (e.g., `/projects/patched-editorial/projects/bulletin-board/AGENT-ROLE-INSTRUCTIONS.md`)
2. **Reference** from workspace (don't duplicate)
3. **Link** in workspace MEMORY.md: `- [Agent Role](../projects/patched-editorial/projects/bulletin-board/AGENT-ROLE-INSTRUCTIONS.md)`

### Workspace Context References
In workspace files, reference project locations explicitly:

```markdown
# workspace-bulletin-bot/AGENTS.md

Project location: /Users/blackmachete/projects/patched-editorial/projects/bulletin-board/
GitHub: https://github.com/miguelalfredooo/patched-bulletin-board.git
Key files:
- AGENT-ROLE-INSTRUCTIONS.md
- AGENT-ONBOARDING-ORDER.md
- SKILLS.md
```

---

## Current Setup Compliance

### ✅ Compliant
- `~/.openclaw/workspace-bulletin-bot/` - Proper workspace with all required files
- `~/.openclaw/workspace-bulletin-bot/AGENTS.md` - References bulletin-board project
- `/projects/patched-editorial/` - Code repository with nested bulletin-board
- `workspace-bulletin-bot` git repo - Private backup of workspace

### ⚠️ Archived (No longer active)
- `/projects/openclaw-artifacts/` - Moved to `~/.openclaw/workspace-artifacts/`
- `/bulletin-board/` (old) - Removed; use `patched-editorial/projects/bulletin-board/`

---

## Setup Checklist

When creating a new agent workspace:

- [ ] Create `~/.openclaw/workspace-<name>/`
- [ ] Create required files: AGENTS.md, SOUL.md, USER.md, IDENTITY.md, TOOLS.md, HEARTBEAT.md
- [ ] Create optional files: BOOT.md, BOOTSTRAP.md, MEMORY.md
- [ ] Create directories: memory/, skills/
- [ ] Initialize private git repo for backup
- [ ] Add reference to project location in AGENTS.md or MEMORY.md
- [ ] Add remote: `git remote add origin <private-repo-url>`
- [ ] First push: `git push -u origin main`

When creating a new project repository:

- [ ] Create `/projects/<project-name>/`
- [ ] Initialize `git init` (standard repo, not workspace)
- [ ] Add README.md, .gitignore
- [ ] Add CLAUDE.md for Claude Code instructions (optional)
- [ ] Store credentials in `.env.example` (never commit real .env)
- [ ] Do NOT add workspace files (AGENTS.md, SOUL.md, etc.)
- [ ] Link workspace references if related to agents

---

## Reference

**OpenClaw Documentation:** https://docs.openclaw.ai/

**Key Concepts:**
- **Workspace** = Agent's home and memory (private, backed up in git)
- **Project** = Code repository (standard git, can be public or private)
- **Config** = Lives in ~/.openclaw/ (never versioned, secure)
- **Sessions** = Stored in ~/.openclaw/agents/<agentId>/sessions/ (separate backup)

**Related:**
- HEARTBEAT.md - Status and updates for workspace
- SESSION - Session storage and management
- Standing orders - Persistent instructions in workspace files
