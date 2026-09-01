## 1. License and Repository Hygiene

- [x] 1.1 Add the unmodified MIT text to root `LICENSE` with `Copyright (c) 2026 StarQuantix`; verify the notice and standard license text exactly match the approved artifact.
- [x] 1.2 Add publication-safe root ignore rules for environment files, credentials, operating-system files, editor output, build artifacts, and local agent/runtime state without excluding shared OpenSpec or agent instructions; verify `git status --short --ignored` classifies intended and ignored files correctly.

## 2. Durable Engineering Context

- [x] 2.1 Extend `openspec/config.yaml` with the approved testing, security, maintainability, CI, dependency, documentation, and AI-integration principles; verify `openspec instructions proposal --change establish-open-source-engineering-baseline --json` includes the new context without YAML errors.
- [x] 2.2 Update `AGENTS.md` with the layered testing policy, security review triggers, honest verification rules, DRY interpretation, dependency hygiene, and approved AI-provider constraints; verify it defers product behavior to OpenSpec and does not claim an AI provider is implemented.
- [x] 2.3 Expand `README.md` with mission and maturity, opportunity-area boundaries, OpenSpec workflow, engineering and test baseline, security expectations, AI options, contribution steps, canonical repository, and MIT license; verify every documented path and command exists or is explicitly labeled as future work.

## 3. Governance Automation

- [x] 3.1 Add a minimal GitHub Actions governance workflow that validates all OpenSpec artifacts strictly and scans committed content for secrets using immutable action references; verify the workflow syntax and action references against primary documentation and a local parser where available.
- [x] 3.2 Add GitHub Actions dependency-update configuration for the governance workflow; verify the configuration targets the correct ecosystem and repository path.

## 4. Local Verification and Publication Review

- [x] 4.1 Run strict OpenSpec validation and repository health checks for all active changes; verify both changes are valid and no artifact dependency is missing.
- [x] 4.2 Scan the exact candidate repository content with a reputable secret scanner using no production credentials; verify there are no unresolved findings and review ignored/untracked files for private family data or local state.
- [x] 4.3 Stage only intended public files, inspect the complete staged file list and diff, and create a baseline commit; verify the commit contains no ignored local state, secret material, or unrelated files and leaves the worktree clean.

## 5. Public GitHub Repository

- [x] 5.1 Re-check that `StarQuantix/KinOS` does not exist, the authenticated GitHub account has organization repository-creation authority, and no conflicting `origin` exists; stop without mutation on any conflict and report the evidence.
- [ ] 5.2 Create `StarQuantix/KinOS` as a public GitHub repository, set it as `origin`, and push the verified local `HEAD` to remote `main`; verify `origin` targets the canonical repository and GitHub reports public visibility with `main` as the default branch.
- [ ] 5.3 Inspect the public repository after push; verify the README renders, GitHub detects the MIT license, governance CI starts or passes, and the public tree matches the reviewed commit.
