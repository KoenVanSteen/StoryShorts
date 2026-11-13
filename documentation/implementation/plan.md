# Implementation Plan: StoryShorts — The Unsent Archive

**Date:** 2026-11-13  
**Source:** [PROJECT_IDEA.md](../PROJECT_IDEA.md)

## Summary

Build a small, local command-line pipeline for one channel. The owner supplies original Markdown scripts in a folder per story; the app reads `short.md`, `long.md`, or both, then generates a separate video from each supplied version. It must stop for owner approval before each upload or scheduled release.

Keep the runtime deterministic: no LLM story generation, no agent framework, no database, no web UI, and no new paid service. This makes runtime story-generation token use zero and keeps routine output to concise status/error messages. Later channels and third-party stories are out of scope.

## Technical Context

- **Language:** Python 3.12+; standard library for CLI, JSON, files, and tests. Add only the Google API/OAuth client libraries for YouTube upload.
- **Media:** FFmpeg/ffprobe command-line tools; a local TTS executable and voice selected only after quality and license checks.
- **YouTube:** YouTube Data API with OAuth desktop credentials; verify current quota and costs, then upload privately and schedule only after a per-video approval.
- **Storage:** Markdown story folders, a small asset-license manifest, temporary render files, and outputs on local disk. No database or cloud storage.
- **Story input:** `stories/<slug>/short.md` and `stories/<slug>/long.md` are independently authored and optional individually. `render <story-folder> --format short|long|both` renders the selected file; `both` requires both files and fails clearly if one is missing.
- **Testing:** Python `unittest`; fake TTS/YouTube adapters for offline tests; one explicitly approved private upload for end-to-end verification.
- **Deployment:** Run locally first; add a small Dockerfile after the local pipeline works. Mount stories, output, TTS models, and OAuth files; never bake secrets into the image.
- **Output/token budget:** No LLM runtime calls. Print short progress and actionable errors; do not emit generated reasoning, verbose transcripts, or unnecessary logs.

## Constitution Check

No project constitution, existing application code, architecture artifact, dependency artifact, or topology file was found. This is a greenfield plan. It follows the constraints in the source idea: original owner-written scripts, no unapproved costs, minimal dependencies, and approval before each upload. No missing design artifact is needed to start this small CLI.

## Applied Guidelines

No migration or framework-specific guidelines apply. A workspace implementation agent and skill may guide development task-by-task; they are development-time tooling only and add no runtime dependency or token use to the production pipeline.

## Implementation Steps

### Phase 1: Setup

#### 1.1 Minimal CLI and Markdown story folders
- **Requirements:** REQ-001, REQ-002, REQ-005, REQ-009
- **Description:** Create a Python package with a small `argparse` CLI (`validate`, `render`, `review`, `publish`). Read one story folder containing optional `short.md` and `long.md` files. Support a small Markdown subset: `# Title`, `## Scene heading`, and plain-text paragraphs. The filename selects the format; no JSON story schema, YAML front matter, or LLM client is needed. `render <story-folder> --format short|long|both` processes the selected script(s) independently; `both` requires both files and fails clearly if either is missing.
- **Tasks:**
  - [ ] T001 [Plan:1.1] Create `pyproject.toml`, `src/storyshorts/__init__.py`, `src/storyshorts/__main__.py`, and a concise `src/storyshorts/cli.py`.
  - [ ] T002 [Plan:1.1] Parse and validate `stories/<slug>/short.md` and `stories/<slug>/long.md` in `src/storyshorts/story.py`; add a paired fixture, `assets/licenses.json`, and tests for either version, both versions, and a clear error when a requested version is missing.

#### 1.2 Local narration tool selection
- **Requirements:** REQ-003, REQ-008
- **Description:** Select one local TTS engine and English voice only after a short quality test and review of the engine and voice-model licenses for the intended use. Keep it local and free; if none qualifies, stop and ask the owner rather than substituting a paid API.
- **Tasks:**
  - [ ] T003 [Plan:1.2] Test a local TTS candidate and record the selected engine, voice, license evidence, and install method in `documentation/implementation/research.md`.

### Phase 2: Owner script to finished video [US1]

#### 2.1 Narration and captions for each supplied version
- **Requirements:** REQ-003, REQ-008, REQ-009
- **Description:** Synthesize each Markdown scene's paragraphs locally and use segment durations to create synchronized captions. Produce narration audio and an `.srt` file for each selected version without any LLM calls.
- **Tasks:**
  - [ ] T004 [US1] [Plan:2.1] Implement local narration and caption generation in `src/storyshorts/narration.py`; test timing and failure handling in `tests/test_narration.py`.

#### 2.2 Artifact-led video rendering
- **Requirements:** REQ-002, REQ-004, REQ-005
- **Description:** Render original artifact cards and scene-specific typography with FFmpeg. Render `short.md` as a vertical Short and `long.md` as a landscape video; when both are selected, produce two separate outputs. Include burned-in captions and a sidecar `.srt`. Use only original or explicitly licensed media assets.
- **Tasks:**
  - [ ] T005 [US1] [Plan:2.2] Implement preview and final rendering in `src/storyshorts/render.py`; add a short vertical and long-form smoke-test fixture under `tests/fixtures/`.

### Phase 3: Approved YouTube publishing [US2]

#### 3.1 Per-video review gate
- **Requirements:** REQ-006, REQ-009
- **Description:** Present each rendered file, its source Markdown version, metadata, and target publish time. Require separate explicit owner confirmation for each exact output before upload; never allow scheduling or upload to bypass the gate.
- **Tasks:**
  - [ ] T006 [US2] Add per-output review and explicit confirmation to `src/storyshorts/cli.py`; test that missing or stale approval blocks publishing in `tests/test_publish_gate.py`.

#### 3.2 Upload and schedule
- **Requirements:** REQ-006, REQ-007, REQ-008
- **Description:** Use the YouTube Data API OAuth upload flow. Upload as private, set scheduling only after approval, protect local OAuth files, and report a failed upload as failed rather than success.
- **Tasks:**
  - [ ] T007 [US2] Implement OAuth, private upload, and scheduled publication in `src/storyshorts/publish.py`; test with a fake API before one explicitly approved private test upload.

### Phase 4: Packaging and verification

#### 4.1 Docker
- **Requirements:** REQ-009
- **Description:** Add a minimal container after local rendering and OAuth work. Keep input/output/model directories mounted and secrets outside the image.
- **Tasks:**
  - [ ] T008 [Plan:4.1] Add `Dockerfile`, `.dockerignore`, and required `.gitignore` entries; verify a render works with mounted story and output folders.

#### 4.2 End-to-end acceptance
- **Requirements:** REQ-001 through REQ-009
- **Description:** Run the pipeline on owner-authored pilot material, verify formats and captions, exercise approval and cost gates, and document concise setup and commands.
- **Tasks:**
  - [ ] T009 [Plan:4.2] Complete offline unit/render tests and document setup, the Markdown story-folder convention, local TTS licensing, OAuth, approval, and scheduling in `README.md`; verify no LLM dependency or unapproved spending.

## Project Structure

```text
.github/
  agents/
    storyshorts-implementer.agent.md
  skills/
    storyshorts-implementation/
      SKILL.md
documentation/
  PROJECT_IDEA.md
  implementation/
    plan.md
    research.md
    checkpoints/
      spec-to-plan.yaml
      plan-to-tasks.yaml
README.md
pyproject.toml
Dockerfile
src/storyshorts/
  __main__.py
  cli.py
  story.py
  narration.py
  render.py
  publish.py
stories/<slug>/
  short.md
  long.md
assets/
  licenses.json
output/<slug>/
  short/
  long/
tests/
```

## Testing Strategy

- Validate the Markdown subset, detect available story versions, fail when a requested version is missing, and validate asset-license records without network access.
- Use a fake TTS command and fake YouTube client to test narration, captions, render invocation, retries, and approval blocking.
- Smoke-render one short fixture and one long-form fixture; verify duration, dimensions, audio, and subtitle output.
- Only perform a real API test after the owner explicitly approves it; keep the upload private unless a specific public schedule is approved.
- **Pass condition:** Separate short and long videos can be produced from their respective owner-written Markdown scripts with no LLM calls or new subscription, and publishing is impossible until the owner confirms each exact video.

## Requirement Mapping

Requirement IDs below are assigned from the project idea and the user's clarifications for traceability.

| REQ ID | Description | Plan Items | Implementation Evidence |
|---|---|---|---|
| REQ-001 | Owner-authored Markdown scripts in a folder per story; no LLM generation | 1.1, 4.2 | `stories/<slug>/*.md`, `story.py`, `README.md` |
| REQ-002 | Independently render supplied short and long scripts | 1.1, 2.2 | `story.py`, `render.py`, render fixtures |
| REQ-003 | Local narration and synchronized captions | 1.2, 2.1 | `narration.py`, `research.md` |
| REQ-004 | Original artifact-led, varied visual presentation | 2.2 | `render.py`, render fixtures |
| REQ-005 | Track and use only cleared third-party assets | 1.1, 2.2 | `story.py`, `assets/licenses.json` |
| REQ-006 | Owner approval before each upload or schedule | 3.1, 3.2 | `cli.py`, `publish.py`, `test_publish_gate.py` |
| REQ-007 | YouTube upload and scheduled publication | 3.2 | `publish.py` |
| REQ-008 | No unapproved costs or token-generating services | 1.2, 2.1, 3.2, 4.2 | `research.md`, `narration.py`, `publish.py`, `README.md` |
| REQ-009 | Minimal local CLI, Docker, and concise output | 1.1, 4.1, 4.2 | `cli.py`, `Dockerfile`, `README.md` |
