# dot-claude

Personal Claude Code configuration and guidelines.

## Contents

### CLAUDE.md

The main config file — automatically loaded by Claude Code at session start. Contains:

- **Setup instructions** for installing the everything-claude-code plugin
- **Karpathy coding guidelines** — four principles (think first, simplicity, surgical changes, goal-driven execution) derived from [Andrej Karpathy's observations](https://x.com/karpathy/status/2015883857489522876)
- **Preferred CLI tools** — modern alternatives (`rg`, `fd`, `bat`, `eza`, `jq`, `delta`, etc.)

### everything-claude-code (submodule)

A git submodule tracking [affaan-m/everything-claude-code](https://github.com/affaan-m/everything-claude-code) — agents, skills, hooks, commands, rules, and MCP configs for Claude Code.

## Installation

#### Install as Plugin (Recommended)
</br>

**Add this repo as a marketplace**
```
/plugin marketplace add affaan-m/everything-claude-code
```
**Install the plugin**
```
/plugin install everything-claude-code@everything-claude-code
```
---

**TODO**

 - [ ]  Install the plugin to claude code.

- [ ]   Add CLAUDE.md file to the project manually.

---

## Updating

```bash
git submodule update --remote everything-claude-code
```

## Cloning

```bash
git clone --recurse-submodules <repo-url>
```
