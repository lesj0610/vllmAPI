# ZenithForge Charter

> [!IMPORTANT]
> `ZenithForge policy`.
> This document defines the product boundary and overrides inherited `tabbyAPI` documentation where they conflict.

## Goal

`ZenithForge` is a separately branded fork derived from `tabbyAPI` `main`.
Its purpose is to become a general-purpose, OpenAI-compatible LLM serving stack with:

- `exllamav3` as the primary generation backend
- `vLLM` as the primary reference for serving semantics
- stricter parser, template, and streaming contracts than the inherited baseline
- stronger regression control than the upstream `tabbyAPI` workflow

This is not a branding-only fork.
It is a product reset with a narrower and more defensible technical direction.

## Brand And Attribution Rules

`ZenithForge` is the public product name.

Upstream names are used only for:

- attribution
- license and notice handling
- compatibility discussion
- architectural reference

Project policy:

- do not present the project as an official `tabbyAPI`, `vLLM`, or `exllamav3` distribution
- do not use upstream names as the primary product identity
- keep fork ancestry and third-party attribution explicit in docs and notices

## Product Direction

The target is not to copy `vLLM` line-for-line.

The target is:

- follow `vLLM` where its serving contracts are better specified
- keep `exllamav3` as the core generation runtime
- treat inherited `tabbyAPI` code as migration material, not automatic source of truth
- replace ad-hoc compatibility logic with explicit protocol, render, parser, streaming, and runtime layers

## Source Of Truth Layers

The project intentionally keeps three reference layers:

1. `vLLM`
   - source of truth for serving semantics
   - source of truth for request/response contract design
   - source of truth for reasoning parser and tool parser architecture
2. `exllamav3`
   - source of truth for generation runtime behavior and backend boundaries
3. `tabbyAPI`
   - source of truth only for legal/code ancestry and reusable utilities that survive review

## Non-Goals

The project should not:

- become a renamed copy of `vLLM`
- inherit unstable, unreviewed `tabbyAPI` behavior by default
- accept broad compatibility patches without contract tests
- preserve model-name hacks where parser/template metadata should solve the problem
- couple the public product identity to upstream branding

## Architecture Direction

The long-term layout should converge toward these responsibilities:

- `backends/`
  - backend capability detection
  - `exllamav3` runtime adapter
  - future non-generation backend families for pooling or speech
- `endpoints/`
  - thin transport routers only
- `services/` or equivalent layered modules
  - request validation
  - rendering/preprocessing
  - parser orchestration
  - stream assembly
  - backend capability routing
- `tests/`
  - golden protocol tests
  - parser and template tests
  - real-model smoke tests
  - client compatibility tests

## Development Rules

1. Contract tests before behavior changes
   - every client-facing semantic change needs a test
2. Public API accuracy over convenience
   - `chat/completions`, `responses`, streaming, and tool calling must be correct enough for real clients
3. Explicit capability handling
   - unsupported features must be gated clearly, not silently ignored
4. Incremental PRs only
   - no monolithic rewrite branches
5. Intentional upstream review
   - `vLLM` behavior is reviewed semantically, then ported deliberately

## Upstream Tracking

Track upstreams separately:

- `upstream-tabbyapi`
  - fork ancestry and reusable baseline
- local `vLLM` mirror
  - protocol and serving reference
- local `exllamav3`
  - backend dependency and integration reference

Porting from `vLLM` should be semantic review first, code movement second.

## Immediate Implementation Order

1. complete the branding and product-identity transition to `ZenithForge`
2. lock down a `vLLM`-referenced rearchitecture plan
3. rebuild startup around CLI-first serving
4. rebuild chat rendering, parser wiring, and streaming contracts
5. expand to broader parity only after the core contract is stable
