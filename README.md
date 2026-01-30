# dot-claude

Personal Claude Code configuration and guidelines.

## Contents

### karpathy-guidelines.md

Behavioral guidelines for LLM-assisted coding, derived from [Andrej Karpathy's observations](https://x.com/karpathy/status/2015883857489522876) on common LLM coding pitfalls. Covers four principles:

1. **Think Before Coding** — surface assumptions and tradeoffs before writing code
2. **Simplicity First** — minimum code that solves the problem, nothing speculative
3. **Surgical Changes** — only touch what the task requires
4. **Goal-Driven Execution** — define verifiable success criteria and loop until met

### everything-claude-code (submodule)

A git submodule tracking [affaan-m/everything-claude-code](https://github.com/affaan-m/everything-claude-code) — a comprehensive collection of Claude Code configs including agents, skills, hooks, commands, rules, and MCP configurations.

To use it, either install as a Claude Code plugin:

```
/plugin marketplace add affaan-m/everything-claude-code
/plugin install everything-claude-code@everything-claude-code
```

Or copy components manually into `~/.claude/`:

```bash
cp everything-claude-code/agents/*.md ~/.claude/agents/
cp everything-claude-code/rules/*.md ~/.claude/rules/
cp everything-claude-code/commands/*.md ~/.claude/commands/
cp -r everything-claude-code/skills/* ~/.claude/skills/
```

## Updating

Pull latest changes from the everything-claude-code upstream:

```bash
git submodule update --remote everything-claude-code
```

When cloning this repo on a new machine:

```bash
git clone --recurse-submodules <repo-url>
```
