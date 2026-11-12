# Contributing

## Scope

Keep changes within the domain boundary described in [architecture](docs/architecture.md) and [ADR-0001](docs/adr/0001-pure-domain-boundary.md). Do not add storage, transport, provider, process, filesystem, execution, or authorization behavior to this crate.

Use canonical terms from [CONTEXT.md](CONTEXT.md). Keep legacy Node projections isolated under `node_*` modules and document exactly what each projection does not model.

## Local checks

Requirements: Rust 1.85 or newer.

```bash
cargo fmt --all -- --check
cargo test --all-targets --locked
cargo clippy --all-targets --locked -- -D warnings
cargo doc --no-deps --locked
```

Add regression tests for validation boundaries, duplicate or missing references, graph cycles, digest tampering, unsupported versions, and unknown outcomes as applicable. Prefer deterministic, checked-in fixtures over live services.

## Pull requests

Explain the domain behavior changed, compatibility impact, and exact checks run. Do not claim authorization, security, or runtime guarantees from unit tests alone.
