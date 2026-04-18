# Agent-Harness-Bootstrap

[中文说明](./README_CN.md)

> **Stop babysitting your coding agent. Bootstrap the repo instead.**
>
> `agent-harness-bootstrap` turns a normal repository into an **Agent-Readable** workspace with a real entrypoint, repository-native working rules, and persistent project memory.

![Paradigm](https://img.shields.io/badge/Paradigm-Agent--First-blueviolet.svg)
![Architecture](https://img.shields.io/badge/Architecture-Harness_Engineering-success.svg)
![Output](https://img.shields.io/badge/Output-Agent--Readable_Repo-black.svg)

Built around the same idea behind OpenAI's **Harness Engineering**: if you want agents to work well, stop stuffing rules into prompts and start putting them into the repository.

---

## Why It Exists

Most teams do not fail with coding agents because the model is weak.

They fail because the repository has no harness.

That usually looks like this:

- every new session starts with another wall of copied context
- architecture rules live in chat history instead of version control
- the agent does not know what to read first
- plans, blockers, and technical debt are scattered or missing
- code gets written before the repo explains how work is supposed to happen

So the problem is not only generation quality.

The problem is that the repo is not engineered to be the working environment for an agent.

`agent-harness-bootstrap` fixes that first.

---

## What You Get

After bootstrap, the repo stops behaving like a pile of source files and starts behaving like an engineered workspace for agents.

You get:

- a real first entrypoint: `AGENTS.md`
- a design surface: `DESIGN.md`
- an execution and validation surface: `PLANS.md`
- a memory layer under `docs/`
- index files so agents load context in layers instead of swallowing everything at once

The result is simple:

**after bootstrap, the repository becomes the source of working context.**

---

## Before vs After

### Before

The project depends on repeated prompting:

> "Use this architecture, remember this validation rule, read this file first, don't forget this convention, and by the way here's the background again..."

### After

The project explains itself:

> "Read `AGENTS.md`. Follow the index. Work from the repository."

That is the real shift.

You stop treating every session like a fresh onboarding call and start treating the repository like an engineered runtime for agents.

---

## What Gets Created

Bootstrap produces a minimum structure like this:

```text
docs/
  design-docs/
    index.md
  exec-plans/
    active/
    completed/
    tech-debt-tracker.md
  references/
    index.md
DESIGN.md
PLANS.md
AGENTS.md
```

Each file has a clear job:

- `AGENTS.md`
  The first file an agent should read. It points to the rest of the repo.
- `DESIGN.md`
  High-level structure, boundaries, and long-lived project rules.
- `PLANS.md`
  Active work, next steps, validation expectations, and blocker handling.
- `docs/design-docs/index.md`
  The index for design documentation.
- `docs/references/index.md`
  The index for external APIs, platforms, and supporting material.
- `docs/exec-plans/tech-debt-tracker.md`
  The place where unresolved debt is recorded instead of silently forgotten.

If the project has explicit layering, you can also add:

- `docs/design-docs/layer-mapping.md`

---

## Why This Is Different

A normal project template gives you folders.

`agent-harness-bootstrap` gives you an operating shape for agent collaboration.

It answers questions normal scaffolds usually ignore:

- where should an agent start reading
- where should design rules live
- where should plans and blockers live
- how do you avoid re-explaining the same repo every session
- how do you move context from chat into versioned files

This is not about making the repo look tidy.

It is about making the repo usable by an agent that has to keep working tomorrow, not just right now.

---

## Included Templates

The skill ships with templates so initialization does not depend on improvised formatting:

- `assets/AGENTS.template.md`
- `assets/DESIGN.template.md`
- `assets/PLANS.template.md`
- `assets/design-docs.index.template.md`
- `assets/references.index.template.md`
- `assets/core-flows.template.md` — for documenting critical call paths
- `assets/module-validation.template.md` — for module-specific validation commands
- `assets/tech-debt-tracker.template.md`

Optional:

- `assets/layer-mapping.template.md` — for projects with explicit layering
- `assets/glossary.template.md` — for project-specific terminology
- `assets/ci-validation.template.md` — for CI/validation pipeline documentation
- `assets/archive-template.md` — for archiving completed plans

---

## Best Fit

Use it when:

- a new repository is being set up for agent-first development
- an older repository needs its first real `AGENTS.md`
- your team wants the repo, not chat history, to hold the working rules
- you want future agents to inherit project context from files instead of from repeated prompting

Do not use it for:

- ordinary feature work
- a one-off bug fix
- a single test addition
- a small documentation patch
- adding one isolated rule long after initialization

Those tasks should run on top of the harness, not recreate it.

---

## Scope

This project is intentionally narrow.

It does one thing:

**bootstrap the harness once.**

It does not try to:

- replace day-to-day development
- replace project documentation itself
- act as the permanent brain of the repo
- be re-run every time an agent touches the codebase

Once the bootstrap is done, the repository should take over.

---

## How Agents Should Enter the Repo

After initialization, the default read order is:

1. `AGENTS.md`
2. `DESIGN.md`
3. `PLANS.md`
4. `docs/design-docs/index.md`
5. `docs/references/index.md`
6. the specific docs needed for the current task

That is the whole point of this project:

it makes the answer to "where does the agent get its context?" explicit, versioned, and local to the repository.
