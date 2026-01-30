# CLAUDE.md

This file is loaded automatically by Claude Code at the start of every session. It contains coding guidelines, tool preferences, and setup instructions.

## Setup

### Install everything-claude-code plugin

This repo includes [everything-claude-code](https://github.com/affaan-m/everything-claude-code) as a submodule — a battle-tested collection of agents, skills, hooks, commands, rules, and MCP configs for Claude Code.

**Option A: Plugin install (recommended)**

```
/plugin marketplace add affaan-m/everything-claude-code
/plugin install everything-claude-code@everything-claude-code
```

**Option B: Manual install**

```bash
cp everything-claude-code/agents/*.md ~/.claude/agents/
cp everything-claude-code/rules/*.md ~/.claude/rules/
cp everything-claude-code/commands/*.md ~/.claude/commands/
cp -r everything-claude-code/skills/* ~/.claude/skills/
```

Rules must be copied manually regardless of install method:

```bash
cp -r everything-claude-code/rules/* ~/.claude/rules/
```

---

## Coding Guidelines (Karpathy)

Behavioral guidelines to reduce common LLM coding mistakes, derived from [Andrej Karpathy's observations](https://x.com/karpathy/status/2015883857489522876).

**Tradeoff:** These guidelines bias toward caution over speed. For trivial tasks, use judgment.

### 1. Think Before Coding

**Don't assume. Don't hide confusion. Surface tradeoffs.**

- State your assumptions explicitly. If uncertain, ask.
- If multiple interpretations exist, present them - don't pick silently.
- If a simpler approach exists, say so. Push back when warranted.
- If something is unclear, stop. Name what's confusing. Ask.

### 2. Simplicity First

**Minimum code that solves the problem. Nothing speculative.**

- No features beyond what was asked.
- No abstractions for single-use code.
- No "flexibility" or "configurability" that wasn't requested.
- No error handling for impossible scenarios.
- If you write 200 lines and it could be 50, rewrite it.

Ask yourself: "Would a senior engineer say this is overcomplicated?" If yes, simplify.

### 3. Surgical Changes

**Touch only what you must. Clean up only your own mess.**

When editing existing code:
- Don't "improve" adjacent code, comments, or formatting.
- Don't refactor things that aren't broken.
- Match existing style, even if you'd do it differently.
- If you notice unrelated dead code, mention it - don't delete it.

When your changes create orphans:
- Remove imports/variables/functions that YOUR changes made unused.
- Don't remove pre-existing dead code unless asked.

The test: Every changed line should trace directly to the user's request.

### 4. Goal-Driven Execution

**Define success criteria. Loop until verified.**

Transform tasks into verifiable goals:
- "Add validation" → "Write tests for invalid inputs, then make them pass"
- "Fix the bug" → "Write a test that reproduces it, then make it pass"
- "Refactor X" → "Ensure tests pass before and after"

For multi-step tasks, state a brief plan:
```
1. [Step] → verify: [check]
2. [Step] → verify: [check]
3. [Step] → verify: [check]
```

---

## Preferred Command-Line Tools

This machine has modern alternatives to traditional Unix tools installed. ALWAYS prefer using them over the traditional ones unless there's a strong reason not to.

### Search Tools

- **ripgrep (`rg`)** instead of `grep`:
  - Faster recursive search with smart defaults
  - Automatically respects `.gitignore`
  - Example: `rg "pattern"` instead of `grep -r "pattern"`

- **fd** instead of `find`:
  - Faster file search with intuitive syntax
  - Respects `.gitignore` by default
  - Example: `fd "filename"` instead of `find . -name "filename"`

### Available Tools

**GitHub**: `gh` - always use for GitHub operations (PRs, issues, repos, actions, API)

**File viewing**:
- `bat` - syntax-highlighted cat
- `eza` - modern ls with git integration
- `glow` - render markdown in terminal

**Data processing**:
- `jq` - JSON processor
- `yq` - YAML processor (same syntax as jq)

**Search & selection**:
- `rg` (ripgrep) - fast grep
- `fd` - fast find
- `fzf` - fuzzy finder for interactive selection

**Git**:
- `delta` - better diff viewer
- `lazygit` - TUI for complex git operations

**System**:
- `duf` - disk usage (modern df)
- `ncdu` - interactive disk usage explorer
- `hyperfine` - benchmarking

**HTTP**: `http` / `https` (httpie) - user-friendly curl alternative

**File watching**: `entr` - run commands when files change (e.g., `ls *.py | entr pytest`)

**macOS**: `pbcopy`/`pbpaste` (clipboard), `open` (open files/URLs/apps)

**Note**: When asked to "copy" something, pipe it through `pbcopy` to put it on the clipboard.
