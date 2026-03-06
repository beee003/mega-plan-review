# Mega Plan Review for Claude Code

A rigorous 10-section plan review framework for [Claude Code](https://docs.anthropic.com/en/docs/claude-code), based on [Garry Tan's Mega Plan Review Mode](https://gist.github.com/garrytan/120bdbbd17e1b3abd5332391d77963e7).

Type `/review` in Claude Code and get a structured, security-first review of any engineering plan before you write a single line of code.

## What it does

Three review modes depending on what you need:

| Mode | When to use | Posture |
|---|---|---|
| **SCOPE EXPANSION** | Greenfield features, ambitious builds | "What would make this 10x better?" |
| **HOLD SCOPE** | Bug fixes, refactors, most PRs | "Make it bulletproof" |
| **SCOPE REDUCTION** | Overbuilt plans, tight deadlines | "What's the minimum that ships value?" |

Ten review sections, each with a mandatory pause for your feedback:

1. **Architecture** — dependency graphs, scaling, rollback posture
2. **Error & Rescue Map** — every failure mode named, every exception class mapped
3. **Security & Threat Model** — attack surface, input validation, auth, injection vectors
4. **Data Flow & Edge Cases** — nil/empty/error shadow paths for every flow
5. **Code Quality** — DRY, naming, cyclomatic complexity, over/under-engineering
6. **Tests** — test pyramid, chaos tests, flakiness risk, coverage gaps
7. **Performance** — N+1 queries, memory, caching, connection pools
8. **Observability** — logging, metrics, alerting, runbooks
9. **Deployment** — migration safety, feature flags, rollback plan, smoke tests
10. **Long-Term Trajectory** — tech debt, reversibility, path dependency

## Install

### Option A: Global (all projects)

```bash
# Create the commands directory if it doesn't exist
mkdir -p ~/.claude/commands

# Copy the review command
curl -o ~/.claude/commands/review.md https://raw.githubusercontent.com/beee003/mega-plan-review/main/review.md
```

### Option B: Per-project

```bash
# From your project root
mkdir -p .claude/commands

# Copy the review command
curl -o .claude/commands/review.md https://raw.githubusercontent.com/beee003/mega-plan-review/main/review.md
```

### Option C: Clone and symlink

```bash
git clone https://github.com/beee003/mega-plan-review.git ~/mega-plan-review

# Global
mkdir -p ~/.claude/commands
ln -s ~/mega-plan-review/review.md ~/.claude/commands/review.md

# Or per-project
mkdir -p .claude/commands
ln -s ~/mega-plan-review/review.md .claude/commands/review.md
```

## Usage

In any Claude Code session:

```
/review
```

That's it. The review framework will:
1. Run a system audit (git log, TODOs, existing pain points)
2. Challenge the premise (Step 0) and ask you to pick a mode
3. Walk through all 10 sections, pausing after each for your feedback
4. Produce required outputs: error registry, failure modes, diagrams, TODOS.md updates

## Prime Directives

1. **Zero silent failures** — every failure mode must be visible
2. **Every error has a name** — no generic `except Exception`
3. **Data flows have shadow paths** — happy path + nil + empty + error
4. **Interactions have edge cases** — double-click, navigate-away, stale state
5. **Observability is scope, not afterthought** — dashboards and alerts ship with the feature
6. **Diagrams are mandatory** — ASCII art for every non-trivial flow
7. **Everything deferred must be written down** — TODOS.md or it doesn't exist
8. **Optimize for 6 months out** — don't create next quarter's nightmare
9. **Permission to say "scrap it"** — if there's a better approach, surface it

## Credits

Based on [Garry Tan's Mega Plan Review Mode](https://gist.github.com/garrytan/120bdbbd17e1b3abd5332391d77963e7). Packaged as a Claude Code slash command for easy installation.

## License

MIT
