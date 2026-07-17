# ponytail-graphify

A Claude Code skill that wires [Ponytail](https://github.com/ponytail-dev/ponytail) + [Graphify](https://github.com/Graphify-Labs/graphify) together.

**Before writing any new code, check if it already exists in your codebase.**

Ponytail's rung 2 says: *"Already in this codebase? Reuse it."* This skill enforces that rule automatically — it queries your Graphify knowledge graph before implementing anything new.

## How it works

You ask Claude to build something. Instead of writing immediately, it:

1. Queries your codebase graph for existing matches
2. If found → points you to it with the file path
3. If partial match → proposes a minimal extension to what exists
4. If nothing → builds the shortest working implementation (ponytail full)

```
You:   "add a loading skeleton component"

Without this skill:  Claude writes a new LoadingSkeleton from scratch.

With this skill:     Already exists: Skeleton at src/v2/components/Skeleton/index.js.
                     Use it like: <Skeleton width="100%" height={20} />
```

## Requirements

- [Claude Code](https://claude.ai/code)
- [Graphify](https://github.com/Graphify-Labs/graphify) installed and graph built
- [Ponytail](https://github.com/ponytail-dev/ponytail) (optional but intended companion)

## Install

```bash
# 1. Install graphify and build your codebase graph
uv tool install graphifyy
graphify install
graphify .

# 2. Add this skill to your project
mkdir -p .claude/skills/ponytail-graphify
curl -o .claude/skills/ponytail-graphify/SKILL.md \
  https://raw.githubusercontent.com/dev284200/ponytail-graphify/main/SKILL.md

# 3. Add the routing rule to your CLAUDE.md
echo "\n- Build, add, create, implement anything new → invoke ponytail-graphify first" >> CLAUDE.md
```

## Usage

Just ask Claude to build something. The skill triggers automatically via the routing rule. Or invoke it directly:

```
/ponytail-graphify add a date formatting utility
```

## Why

Every codebase accumulates helpers, utils, and components that get re-implemented because nobody remembered they existed. This is especially painful in large codebases where grep isn't enough. Graphify maps your code into a queryable graph; this skill makes Claude check it before touching a keyboard.
