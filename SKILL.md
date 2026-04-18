# Foreman Skill for Factory Droid

Foreman currently ships as a Factory Droid-oriented skill/bootstrap kit.

Canonical source:
- `https://github.com/akncx/Foreman`

Use this repository as the source of truth for the Foreman Factory Droid skill/toolkit and for future updates.

## Purpose

Use this skill when you want to deploy a Foreman-style orchestration layer into a project so one controller agent can:
- manage task branches and worktrees
- delegate execution to workers
- run validation/builds in the correct worktree
- coordinate commit/push/PR flow
- resume existing tasks after bug reports

## Current support

At the moment, Foreman is supported only for **Factory Droid**.

It is not yet packaged for other agents or editors.

## Expected deployment result

When applied to a project, Foreman should provision:
- orchestrator and worker droid definitions
- task registry helpers
- task state templates
- worktree/build/push/pr scripts
- orchestration policies and flow files

## Recommended usage

Use Foreman in chat as the main controller.
Let Foreman allocate worktrees, delegate to workers, and drive the implementation loop.
