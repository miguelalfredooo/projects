# Project Aliases & Functions

Complete reference for all available aliases and functions in the projects monorepo.

**Setup:** Add to `~/.zshrc` or `~/.bashrc`:
```bash
source /Users/blackmachete/projects/.projects-setup
```

---

## Quick Jump Aliases

| Alias | Destination | Use Case |
|-------|-------------|----------|
| `bb` | `/projects/patched-editorial/projects/bulletin-board` | Primary work directory |
| `pb` | `/projects/patched-editorial` | Parent project (Telegram bot, deployment) |
| `projects` | `/Users/blackmachete/projects` | Monorepo root |
| `oc-artifacts` | `/projects/openclaw-artifacts` | Archived workspace reference |
| `oc-mission` | `/projects/openclaw-mission-control` | Gateway infrastructure |
| `brief` | `/projects/the-brief` | Agent briefs and identity docs |

---

## Status & Update Functions

### `projects-status`
Show git status for all projects at once.

```bash
$ projects-status
=== Projects Monorepo Status ===

📍 Main Monorepo:
[shows monorepo changes]

📦 Subprojects:
  patched-editorial:
  [shows patched-editorial changes]
  
  openclaw-artifacts:
  [shows openclaw-artifacts changes]
  
  openclaw-mission-control:
  [shows openclaw-mission-control changes]
```

**Use when:** You want to see everything that's changed across all projects

---

### `projects-update`
Pull latest from main monorepo and all submodules.

```bash
$ projects-update
=== Updating all projects ===
Updating main monorepo...
Updating submodules...
✅ All projects updated
```

**Use when:** You want to sync everything to latest from GitHub

---

### `projects-sync`
Commit and push current project changes back to monorepo.

```bash
$ bb
$ [edit files]
$ git add -A && git commit -m "My changes"
$ git push origin curator-integration
$ projects-sync
Syncing patched-editorial...
[commits submodule update to main monorepo]
```

**Use when:** You've pushed to a project and want to update the monorepo's submodule reference

---

## Documentation Functions

### `projects-help`
Display complete workflow guide and documentation.

```bash
$ projects-help
╔════════════════════════════════════════════════════════════════════════════╗
║                  PROJECTS MONOREPO WORKFLOW GUIDE                          ║
╚════════════════════════════════════════════════════════════════════════════╝
[shows full guide]
```

---

## Typical Workflow Example

```bash
# 1. Jump to bulletin-board (primary work)
$ bb
$ git status

# 2. Work on a branch
$ git checkout curator-integration
$ [edit files, test]
$ git add -A
$ git commit -m "Add feature X"
$ git push origin curator-integration

# 3. Update monorepo to track this
$ projects-sync

# 4. Check overall status
$ projects-status

# 5. Jump to another project if needed
$ oc-mission
$ git status
$ [work...]

# 6. Back to bulletin-board
$ bb

# 7. Before ending session, sync everything
$ projects-update
```

---

## Adding New Aliases

Edit `/Users/blackmachete/projects/.projects-setup` to add new aliases:

```bash
alias my-project='cd /Users/blackmachete/projects/my-project'
```

Then reload:
```bash
source ~/.zshrc
```

Update this `ALIASES.md` to document the new alias.

---

## Reference

- **Setup script:** `/Users/blackmachete/projects/.projects-setup`
- **Monorepo structure:** [PROJECTS-MAP.md](PROJECTS-MAP.md)
- **Workspace standards:** [OPENCLAW-WORKSPACE-GUIDE.md](OPENCLAW-WORKSPACE-GUIDE.md)
- **Primary project:** [patched-editorial/README.md](patched-editorial/README.md)

---

## Troubleshooting

**Aliases not working?**
```bash
# Make sure you've sourced the setup
source /Users/blackmachete/projects/.projects-setup

# Or add to ~/.zshrc permanently
echo 'source /Users/blackmachete/projects/.projects-setup' >> ~/.zshrc
source ~/.zshrc
```

**`projects-sync` fails?**
Make sure you're in a project directory and have committed changes:
```bash
$ pwd  # Verify location
$ git status  # Should show clean working tree
$ git push origin <branch>  # Push before sync
```

**Submodules out of sync?**
```bash
$ projects-update  # Pulls latest from all projects
$ projects-status  # Shows what's changed
```
