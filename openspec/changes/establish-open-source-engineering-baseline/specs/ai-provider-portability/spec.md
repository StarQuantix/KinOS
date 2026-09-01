## Purpose

Defines safe, replaceable AI integration boundaries so KinOS can use approved API or local CLI providers without coupling family workflows or sensitive data to one vendor.

## ADDED Requirements

### Requirement: AI integrations use approved provider options
KinOS AI features SHALL use only an explicitly configured adapter for an approved option: DeepSeek API, Codex CLI, or Kimi CLI. No provider SHALL be assumed to exist, be authenticated, or be the default unless a later approved change defines that behavior.

#### Scenario: No AI provider is configured
- **WHEN** a KinOS workflow reaches an optional AI capability without a configured provider
- **THEN** the system reports that AI is unavailable and preserves the underlying family workflow and data

#### Scenario: An unsupported provider is requested
- **WHEN** configuration names an AI provider outside the approved options
- **THEN** the system rejects the configuration with an actionable error and does not send data or launch a process

### Requirement: Product behavior is provider-portable
Product workflows SHALL depend on provider-neutral AI capabilities and results rather than vendor-specific commands or response formats. Provider-specific features MUST be isolated behind an adapter and exposed only through explicit capability detection or provider-specific optional behavior.

#### Scenario: The configured provider changes
- **WHEN** an operator switches between compatible approved providers
- **THEN** supported product workflows continue through the common capability contract without changing stored family data formats

#### Scenario: A provider lacks an optional capability
- **WHEN** a workflow requests an AI capability the configured provider does not support
- **THEN** the system reports the limitation or uses a specified non-AI fallback without silently substituting different behavior

### Requirement: Credentials and process execution are protected
API credentials SHALL be supplied through an approved secret mechanism and MUST NOT be committed, displayed to users, included in prompts, or written to ordinary logs. CLI integrations SHALL invoke validated executables and structured arguments without interpolating untrusted content into a shell command.

#### Scenario: A CLI prompt contains shell metacharacters
- **WHEN** untrusted prompt content includes shell metacharacters or command-like text
- **THEN** the content is passed as data and cannot alter the executable or argument structure

#### Scenario: Diagnostic output is recorded
- **WHEN** an AI adapter records an error or diagnostic event
- **THEN** credentials and sensitive prompt or response content are absent or redacted according to the approved logging policy

### Requirement: Family data is minimized and visible to the user
An AI integration SHALL send only the data necessary for the approved capability. Before family or financial data is transmitted to an external API or exposed to a local AI process, the product behavior SHALL make the data use and relevant provider boundary clear and apply the approved consent, authorization, and retention rules.

#### Scenario: An AI request can omit unrelated family data
- **WHEN** a feature prepares an AI request for one household item
- **THEN** unrelated household items, credentials, private member data, and unnecessary identifiers are excluded

### Requirement: AI failures are bounded and observable
Every AI adapter SHALL support bounded execution, cancellation where technically available, normalized error reporting, and safe handling of malformed, partial, or untrusted model output. AI output MUST NOT directly perform irreversible or security-sensitive actions without validation and any approval required by the product specification.

#### Scenario: An AI provider times out
- **WHEN** the configured provider exceeds the approved execution limit
- **THEN** the request terminates or is abandoned safely, the user receives a useful failure state, and underlying family data remains consistent

#### Scenario: AI proposes a sensitive action
- **WHEN** model output requests deletion, sharing, financial mutation, permission change, or another sensitive action
- **THEN** the output is treated as untrusted input and cannot execute the action without deterministic validation and required user confirmation
