---
name: feature
description: Runs the full feature workflow - functional analysis, technical analysis, development and quality assurance - using the agents from the dev-agents plugin.
disable-model-invocation: true
argument-hint: <feature description or issue number>
---
Implement this feature: $ARGUMENTS

This workflow uses the functional-analyst, technical-analyst, developer and
quality-assurance agents from the dev-agents plugin. If they are not available,
tell the user to install `dev-agents@cv-tools` and stop.

The agents hand work to each other through files, not summaries. Pick a short
kebab-case name for the feature and use `docs/features/<name>/spec.md` and
`docs/features/<name>/plan.md`, unless CLAUDE.md names another location. Always pass
these paths to the agents.

1. Functional analysis: ask the functional-analyst agent to write the specification to
   the spec path. Show the user its summary and open questions. Record the user's
   answers and any changes in the spec file, and wait for the user to approve it.
2. Technical analysis: ask the technical-analyst agent to write the plan to the plan
   path, based on the spec file. Show the user its summary and open questions. Record
   the answers in the plan file, and wait for the user to approve it.
3. Development: ask the developer agent to implement the plan, giving it both file
   paths. If it reports that the plan does not work, discuss it with the user and
   update the plan file before continuing.
4. Quality assurance: ask the quality-assurance agent to verify the change, giving it
   both file paths.
5. Fix: if quality assurance reports confirmed issues or failing criteria, send those
   findings to the developer agent to fix, then run quality assurance again. Stop
   after two rounds and ask the user how to proceed. Tell the user which findings you
   did not act on and why.
6. Summarise: list what changed, the acceptance-criteria status, the test result, and
   a suggested commit message. Do not commit unless the user asks.
