# vllmAPI Charter

> [!IMPORTANT]
> `vllmAPI policy`.
> This document defines fork direction and overrides inherited `tabbyAPI` documentation where they conflict.

## Goal

`vllmAPI` is a clean fork workspace derived from `tabbyAPI` `main`, intended to grow into a general-purpose LLM chat server with:

- `exllamav3` as a first-class backend
- `vLLM` as the primary reference for serving semantics
- strict OpenAI-compatible API behavior
- stronger regression control than the current `tabbyAPI` development flow

This is not a branding-only fork. It is a product boundary reset.

## Product Direction

The target is not to copy `vLLM` line-for-line.

The target is:

- follow `vLLM` where it has a better protocol or serving contract
- keep `exllamav3` as the core inference engine
- reuse only the `tabbyAPI` pieces that remain defensible under testing
- replace ad-hoc compatibility logic with explicit protocol, parser, templating, and streaming layers

## Source of Truth

The project uses three reference layers:

1. `vLLM`
   - source of truth for OpenAI-compatible serving semantics
   - source of truth for request/response protocol design
   - source of truth for chat template and reasoning parser behavior
2. `exllamav3`
   - source of truth for backend inference capabilities and engine integration
3. existing `tabbyAPI`
   - migration source for reusable backend glue, configuration handling, and proven utilities

## Non-Goals

The project should not:

- become a copy of `vLLM`
- inherit unstable dirty state from the current `tabbyAPI` working tree
- accept broad compatibility patches without contract tests
- keep model-name hardcoding where template metadata or parser semantics can solve the issue

## Initial Architecture

The long-term layout should converge toward these responsibilities:

- `backends/`
  - backend capability detection
  - `exllamav3` runtime adapter
  - future backend isolation points
- `endpoints/OAI/types/`
  - request and response protocol models
- `endpoints/OAI/utils/`
  - request normalization
  - chat / responses orchestration
  - streaming event builders
- `endpoints/OAI/reasoning/`
  - parser registry
  - reasoning splitters
  - template semantics helpers
- `common/templating.py`
  - template loading
  - template metadata extraction
  - safe variable handling
- `tests/`
  - protocol tests
  - streaming golden tests
  - parser and template semantics tests
  - real-model integration tests

## Development Rules

1. Clean branch stack only
   - work starts from clean branches
   - no feature work on dirty practical trees
2. Contract tests before compatibility patches
   - every client-facing behavior change needs a test
3. Public semantics over convenience
   - `chat/completions`, `responses`, streaming, and tool calling must be exact enough for real clients
4. Explicit capability handling
   - if a backend cannot support a feature, the server should fail clearly or gate the feature
5. Upstream sync as an ongoing process
   - `vLLM` changes are reviewed continuously, then ported intentionally

## Upstream Tracking Strategy

Track upstreams separately:

- `upstream-tabbyapi`
  - compatibility source for existing fork ancestry
- local mirror of `vLLM`
  - periodic review target for protocol, templating, parser, and streaming changes
- local `exllamav3`
  - backend dependency and integration target

Porting from `vLLM` should be done by semantic review, not blind cherry-pick.

## First Implementation Slices

1. Re-establish a clean, reproducible baseline from `tabbyAPI` `main`
2. Introduce a `vllmAPI` branch stack and testing discipline
3. Build protocol correctness around:
   - `/v1/models`
   - `/v1/chat/completions`
   - `/v1/responses`
4. Rework chat template and reasoning semantics using `vLLM` as the reference
5. Harden streaming and client compatibility using:
   - raw `curl`
   - OpenAI SDK
   - Open WebUI
   - LobeChat

## Immediate Next Step

Start with a clean audit of the current `main` baseline and define the first vertical slice:

- exact OpenAI-compatible chat streaming contract
- template semantics contract
- parser registry contract

That slice must be correct before larger feature expansion.
