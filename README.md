# Foreman

Foreman is a plugin-first orchestration package for Factory Droid.

It turns the main chat into a repository orchestrator that can inspect a repo, split work into independent streams, propose a plan, and launch real worker subagents for execution.

Canonical repository:
- `https://github.com/akncx/Foreman`

## What this plugin provides

- `/foreman` slash entrypoint
- a reusable `foreman` orchestration skill
- a `foreman` droid for coordination
- a `worker` droid for delegated execution

## Operating model

- main chat = orchestrator
- `worker` subagents = executors
- one independent workstream usually maps to one branch and one worktree
- repository inspection happens locally through Droid tools, not web fetch
- runtime state, if needed, lives in the target repo under `.foreman/`

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

## Repository layout

- `.factory-plugin/plugin.json` — plugin manifest
- `skills/foreman/SKILL.md` — orchestration logic
- `droids/foreman.md` — coordinator droid
- `droids/worker.md` — execution droid

## Local development

Install from the local directory:

```bash
droid plugin marketplace add .
droid plugin install foreman@foreman
```

Then invoke:

```text
/foreman <your request>
```

## Design constraints

- no dependency on repository scripts
- no bundled bootstrap state
- no web fetch for local repository understanding
- orchestration logic lives in the plugin assets themselves
