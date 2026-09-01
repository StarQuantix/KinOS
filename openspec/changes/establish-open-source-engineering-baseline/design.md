## Context

The repository currently contains OpenSpec governance artifacts but no application stack or runtime code. It has an empty initial commit shared by local branches `main` and `mermaid`, with no remote. The local GitHub CLI is authenticated as `eidast`; a read-only preflight confirmed active organization-admin membership in `StarQuantix` and that `StarQuantix/KinOS` does not currently resolve. Write authorization and name availability must be checked again immediately before creation. See `proposal.md` for motivation.

## Goals / Non-Goals

**Goals:**

- Make the repository legally reusable and ready for safe public visibility.
- Establish quality rules that are enforceable now and become concrete when a stack is selected.
- Keep future AI work portable across one API provider and two local CLI providers.
- Avoid publishing local agent state or sensitive data.

**Non-Goals:**

- Pretend that runtime tests can exist before runtime code or a stack exists.
- Create a universal AI abstraction before a real AI-backed workflow is specified.
- Add contributor bureaucracy unrelated to present risks.
- Commit to provider feature parity, pricing, availability, or data-processing terms.

## Decisions

### Use the standard MIT License without custom clauses

The root `LICENSE` will contain the OSI-standard MIT text and the notice `Copyright (c) 2026 StarQuantix`. Custom restrictions would make the license non-standard and could undermine the open-source intent.

Alternative considered: add family-data or ethical-use restrictions to the license. Rejected because use restrictions are incompatible with the requested simple MIT licensing model; privacy safeguards belong in product behavior and project policy.

### Define a layered, risk-based test policy

The baseline requires unit tests for isolated logic, integration tests for component boundaries, system tests for critical workflows, and targeted security tests for trust boundaries. Documentation-only changes use relevant validation instead of artificial runtime tests. Concrete frameworks, coverage thresholds, and commands are deferred to the stack-selection change.

Alternative considered: mandate a universal percentage coverage threshold now. Rejected because coverage percentage is easy to game and cannot express risk without code or a selected test stack.

### Interpret DRY as single ownership of knowledge

The project will deduplicate rules that must change together, not every repeated code shape. This avoids both divergent business rules and premature abstractions.

Alternative considered: require zero duplication. Rejected because incidental similarity is often cheaper and clearer than a shared abstraction with multiple reasons to change.

### Establish lightweight CI before runtime code

The initial GitHub workflow will validate OpenSpec artifacts and scan tracked content for secrets. GitHub Actions dependencies will be pinned to immutable commit SHAs, with automated update configuration where practical. Stack-specific checks will be added by the change that selects the stack.

Alternative considered: wait for application code before adding any CI. Rejected because specifications and public repository content already have meaningful validation and disclosure risks.

### Isolate providers at capability boundaries

Future AI features will define the smallest provider-neutral capability their workflow needs, then implement approved provider adapters. Adapters normalize results and errors while permitting explicit optional capability detection. CLI processes receive structured arguments or standard input without shell interpolation; API tokens come from secret storage.

Alternative considered: expose DeepSeek, Codex, or Kimi primitives throughout product code. Rejected because it would couple family workflows, tests, and stored data to a vendor.

### Publish only after creating a reviewed initial commit

Apply will add publication-safe ignore rules, validate OpenSpec, scan tracked content, review the exact commit contents, create a local baseline commit, then create `StarQuantix/KinOS` as public and push `HEAD` to the remote `main` branch. This preserves the workspace's local branch name while establishing the conventional public default branch. Repository creation must be idempotent: if the target already exists, apply stops and reports ownership/state instead of overwriting or repointing it silently.

Alternative considered: create the empty GitHub repository first. Rejected because a public placeholder can be claimed as complete and publication checks are stronger when performed against the exact initial commit.

## Risks / Trade-offs

- [The `StarQuantix/KinOS` name exists or the authenticated user lacks organization write access] → Stop before external mutation and report the exact GitHub state; do not create a substitute repository name.
- [A public push exposes local agent state or sensitive content] → Ignore ephemeral state, scan tracked files and history, and inspect the exact initial commit before repository creation.
- [Security scanning produces false positives] → Review findings explicitly; suppress only with a documented, narrowly scoped reason.
- [Policy becomes aspirational] → Require the future stack-selection change to define executable local and CI commands before application implementation is accepted.
- [Provider portability collapses to a lowest common denominator] → Keep contracts capability-specific and allow explicit optional features rather than pretending all providers are identical.
- [Provider data terms change] → Treat provider enablement and data handling as deployment configuration subject to later privacy review, not a permanent promise in this baseline.

## Migration Plan

1. Confirm or revise the copyright holder and review all change artifacts.
2. Add the MIT license, documentation, engineering context, ignore rules, and governance CI.
3. Validate OpenSpec and scan the exact files intended for the initial commit.
4. Create and inspect the local baseline commit on the current workspace branch.
5. Verify `StarQuantix/KinOS` availability and organization permissions.
6. Create the public GitHub repository, set `origin`, push `HEAD:main`, and verify public visibility, the default branch, and rendered README/license metadata.
7. If publication fails, retain the verified local commit, remove only a newly added invalid remote when safe, and report the external state without choosing a different destination.

## Open Questions

- Whether the organization later wants copyright assignment, a contributor license agreement, or Developer Certificate of Origin can be decided when outside contributions begin.
- Concrete test frameworks, coverage reporting, supported development environments, and branch protection rules will be selected with the application stack and team workflow.
- Which approved AI provider first supports a real KinOS workflow remains intentionally undecided.
