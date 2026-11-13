# Roadmap

Add a role or skill only when real use shows it is needed. Every agent handoff loses
detail and costs tokens.

## Next

### `/bugfix` skill and `investigator` agent
A bug workflow: reproduce, find the root cause, fix, verify.
- `investigator` agent (in `dev-agents`): finds the root cause. Read-only, with Bash
  to run code and tests. Reports the cause with evidence, not just the symptom.
- `/dev-workflow:bugfix` skill:
  1. The investigator finds the root cause.
  2. Quality assurance writes a test that fails because of the bug.
  3. The developer fixes the cause until that test passes.
  4. Quality assurance checks for the same problem elsewhere in the code.

### `/retro` skill
Run after a feature or bug fix. It reviews what happened: where an agent
misunderstood, a convention was missed, or the user had to correct Claude. It then
proposes concrete edits to the project's CLAUDE.md or to the agent and skill prompts,
and applies only the ones the user approves.

### `/refactor` skill
Changes structure without changing behaviour, using the existing developer and
quality-assurance agents:
1. Check that tests cover the code being refactored, and add them first if they are
   missing.
2. Refactor in small steps, keeping the tests passing after each one.
3. Refuse behaviour changes. Note them as follow-ups instead.

## Later

- **`/commit` skill:** reviews the staged changes, runs the tests and writes a commit
  message in the project's style.
- **`dependency-upgrader` agent:** upgrades libraries (Spring Boot, npm packages),
  reads changelogs for breaking changes, fixes what breaks and runs the tests.
- **Small-change option for `/feature`:** for example `/dev-workflow:feature --small`,
  which skips functional and technical analysis for small changes.

## Housekeeping

- Update `claude-dev-team-setup.md`: it still describes the single `dev-team` plugin
  with planner, reviewer and test-writer.
- Add a LICENSE if the plugins will ever be submitted to the public plugin directory.

## Not planned

These overlap with Claude Code's built-in commands (`/code-review`,
`/security-review`, `/simplify`) or with existing roles:
- separate security, performance or architecture reviewer agents
- a documentation agent (part of the developer's work)
- a product-owner agent (that's the user)
