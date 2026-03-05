# Spec Index

## Purpose

This index lists every active capability specification in `openspec/specs/`. Each entry links to
the corresponding `spec.md` file and provides a one-line description of the capability.

AI agents SHOULD consult this index first to locate the relevant spec before reading individual
`spec.md` files.

---

## CLI Commands

| Spec | Description |
|------|-------------|
| [cli-archive](cli-archive/spec.md) | `openspec change archive` — moves completed changes to the archive folder with date-based naming |
| [cli-artifact-workflow](cli-artifact-workflow/spec.md) | `openspec workflow` — artifact-guided workflow commands (`status`, `instructions`, `templates`) |
| [cli-change](cli-change/spec.md) | `openspec change` — show, list, and validate change proposals and deltas |
| [cli-completion](cli-completion/spec.md) | `openspec completion` — shell tab-completion for commands, flags, and dynamic values |
| [cli-config](cli-config/spec.md) | `openspec config` — view and modify global OpenSpec configuration settings |
| [cli-feedback](cli-feedback/spec.md) | `openspec feedback` — create GitHub issues or provide a manual fallback URL |
| [cli-init](cli-init/spec.md) | `openspec init` — create OpenSpec directory structure and configure AI tools |
| [cli-list](cli-list/spec.md) | `openspec list` — list all active changes with task completion status |
| [cli-show](cli-show/spec.md) | `openspec show` — interactive and direct display of change and spec content |
| [cli-spec](cli-spec/spec.md) | `openspec spec` — list, show, and validate source-of-truth specifications |
| [cli-update](cli-update/spec.md) | `openspec update` — update AI agent instructions when new versions are released |
| [cli-validate](cli-validate/spec.md) | `openspec validate` — validate changes and specs with actionable remediation guidance |
| [cli-view](cli-view/spec.md) | `openspec view` — dashboard view of specs, changes, and progress metrics |

## Core System Capabilities

| Spec | Description |
|------|-------------|
| [ai-tool-paths](ai-tool-paths/spec.md) | AI tool path metadata used to generate skills and commands in tool-specific directories |
| [artifact-graph](artifact-graph/spec.md) | Artifact graph model, dependency validation, and completion-state logic for schema-driven workflows |
| [change-creation](change-creation/spec.md) | Programmatic utilities for creating and validating OpenSpec change directories |
| [command-generation](command-generation/spec.md) | Tool-agnostic command content and adapter contracts for generating tool-specific command files |
| [config-loading](config-loading/spec.md) | Discovery, parsing, validation, and safe fallback for `openspec/config.yaml` |
| [context-injection](context-injection/spec.md) | Injection of project context from `openspec/config.yaml` into workflow instructions |
| [global-config](global-config/spec.md) | User-level global configuration with XDG Base Directory support and schema evolution rules |
| [instruction-loader](instruction-loader/spec.md) | Loading, validation, and enrichment of instruction templates from schema directories |
| [legacy-cleanup](legacy-cleanup/spec.md) | Detection and cleanup of legacy OpenSpec artifacts during `init` and `update` |
| [schema-resolution](schema-resolution/spec.md) | Project-local schema resolution with precedence order and backward-compatible fallback |

## Schema Commands

| Spec | Description |
|------|-------------|
| [schema-fork-command](schema-fork-command/spec.md) | `openspec schema fork` — clone existing schemas into project-local schemas |
| [schema-init-command](schema-init-command/spec.md) | `openspec schema init` — create project-local schema skeletons |
| [schema-validate-command](schema-validate-command/spec.md) | `openspec schema validate` — validate schema syntax, structure, templates, and dependency graphs |
| [schema-which-command](schema-which-command/spec.md) | `openspec schema which` — report resolved schema source and location |

## AI Workflow Skills

| Spec | Description |
|------|-------------|
| [docs-agent-instructions](docs-agent-instructions/spec.md) | Authoring standards for generated agent instruction docs |
| [opsx-archive-skill](opsx-archive-skill/spec.md) | `/opsx:archive` — readiness checks, spec sync, and archive execution |
| [opsx-onboard-skill](opsx-onboard-skill/spec.md) | `/opsx:onboard` — guide users through an end-to-end OpenSpec workflow |
| [opsx-verify-skill](opsx-verify-skill/spec.md) | `/opsx:verify` — assess implementation completeness against change artifacts |
| [rules-injection](rules-injection/spec.md) | Injection of per-artifact rules from project config into generated instructions |
| [specs-sync-skill](specs-sync-skill/spec.md) | Agent skill for syncing delta specs from changes to main specs |

## Conventions & Telemetry

| Spec | Description |
|------|-------------|
| [ci-nix-validation](ci-nix-validation/spec.md) | CI validation of Nix flake builds and maintenance scripts |
| [openspec-conventions](openspec-conventions/spec.md) | Meta-spec defining structured spec format, change management conventions, and project structure |
| [telemetry](telemetry/spec.md) | Anonymous usage telemetry with PostHog, opt-out support, and privacy-preserving event design |
