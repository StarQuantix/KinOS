## Purpose

Provides one vendor-neutral workflow so human contributors and AI agents can change KinOS safely while OpenSpec remains the durable source of product truth.

## ADDED Requirements

### Requirement: OpenSpec is authoritative
The repository SHALL treat accepted specifications under `openspec/specs/` as the authority for current product requirements and active changes under `openspec/changes/` as the authority for proposed work. Chat transcripts, task trackers, tool-specific instructions, and implementation code MUST NOT silently override an accepted specification.

#### Scenario: A request conflicts with an accepted specification
- **WHEN** a contributor receives a request that conflicts with an accepted specification
- **THEN** the contributor proposes an OpenSpec change and does not implement the conflicting behavior until the change is approved

### Requirement: Product behavior follows the change lifecycle
Any work that adds, modifies, or removes product behavior SHALL begin as an OpenSpec change containing the artifacts required by the configured schema. Implementation SHALL start only after the relevant proposal, requirements, design decisions, and tasks are sufficiently complete and accepted by the human owner.

#### Scenario: A new feature is requested
- **WHEN** a contributor is asked to add new user-visible behavior
- **THEN** the contributor creates or updates an OpenSpec change before modifying runtime code

#### Scenario: A non-behavioral edit is requested
- **WHEN** a contributor performs a clearly non-behavioral edit such as correcting a typo
- **THEN** the contributor may make the edit directly if it does not contradict an active change or accepted specification

### Requirement: Changes have one accountable owner
Each active change SHALL have one accountable owner or coordinating agent. Additional agents MAY perform bounded tasks, but they MUST use the same OpenSpec artifacts, report files changed and verification evidence, and avoid editing the same files concurrently unless explicitly coordinated.

#### Scenario: Work is delegated across agents
- **WHEN** the owner delegates parts of an active change
- **THEN** every delegated task has a clear scope and returns its edits, decisions, unresolved issues, and verification results to the owner

#### Scenario: Concurrent edits would overlap
- **WHEN** two contributors are likely to modify the same file or requirement
- **THEN** the accountable owner serializes or repartitions the work before edits begin

### Requirement: Decisions remain vendor-neutral
Durable product requirements and architectural decisions SHALL be recorded in OpenSpec artifacts using tool-neutral language. Vendor-specific instruction files MAY adapt invocation syntax, but MUST defer to the root collaboration contract and OpenSpec when meaning differs.

#### Scenario: Tools use different commands
- **WHEN** two AI tools expose different command names for the OpenSpec workflow
- **THEN** both tools operate on the same repository-local OpenSpec artifacts and preserve equivalent lifecycle semantics

### Requirement: Completion includes verification and archival
A change SHALL NOT be represented as complete until its scoped tasks are finished, applicable checks have passed or documented exceptions are accepted, implementation is compared against the approved requirements, and the completed change is archived into the living specifications.

#### Scenario: Implementation is ready for handoff
- **WHEN** all implementation tasks appear complete
- **THEN** the owner reports verification evidence and any exceptions before archiving the change
