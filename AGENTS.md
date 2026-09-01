# KinOS Collaboration Contract

This is the vendor-neutral entry point for every human contributor and AI agent working in this repository. Tool-specific commands may differ, but the rules and OpenSpec artifacts are shared.

## Authority

OpenSpec is the source of truth for product behavior and planned changes:

1. `openspec/specs/` contains accepted, current requirements.
2. `openspec/changes/` contains proposed or active changes.
3. `openspec/config.yaml` contains shared project context and artifact rules.
4. This file defines the collaboration process.
5. Tool-specific instructions adapt that process but do not redefine it.

Code and tests are implementation evidence. They do not silently supersede a specification. If a human request conflicts with an accepted spec, surface the conflict and update the OpenSpec change before implementing it.

## Start Every Task With Context

Before changing files:

1. Read `openspec/config.yaml`.
2. Run `openspec list --specs` and `openspec list`.
3. Read the accepted specs and active change artifacts relevant to the task.
4. Run `openspec status --change <name>` when continuing an active change.
5. If `.codegraph/` exists, use CodeGraph before text search to locate or understand code. Otherwise use `rg`/`rg --files` before broader filesystem searches.
6. Inspect repository status and preserve unrelated work.

Do not infer shipped behavior from the opportunity areas in project context. They are discovery inputs until an approved change specifies them.

## OpenSpec Workflow

Use this lifecycle for additions, behavior changes, removals, architecture decisions, data model changes, integrations, and meaningful bug fixes:

1. **Explore** unclear needs without changing product truth.
2. **Propose** a named change in `openspec/changes/<change-name>/`.
3. **Review** proposal, delta specs, design, and tasks with the human owner. Resolve material unknowns before implementation.
4. **Apply** only the approved scope, keeping tasks and artifacts current.
5. **Verify** implementation against scenarios and record concrete evidence.
6. **Archive** the completed change so accepted deltas become living specs.

Small edits that cannot affect behavior—such as typo-only corrections—may be made directly. When uncertain, create a change.

Useful CLI checks:

```sh
openspec list
openspec list --specs
openspec status --change <change-name>
openspec validate <change-name> --strict
openspec doctor
```

Use the OpenSpec commands/skills installed for your tool. Unsupported tools follow this file and the same CLI-backed artifacts.

## Multi-Agent Coordination

- One human or coordinating agent owns each active change and its final integration.
- Delegate only bounded tasks with explicit inputs, outputs, allowed files, and verification.
- Before parallel work, partition ownership by file or independent concern. Never allow uncoordinated edits to the same file.
- Every handoff reports: scope completed, files changed, decisions made, checks run and results, plus risks or unresolved questions.
- Record durable requirements and decisions in the active OpenSpec change. Do not treat chat history, hidden agent memory, or vendor-specific task state as durable truth.
- Re-read changed artifacts after another contributor's handoff; never assume workspace state is unchanged.
- The coordinating owner resolves conflicting contributions against the approved OpenSpec artifacts and asks the human owner when the spec does not decide the issue.

## Engineering Baseline

- Make the smallest coherent change that satisfies the approved requirements.
- Do not select frameworks, services, databases, or abstractions speculatively.
- Never commit secrets, credentials, private family records, or real financial data. Use synthetic examples.
- Treat authentication, permissions, household membership, reminders, and financial information as security- and privacy-sensitive.
- Do not overwrite, delete, or reformat unrelated work.
- Update relevant OpenSpec artifacts when implementation teaches us something durable.

### Testing and quality gates

- Test at the lowest effective level: unit tests for isolated logic, integration tests for persistence/network/process/provider boundaries, and end-to-end or equivalent system tests for critical family workflows.
- Add targeted security tests whenever a change affects authorization, input validation, secrets, data exposure, deletion, external APIs, or local process execution. Cover both allowed and denied paths where permissions are involved.
- The OpenSpec change that selects a technology stack must define one documented command set for formatting, linting or static analysis, applicable type checks, unit/integration/system tests, build validation, dependency review, and security checks.
- Keep local and CI commands equivalent. Required CI checks must fail visibly when a gate fails or is skipped unexpectedly.
- Never claim a check passed unless it ran. Report commands, results, omitted checks, reasons, and residual risks.

### Maintainability and dependencies

- Apply DRY to knowledge that must change together—business rules, security rules, schemas, and protocols. Similar-looking code with different reasons to change may remain separate.
- Introduce a shared abstraction only when the concept is stable and the result is easier to understand and test than the duplication.
- Before adding or updating a dependency, document its purpose and review maintenance status, license compatibility, version constraint, and known vulnerabilities.
- Keep contributor documentation, public behavior, and OpenSpec artifacts synchronized.

### AI integration constraints

- Approved future options are DeepSeek API, Codex CLI, and Kimi CLI. None is currently implemented, configured, or selected as the default.
- Product workflows depend on provider-neutral capabilities; vendor commands, formats, and optional features stay inside adapters.
- API credentials must use approved secret storage. CLI adapters must invoke validated executables with structured arguments or standard input, never shell interpolation of untrusted content.
- Minimize family data sent to any provider and make the provider boundary clear. Future AI changes must specify authorization, consent, retention, timeouts, cancellation, redaction, malformed-output handling, and safe fallbacks.
- Treat model output as untrusted input. It cannot directly perform irreversible or security-sensitive actions without deterministic validation and required human confirmation.

## Completion and Handoff

A task is complete only when scoped work is implemented, relevant checks pass (or an exception is explicitly documented), active tasks reflect reality, and implementation matches the approved specs. A change is complete only after human review and OpenSpec archival.

End handoffs with a compact report:

- Outcome
- Files changed
- Verification
- Open questions or risks
- Recommended next OpenSpec action
