# Reconstruct — Claude Code plugin (releases)

This repository is the **Claude Code plugin marketplace** for Reconstruct: a small catalog ([`.claude-plugin/marketplace.json`](./.claude-plugin/marketplace.json)) plus the **`reconstruct`** plugin under [`plugins/reconstruct/`](./plugins/reconstruct/).

In the **[reconstruct](https://github.com/blkinnovate/reconstruct)** monorepo, this project is linked as a **git submodule** at `reconstruct-claude-plugin/`. Clone the monorepo with **`git clone --recurse-submodules`**, or after a normal clone run **`git submodule update --init --recursive`**.

## Users

**VS Code / GitHub Copilot Agent plugins** use the separate **[reconstruct-copilot-plugin](https://github.com/blkinnovate/reconstruct-copilot-plugin)** repo (this marketplace layout is for Claude Code only; cloning this repo for VS Code does not expose a root **`plugin.json`** the way Copilot expects).

1. In Claude Code: **`/plugin marketplace add blkinnovate/reconstruct-claude-plugin`**
2. Then: **`/plugin install reconstruct@reconstruct-plugins`** (user scope is default), or use **`reconstruct install --assistant claude`** from [reconstruct-cli](https://github.com/blkinnovate/reconstruct/tree/main/reconstruct-cli), which runs the same flow and writes your **`.mcp.json`** credentials into the plugin cache.

Docs: [Claude Code — plugin marketplaces](https://code.claude.com/docs/en/plugin-marketplaces), [Discover and install plugins](https://code.claude.com/docs/en/discover-plugins).

## Maintainers — keep marketplace and CLI bundle aligned

- **Marketplace source:** `plugins/reconstruct/` in **this** repository (what Claude Code loads from GitHub).
- **npm CLI bundle:** `reconstruct-cli/bundled/reconstruct-claude-plugin/` in the monorepo (shipped inside `reconstruct-cli`).

Those two trees should stay identical when you cut a release. Typical workflow:

1. Edit the plugin in **this repo** (or edit the bundle in the monorepo, then copy—see below).
2. Commit and push **this** repository.
3. In the monorepo, **`cd reconstruct-claude-plugin && git pull`** (or **`git submodule update --remote`**) and commit the updated submodule pointer on your branch.

**Copy from monorepo bundle into this repo** (when the bundle was changed first):

```bash
# From the reconstruct monorepo root (submodule checkout)
rm -rf reconstruct-claude-plugin/plugins/reconstruct/*
cp -R reconstruct-cli/bundled/reconstruct-claude-plugin/. reconstruct-claude-plugin/plugins/reconstruct/
cd reconstruct-claude-plugin && git add -A && git commit -m "sync plugin from cli bundle" && git push
cd .. && git add reconstruct-claude-plugin && git commit -m "chore: bump reconstruct-claude-plugin submodule"
```

**Copy from this repo into the monorepo bundle** (after you released here):

```bash
rm -rf reconstruct-cli/bundled/reconstruct-claude-plugin/*
cp -R reconstruct-claude-plugin/plugins/reconstruct/. reconstruct-cli/bundled/reconstruct-claude-plugin/
```

## Marketplace id

- **Marketplace name:** `reconstruct-plugins`
- **Plugin install spec:** `reconstruct@reconstruct-plugins`
