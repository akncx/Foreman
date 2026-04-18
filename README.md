# Foreman

[Русская версия](./README-ru.md)

Foreman is a plugin for Factory Droid.

It helps the main chat act as a coordinator for repository work: break a task into parts, launch workers, and guide the next steps.

Canonical repository:
- `https://github.com/akncx/Foreman`

## What this plugin provides

- `/foreman` command
- a reusable `foreman` skill
- a `foreman` droid for coordination
- a `worker` droid for delegated execution

## Operating model

- main chat = orchestrator
- `worker` subagents = executors
- one independent workstream usually maps to one branch and one worktree
- the plugin can split work into separate tasks when useful
- it can keep task context in `.foreman/` inside the target repository

## Example

```text
/foreman Refactor A, B, C
```

Expected behavior:

1. inspect the current repository
2. split the request into workstreams where safe
3. propose a concise plan
4. after confirmation, create branch/worktree strategy
5. launch `worker` subagents through `Task`
6. aggregate results and run validation

## Foreman vs Droid Missions

Foreman is not meant to replace Missions. It is a lighter option for medium-sized repository work.

### Where Foreman is better

- less overkill for medium tasks
- lower token usage and less overhead
- more direct control over workers, branches, and worktrees
- easier to customize
- faster to start for everyday repository tasks

### Where Missions are better

- stronger built-in structure for larger initiatives
- better fit for heavier multi-phase planning and execution

### Practical rule of thumb

- use **Foreman** for medium-sized repository tasks where you want explicit worker orchestration with lower overhead
- use **Missions** for bigger, longer, more structured efforts where extra framework is justified

## Repository layout

- `.factory-plugin/marketplace.json` — single-plugin marketplace manifest
- `.factory-plugin/plugin.json` — plugin manifest
- `skills/foreman/SKILL.md` — main skill
- `droids/foreman.md` — coordinator droid
- `droids/worker.md` — execution droid

## Local development

Install from the local directory:

```bash
droid plugin marketplace add .
droid plugin install foreman@Foreman
```

Then invoke:

```text
/foreman <your request>
```

## Install from GitHub marketplace source

This repository is published as a single-plugin marketplace.

Register the repository as a marketplace source:

```bash
droid plugin marketplace add https://github.com/akncx/Foreman
```

Install the plugin:

```bash
droid plugin install foreman@Foreman
```

Update later with:

```bash
droid plugin update foreman@Foreman
```
