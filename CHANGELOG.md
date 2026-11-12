# Changelog

## 0.1.0 — 2026-11-12

Initial standalone GitHub publication of the workflow-domain library, extracted from Runalith's `runalith-domain` crate at source revision `29c24cfa2b6ead5704d26cf2746bc384f2938b80`.

- Standalone Cargo package and dependency boundary.
- Workflow/task domain types and validation.
- Workflow catalog, custom role/workflow compiler, policies, graph snapshots, and content digests.
- Selected legacy Node compatibility projections and their pinned fixtures.
- Documentation, MIT license, and CI workflow.

The standalone `skill_manifest_v2_parity.rs` integration test was not copied: it tests a separate workstream fixture/compiler implemented inside that test file, not the exported domain crate, and its fixture lives outside the extracted crate. All in-crate module tests and their fixtures are retained.
