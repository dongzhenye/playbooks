---
name: use-clis
description: Help people and agents find and use an existing command-line tool from the projects that need it. Use when adopting a CLI, deciding where to surface it, diagnosing a missed or wrong tool choice, or testing discovery in a fresh session.
---

# Use CLIs

Start with the task in the user's own words. For example, “Show me the outline of this guide.” Find out where the task should work and what an observable result would be. If the user only needs to run a tool, use the existing setup. If they want the next session to find it too, work through the missing pieces below.

## Register once

Look for an existing catalog and for commands the project already supplies. Record the command, what someone would ask it to do, and its maintained source. Include an execution location only when it matters: on PATH, relative to a particular project root, or in another authorized environment. Keep install instructions with their owner and detailed flags in the tool's help.

The full catalog should be searchable from any project. Put one stable pointer to its location or search command in the user's shared agent instructions. A registry entry can be found even when its executable is unavailable on the current machine.

## Decide where it should surface

Choose the smallest useful scope for a **passive hint**: all projects, named projects, or lookup only. Keep active search across the full catalog. Describe the trigger and the executable in one line. For example: “Show a guide's outline → run ./bin/doc-outline from the project root.”

Deliver the hint through an instruction or skill entry that the host actually reads. Respect the project's choice of a shared or local-only entry. Preserve existing instructions; check Git tracking and exclusions before writing a local hint. If the project already supplies the right command, reference it in place. When names collide, check the resolved executable and its source before choosing.

## Run the installed version

Resolve the executable on the intended host and in the intended working directory. Read its own help for the relevant operation. Run the authorized task and check the result. A successful lookup proves discoverability; a working executable and, where relevant, an authenticated account are separate checks. For a discovery test, choose a read-only operation with an observable result.

## Test with fresh sessions

- **Active lookup.** Start a fresh session with just the catalog pointer. Ask which registered tool can do the task, without naming it. Check that the agent actually consults the catalog.
- **Passive discovery.** Start another fresh session in scope. Give only the natural-language task. Check which executable the agent selects, where it runs, and whether the output answers the question.
- **Scope boundary.** In an unrelated project, check that a project-only hint is absent while explicit catalog search still finds the entry.

Report the host, scope, observed tool choice and result. Distinguish a hint present in startup context from a model actually selecting the command. If the model guesses a familiar tool or completes the task another way, record that outcome separately.

[Try the offline example](references/offline-example.md) for a tiny project command, catalog entry and test prompts.
