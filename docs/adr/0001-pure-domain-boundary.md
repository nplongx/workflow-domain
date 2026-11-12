# ADR-0001: Keep the library below runtime and authority boundaries

- **Status:** Accepted
- **Date:** 2026-11-12

## Context

The extracted crate models workflow/task values, typed catalogs, immutable plans, policies, graph snapshots, and evidence references. Its original consumers supplied persistence, providers, transport, process management, and external trust.

A standalone library is reusable only if callers can adopt its domain model without inheriting the original application's runtime and authority wiring.

## Decision

Keep `workflow-domain` a pure Rust domain library. Do not add database, network, provider, filesystem, process, scheduler, executor, signer, identity provider, or approval authority dependencies to the crate.

Keep validation and compilation separate from approval and dispatch. Document that digests, policy values, approval records, and evidence references do not independently establish authenticity, truth, or permission.

## Consequences

- Hosts can persist and authorize domain values using their own infrastructure.
- The crate can test deterministic domain behavior without live services.
- Callers must implement and verify the external trust, persistence, execution, and recovery boundaries they require.
- A successful domain validation must never be reported as proof of authorization or successful execution.
