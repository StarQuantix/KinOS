## Why

KinOS will be developed by people and AI agents from different vendors, so the repository needs one durable, vendor-neutral agreement about product intent and how changes are specified. Establishing that agreement before application code exists prevents prompts, tool-specific files, and implementations from becoming competing sources of truth.

## What Changes

- Define KinOS as a private family coordination product whose initial opportunity areas include shared tasks, recipes, personal finances, household chores, and reminders.
- Make OpenSpec the authoritative system for product requirements and change history.
- Add a vendor-neutral collaboration contract for all contributors and AI agents.
- Document a small, repeatable propose → review → apply → verify → archive workflow.
- Keep technology and architecture decisions intentionally open until they are justified by an approved change.

## Capabilities

### New Capabilities

- `spec-driven-collaboration`: Defines how contributors and heterogeneous AI agents coordinate through OpenSpec without creating conflicting sources of truth.

### Modified Capabilities

None.

## Impact

- Adds repository governance and onboarding files.
- Enriches `openspec/config.yaml` with shared KinOS product context and artifact rules.
- Introduces no runtime code, APIs, dependencies, or architecture decisions.
