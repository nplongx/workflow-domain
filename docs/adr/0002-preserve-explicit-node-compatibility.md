# ADR-0002: Preserve selected Node compatibility projections as isolated modules

- **Status:** Accepted
- **Date:** 2026-11-12

## Context

The extracted domain crate contains useful workflow types and compilers alongside read-only projections for specific legacy Node lifecycle, scheduling, retry, and canonical-serialization behavior. Those projections preserve interoperability with the source system but are not universal workflow semantics.

## Decision

Retain these projections in separately named `node_*` modules for the initial extraction. Do not merge them into generic type names or describe their fixtures as complete runtime parity. Each module's documentation must state the exact projected behavior and relevant exclusions.

## Alternatives considered

- Remove all Node projections during extraction: cleaner initial API, but discards useful compatibility code and differential fixtures.
- Rename them as generic lifecycle/scheduler APIs: rejected because that would overstate their scope and hide source-specific behavior.

## Consequences

- Generic domain types remain separate from legacy compatibility APIs.
- Users can opt into Node-specific projections by importing explicit modules.
- Future extraction can split or remove these modules without changing the core domain concepts, subject to semver review.
