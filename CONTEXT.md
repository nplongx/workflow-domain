# Workflow Domain Language

This file defines canonical domain terms used by this repository. It is a glossary, not an implementation specification.

## Workflow

**Workflow proposal**
A caller-authored workflow definition awaiting validation and any external approval required by its host. Validation does not authorize execution.
_Avoid_: approved workflow, executable workflow.

**Workflow plan**
A versioned task graph compiled from a proposal or catalog definition. A compiled plan fixes task definitions and dependency relationships; it does not grant execution authority.
_Avoid_: permission, dispatch token.

**Task**
A bounded unit of work represented in a workflow plan, with declared role, dependencies, inputs, and required evidence.
_Avoid_: runtime process, worker (unless referring to an executor).

**Task outcome**
A domain classification of the observed task result: succeeded, failed, or unknown. Unknown is not success and must not be treated as an automatic retry instruction.
_Avoid_: inferred success.

## Evidence and identity

**Evidence reference**
A typed reference to an artifact digest and the declared producer task/attempt. It describes lineage claims; it does not independently authenticate the producer or prove the artifact's truth.
_Avoid_: verified evidence (unless an external verification contract has actually succeeded).

**Content hash**
A digest used to identify exact serialized content under a defined serialization rule. A hash alone does not prove authorship, correctness, approval, or custody.
_Avoid_: signature, attestation.

**Immutable snapshot**
A versioned value whose content and digest are checked together. Immutability is a data-model property, not a guarantee that storage or an external authority preserves it.

## Policy and authority

**Workflow policy**
A versioned set of constraints and success predicates associated with a workflow or plan. A policy value is descriptive domain data until an external host evaluates and enforces it.
_Avoid_: authorization grant.

**Approval**
A record describing an approval claim over exact proposal and plan digests. The domain model does not authenticate the actor or verify an external signature.
_Avoid_: verified authorization.

**Authorization**
A decision made by a separately configured authority and enforced by the host. This crate does not provide that authority.
_Avoid_: successful validation.

## Graph model

**Goal/Idea graph**
A versioned graph of goal, idea, plan, execution, artifact, and decision nodes connected by typed relationships. A stored node or edge is not thereby a verified claim.

**Graph snapshot**
A sealed graph revision containing node, edge, and evidence records plus a content digest. Its digest checks content consistency, not the truth of claims or trustworthiness of sources.
