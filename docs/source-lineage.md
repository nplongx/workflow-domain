# Source Lineage

## Upstream source

- Repository: [nplongx/runalith](https://github.com/nplongx/runalith)
- Original crate: `rust/crates/runalith-domain`
- Source revision: [`29c24cfa2b6ead5704d26cf2746bc384f2938b80`](https://github.com/nplongx/runalith/tree/29c24cfa2b6ead5704d26cf2746bc384f2938b80/rust/crates/runalith-domain)
- Upstream license: MIT

The source crate directory was clean at the extraction revision. The extraction was made into a new directory; no upstream source files were edited.

## Extracted content

- `src/`: domain types, validators, compilers, policy models, graph models, and explicit legacy Node compatibility projections.
- `fixtures/`: compiler and catalog golden fixtures.
- `tests/fixtures/`: deterministic Node-generated compatibility fixtures used by in-crate unit tests.

The workspace-inherited Cargo manifest was replaced with a standalone manifest. Direct dependency versions and relevant features were retained. The crate package name is now `workflow-domain` and its Rust import name is `workflow_domain`.

## Excluded upstream material

`tests/skill_manifest_v2_parity.rs` was not extracted. It implements its own manifest compiler inside the integration test, reads a workstream fixture outside the crate, and does not exercise the exported domain API. It belongs to that separate workstream's fixture research, not this reusable library.

Runalith's application README, release records, runtime instructions, host adapters, and workspace configuration were not copied. This repository has its own scope, docs, CI, and release identity.

## Independence statement

The published repository has no Git submodule, workspace path dependency, or runtime dependency on Runalith. Source lineage is retained here for attribution and auditability. Future changes are governed by this repository's own issues, review, tests, and version history.
