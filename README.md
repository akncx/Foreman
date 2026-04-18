# Foreman

One agent in charge. Many tasks in motion.

Foreman is a reusable orchestration toolkit for agent-driven software work. It helps one main controller agent create and manage task branches, worktrees, workers, validation, commits, pushes, pull requests, and bugfix loops.

Canonical repository:
- `https://github.com/akncx/Foreman`

## Current support

Foreman currently works only for **Factory Droid**.

This repository currently provides:
- a Factory Droid-oriented skill/bootstrap layer
- Droid definitions for `foreman` and `worker`
- supporting scripts, templates, schemas, and policies

Support for other agents is not added yet.

## What it does

- accepts a high-level task from the user
- decides whether to create a new task or resume an existing one
- assigns one branch and one worktree per task
- delegates implementation to worker agents
- runs validation/builds in the correct worktree
- keeps task state in a local registry
- supports resume/fix cycles after testing feedback

## Core idea

Foreman is not the worker. Foreman is the coordinator.

- **Foreman** decides
- **Workers** implement
- **Scripts** execute deterministic project operations

## Layout

- `.factory/droids/` — orchestrator and worker definitions
- `scripts/` — helper automation scripts
- `templates/` — task and bug report templates
- `schemas/` — task registry schema
- `state/` — local and example task state
- `policies/` — orchestration rules

## How to use

Use Foreman as the main controller agent in chat.

Recommended flow:
1. open a Droid session in the target repository or orchestration repo
2. invoke the `foreman` orchestrator droid
3. describe the task in plain language
4. let Foreman allocate branch/worktree, delegate to workers, validate, and prepare push/PR flow

## Install for Factory Droid

At the moment, Foreman is intended to be used with Factory Droid.

Recommended installation flow:

1. clone the repository:
   ```bash
   git clone https://github.com/akncx/Foreman
   ```
2. open the repository in a Droid session
3. use the included Factory Droid files from:
   - `.factory/droids/foreman.md`
   - `.factory/droids/worker.md`
   - `SKILL.md`
4. use Foreman in chat as the main controller agent for orchestration tasks

For now, Foreman should be treated as a **Factory Droid-only skill/toolkit**.

## Current MVP

The current MVP includes:
- a Factory Droid skill entry in `SKILL.md`
- a generic orchestrator droid definition
- a generic worker droid definition
- task registry helpers
- task bootstrap and status update scripts
- worktree/build/push/pr helper scripts
- orchestration flow and policy files
