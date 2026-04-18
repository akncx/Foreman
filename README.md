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

- `.factory-plugin/marketplace.json` — single-plugin marketplace manifest
- `.factory-plugin/plugin.json` — plugin manifest
- `skills/foreman/SKILL.md` — orchestration logic
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

## Design constraints

- no dependency on repository scripts
- no bundled bootstrap state
- no web fetch for local repository understanding
- orchestration logic lives in the plugin assets themselves

## Marketplace readiness checklist

- plugin manifest with required metadata
- installable root plugin layout
- reusable skill in `skills/`
- custom droids in `droids/`
- no machine-specific scripts or local bootstrap dependencies
