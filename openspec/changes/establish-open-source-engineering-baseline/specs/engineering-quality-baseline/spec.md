## Purpose

Defines proportionate, repeatable quality evidence for KinOS contributions so reliability, security, and maintainability grow with the product instead of being added after failures.

## ADDED Requirements

### Requirement: Changes include proportionate automated tests
Each implementation change SHALL include automated tests at the lowest effective level and at every system boundary whose failure would invalidate the change. Pure documentation or metadata changes MAY omit runtime tests but MUST still run applicable validation, formatting, link, or policy checks.

#### Scenario: Isolated decision logic changes
- **WHEN** a change adds or modifies deterministic domain logic
- **THEN** unit tests cover its important success, boundary, and failure cases

#### Scenario: A component boundary changes
- **WHEN** a change affects persistence, networking, provider adapters, processes, files, or another component boundary
- **THEN** integration tests verify the collaborating components using controlled test data and no production credentials

#### Scenario: A critical family workflow exists
- **WHEN** a change affects a critical end-to-end workflow such as authentication, authorization, data deletion, reminders, or financial data handling
- **THEN** an end-to-end or equivalent system test verifies the user-visible path and its important failure behavior

### Requirement: Security is verified continuously
Security-sensitive changes SHALL include tests for their relevant threat boundaries, including authorization, input validation, secret handling, data exposure, and failure behavior. The repository SHALL run automated secret and dependency checks when supported by the selected stack and hosting platform.

#### Scenario: Access to family data changes
- **WHEN** a change affects who can read, create, update, share, export, or delete family data
- **THEN** security tests demonstrate both allowed access and denied access across the affected roles or trust boundaries

#### Scenario: A dependency is introduced
- **WHEN** a change adds or updates a third-party dependency
- **THEN** its necessity, license compatibility, version constraint, and known-vulnerability result are reviewable

### Requirement: Every stack defines one repeatable quality gate
When an implementation stack is selected, its OpenSpec change SHALL define documented commands that run formatting, static analysis or linting, type checks where applicable, automated tests, build validation, and security checks. The same commands MUST be runnable locally and by continuous integration without production secrets.

#### Scenario: A contributor prepares a change for review
- **WHEN** the contributor runs the documented quality command set in a supported development environment
- **THEN** the result provides a clear pass or failure for every applicable quality gate

### Requirement: CI protects accepted quality
The canonical repository SHALL run the applicable documented quality gates for proposed changes and protected-branch updates. Required checks MUST fail when a mandatory gate fails and MUST NOT report success for checks that were skipped unexpectedly.

#### Scenario: A mandatory test fails in a pull request
- **WHEN** continuous integration observes a failure in a required test or security check
- **THEN** the corresponding required status check fails and the change is not represented as verified

### Requirement: Maintainability favors clear knowledge ownership
Contributors SHALL avoid duplicated business rules, security rules, schemas, and other knowledge that must change together. Reuse MUST NOT be introduced solely to eliminate coincidental code similarity; abstractions require a stable shared concept and must remain simpler to understand and test than the duplication they replace.

#### Scenario: Similar code has different reasons to change
- **WHEN** two code paths look similar but represent different domain concepts or evolve independently
- **THEN** a contributor may keep them separate and records rationale when the choice is non-obvious

#### Scenario: A rule is implemented inconsistently
- **WHEN** the same product or security rule is duplicated in locations that must remain synchronized
- **THEN** the change establishes one authoritative implementation or generated representation and tests all affected behavior

### Requirement: Review evidence is honest and traceable
Every completed change SHALL report the checks actually run, their results, any unrun checks, and known risks. Documentation and OpenSpec artifacts MUST be updated when public behavior, contributor workflow, or durable engineering decisions change.

#### Scenario: A check cannot be run
- **WHEN** an applicable check is unavailable or blocked
- **THEN** the handoff names the missing check, explains why it was not run, and does not imply full verification
