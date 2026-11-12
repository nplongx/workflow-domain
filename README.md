# Workflow Domain

[![CI](https://github.com/nplongx/workflow-domain/actions/workflows/ci.yml/badge.svg?branch=main)](https://github.com/nplongx/workflow-domain/actions/workflows/ci.yml)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

A pure Rust library for workflow domain types, validation, dependency graphs, immutable plan compilation, policy snapshots, and content-addressed evidence references.

This repository is an independent extraction of the `runalith-domain` crate from [Runalith](https://github.com/nplongx/runalith). Source baseline: `29c24cfa2b6ead5704d26cf2746bc384f2938b80`. The extraction preserves current domain behavior; it does not claim complete compatibility with every Runalith runtime path.

> **Status:** `0.1.0`, initial standalone publication. API and compatibility surface may change before `1.0.0`. This library is not a workflow engine and is not production-certified as a complete authorization or execution system.

## Terminology

See [TERMINOLOGY.md](TERMINOLOGY.md) for shared identifier, lifecycle, evidence, time-unit, and compatibility conventions.

## Scope

- Workflow proposals, task definitions, task/workflow states, and lifecycle constraints.
- Dependency DAG validation and immutable workflow-plan compilation.
- Built-in and versioned custom role/workflow contracts.
- Typed artifact contracts, evidence references, and producer-attempt lineage checks.
- Versioned workflow policies, success contracts, and policy composition models.
- Goal/Idea/Plan/Execution graph snapshots, revisions, typed edges, evidence references, and content hashes.
- Explicitly isolated `node_*` compatibility projections for selected legacy Node workflow semantics.

## Boundaries

This crate has no database, network transport, provider, filesystem, process, scheduler, or executor integration. It performs domain validation and deterministic transformations only.

A valid value is **not** an authorization decision. A digest establishes content identity, not authorship, truth, custody, or approval. An `EvidenceRef` validates the declared artifact digest format and producer task/attempt binding; it does not independently prove that the producer created the artifact. Policy models do not authenticate reviewers or grant permissions. Callers must supply those authority and persistence boundaries.

Compatibility modules prefixed `node_` are intentionally explicit. They model selected legacy behavior; they do not implement a Node runtime or prove complete behavioral parity.

## Quick start

Add the Git dependency:

```toml
[dependencies]
workflow-domain = { git = "https://github.com/nplongx/workflow-domain" }
```

Validate a proposal and its task DAG:

```rust
use std::collections::BTreeMap;
use workflow_domain::{TaskSpec, WorkflowPlan, WorkflowProposal};

fn main() -> Result<(), Box<dyn std::error::Error>> {
    let proposal = WorkflowProposal {
        workflow_id: "job_example".into(),
        title: "Prepare design".into(),
        goal: "Produce a reviewed design".into(),
        tasks: vec![TaskSpec {
            task_id: "design".into(),
            role: "architect".into(),
            description: "Create the design artifact".into(),
            depends_on: vec![],
            required_evidence: vec!["design".into()],
            inputs: BTreeMap::new(),
        }],
        metadata: BTreeMap::new(),
    };

    proposal.validate()?;
    WorkflowPlan {
        schema_version: 1,
        tasks: proposal.tasks,
    }
    .validate()?;
    Ok(())
}
```

The `job_` workflow identifier prefix is preserved from the extracted source contract. It is a compatibility constraint, not a universal workflow standard.

## Development

Requirements: Rust `1.85` or newer.

```bash
cargo fmt --all -- --check
cargo test --all-targets --locked
cargo clippy --all-targets --locked -- -D warnings
cargo doc --no-deps --locked
```

## Documentation

- [Documentation index](docs/README.md)
- [Domain glossary](CONTEXT.md)
- [Architecture and module boundaries](docs/architecture.md)
- [Source lineage and extraction notes](docs/source-lineage.md)
- [Architecture decisions](docs/adr/)
- [Contributing](CONTRIBUTING.md)
- [Security policy](SECURITY.md)
- [Changelog](CHANGELOG.md)

## License

MIT. See [LICENSE](LICENSE).
