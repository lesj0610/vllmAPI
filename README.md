# vllmAPI

> [!IMPORTANT]
> `vllmAPI` is a clean fork of `tabbyAPI`, not a drop-in rename.
> The repository is being rebuilt as a stricter OpenAI-compatible LLM server with `exllamav3` as a first-class backend and `vLLM` as the primary serving reference.

> [!NOTE]
> This repository is in bootstrap stage.
> Parts of the runtime layout and many operational docs still reflect inherited `tabbyAPI` structure while the fork is being normalized.

## What This Fork Is

`vllmAPI` exists because the inherited `tabbyAPI` baseline is not sufficient for the level of protocol correctness, client compatibility, parser behavior, and template semantics this project needs.

The fork direction is:

- keep `exllamav3` integration strong
- follow `vLLM` where its serving contracts are better defined
- replace fragile compatibility patches with explicit protocol and parser layers
- keep the implementation smaller than `vLLM`, but not looser than `vLLM` in API semantics

This is not an attempt to turn the project into `vLLM`.
It is an attempt to build a more rigorous server on top of the existing `tabbyAPI` ancestry.

## Current Status

Current state:

- repository baseline is forked from `tabbyAPI` `main`
- legal baseline remains `AGPL-3.0-only`
- upstreams are tracked separately
- documentation is being rewritten to clearly distinguish inherited content from fork-specific policy

What is stable right now:

- clean fork repository setup
- upstream remote separation
- fork charter
- license policy and notice tracking

What is not yet complete:

- public package rename throughout the codebase
- revised OpenAI-compatible serving stack
- `vLLM`-grade chat streaming and reasoning semantics
- rebuilt docs for all endpoints and integrations

## Repository Layout

- [docs/00-vllmapi-charter.md](docs/00-vllmapi-charter.md)
  - product direction, scope, architecture, and development rules
- [docs/01-license-policy.md](docs/01-license-policy.md)
  - fork license policy and porting rules
- [THIRD_PARTY_LICENSES.md](THIRD_PARTY_LICENSES.md)
  - current third-party attribution and shipped notices
- `backends/`
  - inherited backend integrations, including `exllamav3`
- `endpoints/`
  - inherited API surface that will be tightened incrementally
- `tests/`
  - inherited test base that will be expanded with stricter protocol tests

## Upstream Relationship

This repository intentionally tracks three different sources of truth:

1. `tabbyAPI`
   - fork ancestry
   - reusable backend glue and existing utilities
2. `vLLM`
   - primary reference for serving contracts
   - primary reference for OpenAI-compatible semantics
3. `exllamav3`
   - inference runtime target
   - backend capability boundary

Project rule:

- `vLLM` is the semantic reference
- `exllamav3` is the runtime reference
- inherited `tabbyAPI` code is reused only when it survives testing and design review

## Documentation Status

Most files under `docs/` are inherited from `tabbyAPI`.
They are being retained temporarily so the fork does not lose operational knowledge during the bootstrap phase.

Interpretation rule for inherited docs:

- if a page explicitly says `Inherited from tabbyAPI`, treat it as carried-forward reference material
- if a page explicitly says `vllmAPI policy`, treat it as fork-specific source of truth

Until the rewrite is complete, fork-specific source of truth is limited to:

- [docs/00-vllmapi-charter.md](docs/00-vllmapi-charter.md)
- [docs/01-license-policy.md](docs/01-license-policy.md)
- [THIRD_PARTY_LICENSES.md](THIRD_PARTY_LICENSES.md)

## License

This repository remains `AGPL-3.0-only` because it is derived from `tabbyAPI`.

Additional rules:

- `vLLM`-derived code must retain Apache-2.0 notice coverage
- `exllamav3`-derived code must retain MIT notice coverage
- hosted deployments must respect AGPL network source-offer obligations

See:

- [LICENSE](LICENSE)
- [docs/01-license-policy.md](docs/01-license-policy.md)
- [THIRD_PARTY_LICENSES.md](THIRD_PARTY_LICENSES.md)

## Roadmap

The first implementation slices are:

1. lock down `/v1/chat/completions` streaming semantics
2. rebuild chat template semantics using `vLLM` as reference
3. rebuild reasoning parser behavior without model-name hacks
4. reintroduce `/v1/responses` only after the chat contract is correct
5. add client compatibility tests for raw `curl`, OpenAI SDK, Open WebUI, and LobeChat

## Acknowledgements

This fork would not exist without the work of the upstream projects it builds on:

- [tabbyAPI](https://github.com/theroyallab/tabbyAPI)
- [vLLM](https://github.com/vllm-project/vllm)
- [exllamav3](https://github.com/turboderp-org/exllamav3)
- [FastAPI](https://github.com/fastapi/fastapi)
