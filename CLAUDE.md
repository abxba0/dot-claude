# CLAUDE.md

This file is loaded automatically by Claude Code at the start of every session. It contains coding guidelines and tool preferences.

---

## Project

<!-- Run `/init` in Claude Code to auto-populate this section with your codebase details. -->
<!-- It will detect your tech stack, build commands, test runners, and project structure. -->
<!-- Replace the example below with the actual output. -->

- **Stack**: <!-- e.g. TypeScript, Next.js, PostgreSQL -->
- **Build**: <!-- e.g. `npm run build` -->
- **Test**: <!-- e.g. `npm test` or `pytest` -->
- **Lint**: <!-- e.g. `npm run lint` -->
- **Structure**: <!-- e.g. `src/` for app code, `tests/` for tests -->

---

## Coding Guidelines

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

## Verification Workflow

**Always give Claude a way to verify its own work. This is the single highest-leverage practice.**

- Run tests after every change. Prefer running single relevant tests over the full suite.
- For bug fixes, write a failing test that reproduces the issue first, then fix it.
- For UI changes, take a screenshot and compare to the original. List differences and fix them.
- Address root causes, not symptoms — don't suppress errors to make builds pass.
- If you can't verify it, don't ship it.

---

## Development Workflow (Explore → Plan → Code → Commit)

**Separate research and planning from implementation to avoid solving the wrong problem.**

1. **Explore**: Read relevant code first. Use Plan Mode (Shift+Tab) to investigate without making changes.
2. **Plan**: Create a concrete implementation plan. Identify files to change, edge cases, and risks.
3. **Implement**: Write code with tests, verifying against the plan at each step.
4. **Commit**: Descriptive commit message and PR.

Skip planning for trivial tasks where the scope is obvious and the diff fits in one sentence.

---

## Context Management

**Context is the most important resource to manage. Performance degrades as it fills.**

- Use `/clear` between unrelated tasks — don't let old context pollute new work.
- After 2 failed corrections, `/clear` and write a better prompt incorporating what you learned.
- Scope investigations narrowly. Use subagents for research-heavy exploration to keep the main context clean.
- Use `/compact` when context is getting heavy. Add focus instructions: `/compact Focus on the API changes`.
- Don't let a session become a kitchen sink — one task per session when possible.

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
