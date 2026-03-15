# ZenithForge

> [!IMPORTANT]
> `ZenithForge` is a separately branded fork derived from `tabbyAPI`.
> It is being rebuilt as an `exllamav3`-first, OpenAI-compatible serving stack with `vLLM` used as the primary architectural and protocol reference.

> [!NOTE]
> This repository is still in bootstrap stage.
> A large portion of the operational docs are inherited from `tabbyAPI` and are retained only as temporary reference.

> [!WARNING]
> `ZenithForge` is not affiliated with `vLLM`, `TabbyML`, or the upstream `tabbyAPI` project.
> Upstream names are used only for attribution, compatibility discussion, and architectural reference.

## What ZenithForge Is

`ZenithForge` exists because the inherited `tabbyAPI` baseline is not sufficient for the level of protocol correctness, parser behavior, chat templating, streaming stability, and client compatibility this project is targeting.

The product direction is:

- keep `exllamav3` as the primary text-generation runtime
- use `vLLM` as the semantic reference for serving behavior
- retain only the `tabbyAPI` pieces that survive design review and regression tests
- replace ad-hoc compatibility logic with explicit render, parser, streaming, and runtime layers

This is not a `vLLM` clone and not a branding-only fork.
It is a new product boundary built on top of inherited `tabbyAPI` ancestry.

## Current Status

Stable today:

- clean fork repository setup
- upstream remote separation
- AGPL baseline and third-party notice tracking
- fork charter and rearchitecture planning
- initial `ZenithForge` branding transition

Not complete yet:

- end-to-end serving rearchitecture
- CLI-first bootstrap replacing YAML-first startup
- `vLLM`-grade streaming and parser contracts
- full documentation rewrite
- package/layout normalization

## Upstream Relationship

This repository intentionally keeps three separate reference layers:

1. `tabbyAPI`
   - legal and code ancestry
   - migration source for reusable backend glue and utilities
2. `vLLM`
   - reference for serving contracts, parser behavior, render boundaries, and streaming semantics
3. `exllamav3`
   - primary inference runtime target
   - backend capability boundary

Project rule:

- `vLLM` is the serving reference
- `exllamav3` is the runtime reference
- inherited `tabbyAPI` code is reused only when it survives testing and architecture review

## Documentation Status

Most files under `docs/` are still inherited from `tabbyAPI`.
They should be read as temporary reference, not final product policy, unless the page explicitly says `ZenithForge policy`.

Current source-of-truth documents are:

- [docs/00-zenithforge-charter.md](docs/00-zenithforge-charter.md)
- [docs/01-license-policy.md](docs/01-license-policy.md)
- [docs/11.-ZenithForge-vLLM-Reference-Rearchitecture-Plan.md](docs/11.-ZenithForge-vLLM-Reference-Rearchitecture-Plan.md)
- [THIRD_PARTY_LICENSES.md](THIRD_PARTY_LICENSES.md)

## License

`ZenithForge` remains `AGPL-3.0-only` because it is derived from `tabbyAPI`.

Additional rules:

- code adapted from `vLLM` must retain Apache-2.0 attribution and notice coverage
- copied `exllamav3` code must retain MIT attribution and notice coverage
- hosted deployments must satisfy AGPL network source-offer obligations

See:

- [LICENSE](LICENSE)
- [docs/01-license-policy.md](docs/01-license-policy.md)
- [THIRD_PARTY_LICENSES.md](THIRD_PARTY_LICENSES.md)

## Immediate Direction

The first implementation slices remain:

1. lock down `/v1/chat/completions` rendering and streaming contracts
2. rebuild chat templating, reasoning parsing, and tool parsing using `vLLM` as reference
3. move server startup from YAML-first to CLI-first
4. reintroduce broader parity such as `/v1/responses`, pooling, audio, and realtime only after the core contract is stable
5. add client compatibility tests for raw `curl`, OpenAI SDK, Open WebUI, and LobeChat-class clients

## Acknowledgements

This project builds on the work of upstream projects it references or derives from:

- [tabbyAPI](https://github.com/theroyallab/tabbyAPI)
- [vLLM](https://github.com/vllm-project/vllm)
- [exllamav3](https://github.com/turboderp-org/exllamav3)
- [FastAPI](https://github.com/fastapi/fastapi)
