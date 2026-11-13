---
name: storyshorts-implementation
description: Execute one or more explicitly selected StoryShorts implementation-plan tasks with minimal code, focused tests, and concise output. Use when starting or continuing implementation of this repository.
argument-hint: "[plan task IDs, such as T001]"
---

# StoryShorts implementation workflow

Use this workflow for development tasks only. The production pipeline must not depend on agents, skills, or runtime LLM calls.

## 1. Select the scope

- Read `documentation/implementation/plan.md`, `documentation/implementation/research.md`, and the relevant parts of `documentation/PROJECT_IDEA.md`.
- If the user names task IDs, implement only those tasks. Otherwise start with the earliest unchecked, unblocked task; the first task is `T001`.
- Keep each change bounded to the selected task. Do not begin follow-on tasks just because they are nearby.
- Inspect the worktree before editing and preserve all unrelated or uncommitted changes.

## 2. Implement

- Inspect existing files and tests before choosing an approach; follow established project patterns.
- Keep the implementation local, small, and deterministic. Prefer the Python standard library unless a plan requirement justifies a dependency.
- Keep the story-input contract: `stories/<slug>/short.md` and `long.md` are independently authored; either may be provided, and `both` requires both. Do not summarize, expand, or generate scripts.
- Follow the plan's minimal Markdown syntax and make invalid input or operational failures explicit.
- Add focused tests for behavior introduced or fixed. Avoid unrelated refactors and excess abstractions.
- Do not add story-generation LLM calls, paid services, databases, web UI, or runtime agent/skill frameworks.

## 3. Stop for owner decisions

Pause and ask the owner before:

- Selecting or installing a TTS engine or voice whose quality, license, privacy, or cost is unresolved.
- Adding a paid dependency or service, incurring a cost, or using credentials.
- Uploading or scheduling any video. Each exact output needs separate owner approval.
- Making a significant design choice not resolved by the plan or research.

Do not silently substitute a paid service, accept unclear asset rights, expose secrets, or claim a blocked operation succeeded.

## 4. Validate and report

- Run the smallest relevant existing test, build, or lint command. For documentation-only changes, validation is not required unless documentation checks exist.
- Fix failures caused by the change; report unrelated baseline failures separately.
- Mark a plan task complete only after its acceptance criteria are verified. Update directly related documentation when behavior or decisions change.
- Keep the final report short: task IDs completed, important files changed, validation results, and blockers or owner decisions needed.
