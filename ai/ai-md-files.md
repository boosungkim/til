# AI md files
There are different kinds of md files. Let's make sense of the differences

## AGENTS.md/CLAUDE.md - Everything
File loaded into the context window at the start of every session. Good for project-wide conventions that apply to every interaction. It's passive. It doesn't do anything, it just informs.

I sometimes confused this with the other agent files, but the difference is this: since this file will be read and used by the main session, it sort of acts like an agent file for the main sesion. So preferably, this should be used for absolute primary details.

## Agents - Who
Agents are persistent personas with a dedicated system prompt and fresh context window. They define who is responding - their role, tone, constraints, and goals. They're best for sustained, role-specific workflows where consistent behavior across a whole session matters.

- They also define any sub-agent workflows.

## Slash commands - What
Slash commands are reusable prompt shortcuts or prompt templates. These are stateless and ephemeral and are best for repetitive, well-defined actions.

## Skills - How
Skills are procedural knowledge documents — they don't define who the AI is (that's agents) or what action to trigger (that's commands). Instead, they define how to do something well, encoding hard-won best practices that the AI reads before executing a task.

- A skills file shouldn't be written like documentation. It should be written regarding a task, not a tool.
- Skills should be split by use cases, not topics.
- Claude Code builds an <available_skills> list from the YAML frontmatter of all your skill files and injects it into its tool definition. Hence, skills will be invoked automatically.
- Skills subdirectories are supported.
- We can bundle scripts and supporting files alongside the instructions. This is what makes skills more powerful than slash commands: they can package up instructions and the code that executes them together.
- Good for procedural workflows.

## Rules
Another way to split a bloated CLAUDE.md/AGENTS.md file into pieces. The key difference is that rules have path targeting. You can set up a rule file to only be invoked for specific directories or specific files:

```
---
paths: src/api/**/*.ts
---
```

Coding standards or preferences regarding specific languages would fit quite well here.

## Hooks
Hooks are user-defined shell commands that execute at specific points in Claude Code's lifecycle. When an event fires, Claude Code passes event-specific data as JSON to your script's stdin. Your script reads that data, does its work, and tells Claude Code what to do next via exit code — exit 0 lets the action proceed, exit 2 blocks it.

- Hooks are the only layer that's truly outside Claude's judgment.
- Useful for linting, tests, etc. that need to be run no matter what.