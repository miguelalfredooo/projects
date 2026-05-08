# Projects Monorepo Structure

This is a **monorepo** containing all project repositories as submodules.

## Structure

```
/Users/blackmachete/projects/
├── .gitmodules                          # Submodule configuration
├── OPENCLAW-WORKSPACE-GUIDE.md          # Workspace standards guide
├── PROJECTS-MAP.md                      # This file
│
├── openclaw-mission-control/            # OpenClaw Gateway infrastructure
│   └── https://github.com/abhi1693/openclaw-mission-control.git
│
├── openclaw-artifacts/                  # (Archived) moved to ~/.openclaw/workspace-artifacts/
│   └── https://github.com/miguelalfredooo/openclaw-artifacts.git
│
└── patched-editorial/                   # Bulletin-board project
    ├── .git → https://github.com/miguelalfredooo/patched-bulletin-board.git
    └── projects/bulletin-board/         # Nested bulletin-board codebase
        └── .git → https://github.com/miguelalfredooo/patched-bulletin-board.git
```

## Submodules

| Project | Remote | Purpose |
|---------|--------|---------|
| `openclaw-mission-control` | abhi1693/openclaw-mission-control | Gateway infrastructure |
| `openclaw-artifacts` | miguelalfredooo/openclaw-artifacts | (Archived - moved to workspace) |
| `patched-editorial` | miguelalfredooo/patched-bulletin-board | Bulletin-board project |

## Working with Submodules

### Clone with all submodules
```bash
git clone --recurse-submodules https://github.com/miguelalfredooo/projects.git
```

### Initialize submodules in existing clone
```bash
git submodule update --init --recursive
```

### Pull latest from all submodules
```bash
git submodule foreach git pull origin main
```

### Update a specific submodule
```bash
cd openclaw-mission-control
git pull origin main
cd ..
git add openclaw-mission-control
git commit -m "Update openclaw-mission-control submodule"
git push
```

## Nested Repos

⚠️ **Note:** `patched-editorial/projects/bulletin-board/` contains a nested git repo pointing to the same remote as its parent. This is for convenience—both repos track the same GitHub repository.

To keep them in sync:
```bash
# From projects/patched-editorial/
git pull origin main

# This updates both the parent repo and the nested bulletin-board
```

## Agent Workspaces

⚠️ Agent workspaces do NOT live in this projects folder. See [OPENCLAW-WORKSPACE-GUIDE.md](OPENCLAW-WORKSPACE-GUIDE.md) for workspace locations:
- Workspaces: `~/.openclaw/workspace-*`
- Example: `~/.openclaw/workspace-bulletin-bot/`

## Adding New Projects

To add a new project as a submodule:

```bash
git submodule add <remote-url> <project-name>
git add .gitmodules project-name/
git commit -m "Add <project-name> as submodule"
git push
```

Then update this PROJECTS-MAP.md with the new entry.

## Related Documentation

- [OPENCLAW-WORKSPACE-GUIDE.md](OPENCLAW-WORKSPACE-GUIDE.md) - Workspace and project standards
- [patched-editorial/README.md](patched-editorial/README.md) - Bulletin-board project details
