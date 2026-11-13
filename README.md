# Claude

A Claude Code plugin marketplace (`cv-tools`) with generic agents and skills that work in
any project by reading that project's `CLAUDE.md`. It contains two plugins:

- `dev-agents`: the functional analyst, technical analyst, developer and quality assurance agents
- `dev-workflow`: the pair and feature skills (`/dev-workflow:feature` uses the agents
  from `dev-agents`, so install both to use it)

## Contents

| Plugin | Type | Name | Purpose |
| --- | --- | --- | --- |
| `dev-agents` | Agent | `functional-analyst` | Turns a request into a functional spec with acceptance criteria (read-only) |
| `dev-agents` | Agent | `technical-analyst` | Turns the spec into a technical design and implementation plan (read-only) |
| `dev-agents` | Agent | `developer` | Implements the plan, keeping the build and tests green |
| `dev-agents` | Agent | `quality-assurance` | Verifies acceptance criteria, reviews the diff and adds tests (edits tests only) |
| `dev-workflow` | Skill | `/dev-workflow:pair [me\|you]` | Pair-programming mode with switchable driver and navigator roles |
| `dev-workflow` | Skill | `/dev-workflow:feature <description>` | Functional analysis → technical analysis → development → QA workflow |

## Install

```text
/plugin marketplace add ChrisVesters/Claude
/plugin install dev-agents@cv-tools
/plugin install dev-workflow@cv-tools
```

Update with `/plugin marketplace update cv-tools`, then restart Claude Code.

To test a local checkout instead:

```text
/plugin marketplace add /path/to/your/clone
/plugin install dev-agents@cv-tools
/plugin install dev-workflow@cv-tools
```

## Auto-suggest in a project

Add to the project's checked-in `.claude/settings.json`:

```json
{
  "extraKnownMarketplaces": {
    "cv-tools": {
      "source": { "source": "github", "repo": "ChrisVesters/Claude" }
    }
  },
  "enabledPlugins": {
    "dev-agents@cv-tools": true,
    "dev-workflow@cv-tools": true
  }
}
```

## Per-project configuration

The agents read the project's `CLAUDE.md` for its stack, build/test commands, testing
conventions and code style. Keep project-specific rules there, not in this repo.

`/dev-workflow:feature` saves each feature's specification and plan to
`docs/features/<name>/spec.md` and `plan.md`. To use another location, name it in the
project's `CLAUDE.md`.

To override an agent in one project, add a file with the same `name` to that project's
`.claude/agents/`. Project-only skills go in the project's `.claude/skills/`.

## Releasing

Each plugin has its own version. Bump `version` in `plugins/<plugin>/.claude-plugin/plugin.json`
when you release changes to that plugin.

See [claude-dev-team-setup.md](claude-dev-team-setup.md) for the full design and
[ROADMAP.md](ROADMAP.md) for planned agents and skills.
