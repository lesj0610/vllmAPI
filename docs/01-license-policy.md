# vllmAPI License Policy

> [!IMPORTANT]
> `vllmAPI policy`.
> This document defines the fork's working license rules and notice handling.

This document is a project policy for keeping the fork legally clean.
It is not legal advice.

## Project License

`vllmAPI` is currently a fork of `tabbyAPI`, so the repository remains licensed under:

- `AGPL-3.0-only`

That means modifications distributed to users, and modified network service deployments made available to users, must continue to satisfy the AGPL obligations of the upstream codebase.

## Upstream License Boundaries

The project intentionally combines ideas and code from projects under different licenses:

- `tabbyAPI`: `AGPL-3.0-only`
- `vLLM`: `Apache-2.0`
- `exllamav3`: `MIT`

Current policy:

1. The fork license stays `AGPL-3.0-only`
2. Code adapted from `vLLM` must keep attribution and Apache notice coverage
3. Code copied from `exllamav3` must keep attribution and MIT notice coverage
4. Runtime integration with `exllamav3` alone does not change the repository license

## Practical Rules

### When porting from vLLM

- keep the source reference in commit messages or PR notes
- preserve any required copyright and license notices
- update `THIRD_PARTY_LICENSES.md`
- ensure `LICENSES/Apache-2.0.txt` remains shipped

Apache-2.0 is compatible with GPLv3-family licensing in the direction needed for this fork, so Apache-licensed source can be incorporated into an AGPLv3-covered program when the combined work is distributed under AGPLv3 terms and Apache notices are preserved.

### When copying from exllamav3

- record the copied or adapted file paths in `THIRD_PARTY_LICENSES.md`
- preserve the MIT copyright notice
- ensure `LICENSES/MIT-exllamav3.txt` remains shipped

If `vllmAPI` only talks to `exllamav3` through backend integration boundaries and does not copy code, keep the dependency mention but do not claim copied-file coverage.

### When modifying existing AGPL code

- keep the repository source available
- keep the `LICENSE` file intact
- keep modification history in Git
- do not remove upstream attribution

### When deploying a hosted service

If a modified AGPL-covered server is made available for network interaction, users of that server must be able to receive the corresponding source for the running modified version.

Project policy for hosted deployments:

- keep the public repository updated with the running server source, or
- provide a clearly visible source link for the exact deployed revision

## Required Files

These files must remain present:

- `LICENSE`
- `THIRD_PARTY_LICENSES.md`
- `LICENSES/Apache-2.0.txt`
- `LICENSES/MIT-exllamav3.txt`

## Review Checklist

Before merging any port from `vLLM` or `exllamav3`, verify:

- what code was copied versus only referenced
- which upstream license applies
- whether `THIRD_PARTY_LICENSES.md` needs an update
- whether a new license text file needs to be shipped
- whether deployment/source-offer obligations changed

## References

- GNU AGPLv3 overview: https://www.gnu.org/licenses/quick-guide-gplv3.en.html
- GNU license FAQ: https://www.gnu.org/licenses/gpl-faq.en.html
- Apache GPL compatibility note: https://www.apache.org/licenses/GPL-compatibility
