# Reconstruct — Claude Code plugin (releases)

This repository is the **Claude Code plugin marketplace** for Reconstruct: a small catalog ([`.claude-plugin/marketplace.json`](./.claude-plugin/marketplace.json)) plus the **`reconstruct`** plugin under [`plugins/reconstruct/`](./plugins/reconstruct/).

## Users

1. In Claude Code: **`/plugin marketplace add blkinnovate/reconstruct-claude-plugin`**
2. Then: **`/plugin install reconstruct@reconstruct-plugins`** (user scope is default), or use **`reconstruct install --assistant claude`** from [reconstruct-cli](https://github.com/blkinnovate/reconstruct/tree/main/reconstruct-cli), which runs the same flow and writes your **`.mcp.json`** credentials into the plugin cache.

Docs: [Claude Code — plugin marketplaces](https://code.claude.com/docs/en/plugin-marketplaces), [Discover and install plugins](https://code.claude.com/docs/en/discover-plugins).

## Maintainers — sync from the main repo

The canonical bundled copy used by **`npm install -g reconstruct-cli`** still lives in the monorepo at **`reconstruct-cli/bundled/reconstruct-claude-plugin/`**. Before tagging a release here, sync that tree into **`plugins/reconstruct/`** (replace contents) so the marketplace and the CLI bundle stay aligned.

```bash
# From the reconstruct monorepo root
rm -rf reconstruct-claude-plugin/plugins/reconstruct
cp -R reconstruct-cli/bundled/reconstruct-claude-plugin reconstruct-claude-plugin/plugins/reconstruct
```

Then commit, tag, and push this repository.

## Marketplace id

- **Marketplace name:** `reconstruct-plugins`
- **Plugin install spec:** `reconstruct@reconstruct-plugins`
