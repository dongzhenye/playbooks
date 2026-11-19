# playbooks

Practical skills for working with coding agents. The first playbook, [use-clis](skills/use-clis/SKILL.md), helps an agent find the right command-line tool when you describe a task without naming the command.

## Try it

Start with the [offline walkthrough](skills/use-clis/references/offline-example.md). It creates two temporary Git projects and a tiny command that prints the headings of a Markdown file. You'll check whether a fresh agent can find the command through a catalog, use it from a project hint, and keep that hint out of an unrelated project. The example uses a POSIX shell, Git, awk and jq. It needs no service account.

## Use the skill in a project

Clone this repository. From the root of the project where you want to use the skill, copy the complete `skills/use-clis` folder into your agent's project skill directory:

| Host | Destination |
| --- | --- |
| Codex | `.agents/skills/use-clis/` |
| Claude Code | `.claude/skills/use-clis/` |

Open a fresh session and ask: *Help me make our existing document-outline command discoverable in this project, then test it without naming it in the prompt.* You can also [read the instructions directly](skills/use-clis/SKILL.md) and adapt them to your own catalog and agent.

## License

[MIT](LICENSE).
