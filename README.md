# KinOS

KinOS is an open-source family coordination project from [StarQuantix](https://github.com/StarQuantix). Its goal is one calm, trustworthy, private place where a household can manage everyday life together.

This project is in its foundation and discovery stage. There is no production application or selected technology stack yet. Shared tasks, recipes, personal finances, household chores, and reminders are opportunity areas—not implemented or committed features.

Canonical repository: [github.com/StarQuantix/KinOS](https://github.com/StarQuantix/KinOS)

## OpenSpec is the source of truth

All meaningful product and engineering changes use [OpenSpec](https://openspec.dev/):

- [`openspec/config.yaml`](openspec/config.yaml) contains shared mission, principles, boundaries, and artifact rules.
- [`openspec/specs/`](openspec/specs/) contains accepted requirements describing current behavior.
- [`openspec/changes/`](openspec/changes/) contains proposed and active work.
- [`AGENTS.md`](AGENTS.md) is the vendor-neutral collaboration contract.

The workflow is explore → propose → review → apply → verify → archive. Chat history, implementation code, and vendor-specific agent state do not silently override accepted specifications.

Tool-specific OpenSpec commands are generated for Codex, Kimi Code, Antigravity, and OpenCode. Other contributors and agents follow `AGENTS.md` and the same repository-local OpenSpec artifacts.

## Engineering baseline

Verification is proportional to risk and happens at the lowest effective level:

- **Unit tests** cover isolated domain and decision logic, including boundaries and failures.
- **Integration tests** cover persistence, networking, files, processes, provider adapters, and other component boundaries.
- **End-to-end tests** cover critical family workflows such as authentication, authorization, deletion, reminders, and financial-data handling once those workflows exist.
- **Security tests** cover trust boundaries, allowed and denied access, validation, secret handling, data exposure, and safe failures.

The change that selects the application stack must define repeatable local and CI commands for formatting, static analysis or linting, applicable type checks, automated tests, builds, dependency review, and security checks. Until runtime code exists, governance CI validates OpenSpec and scans committed content for secrets.

DRY means one authoritative home for knowledge that must change together. It does not mean extracting every similar-looking block: an abstraction must represent a stable shared concept and be easier to understand and test than the duplication it replaces.

Dependencies must be necessary, version-constrained, license-compatible, and reviewable for maintenance and known vulnerabilities. Verification reports must state what actually ran, what did not run, and any remaining risk.

## Security and privacy

KinOS is intended for sensitive household data. Never commit credentials, secrets, private family records, or real financial data; use synthetic examples. Changes involving identity, permissions, sharing, deletion, external providers, reminders, or financial information require an explicit security and privacy review in their OpenSpec artifacts.

If you discover a vulnerability, do not open a public issue containing exploit details or private data. Contact the StarQuantix repository maintainers through GitHub so a private reporting path can be coordinated.

## AI integration policy

Approved options for future AI-backed features are:

- DeepSeek API
- Codex CLI
- Kimi CLI

No provider is implemented, configured, or selected by default today. Future features must use provider-neutral capability boundaries, keep provider-specific behavior in adapters, protect API credentials, invoke CLI processes without shell interpolation, minimize family data disclosure, and treat model output as untrusted input. A provider failure must not corrupt or block the underlying family workflow.

## Contributing

Install Node.js 20.19 or newer and OpenSpec, then inspect current work:

```sh
npm install -g @fission-ai/openspec@latest
openspec list --specs
openspec list
openspec doctor
```

Before making a meaningful change:

1. Read [`AGENTS.md`](AGENTS.md) and [`openspec/config.yaml`](openspec/config.yaml).
2. Explore unclear needs without changing product truth.
3. Create or continue an OpenSpec change and review its proposal, specs, design, and tasks.
4. Implement only the approved scope with proportionate tests.
5. Report concrete verification evidence and archive the completed change.

Stack-specific setup and quality commands will be documented when the application stack is selected.

## License

KinOS is licensed under the [MIT License](LICENSE). Copyright (c) 2026 StarQuantix.
