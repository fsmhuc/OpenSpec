# Module Overview

## Purpose

This document describes the source-code modules that make up the OpenSpec CLI. It is intended
for AI agents that need to locate the correct file before generating or modifying code.

## Source Layout

```
src/
├── cli/             # CLI entry point — registers all top-level commands
├── commands/        # Thin command handlers (argument parsing, output formatting)
├── core/            # Business logic — all meaningful work happens here
│   ├── archive.ts
│   ├── available-tools.ts
│   ├── artifact-graph/
│   ├── command-generation/
│   ├── completions/
│   ├── config.ts / config-schema.ts / config-prompts.ts
│   ├── converters/
│   ├── global-config.ts
│   ├── init.ts
│   ├── legacy-cleanup.ts
│   ├── list.ts
│   ├── migration.ts
│   ├── parsers/
│   ├── profiles.ts / profile-sync-drift.ts
│   ├── project-config.ts
│   ├── schemas/
│   ├── shared/
│   ├── specs-apply.ts
│   ├── styles/
│   ├── templates/   # AI skill / slash-command templates (one sub-dir per workflow)
│   ├── update.ts
│   ├── validation/
│   └── view.ts
├── prompts/         # Reusable interactive prompt components (Inquirer-based)
├── telemetry/       # Anonymous usage telemetry (PostHog)
├── ui/              # ASCII art, welcome screen
└── utils/           # Shared utilities (file I/O, path helpers, item discovery)
```

## Module Responsibilities

### `src/cli/`
Registers every Commander.js command and wires it to the matching handler in `src/commands/`.
Entry point: `src/cli/index.ts`.

### `src/commands/`
One file per top-level CLI command (`change`, `completion`, `config`, `feedback`, `schema`,
`show`, `spec`, `validate`). Each file parses flags, calls into `src/core/`, and formats output.
The `workflow/` sub-directory handles the artifact-guided workflow commands.

### `src/core/`
All business logic lives here. Key responsibilities by file:

| File / Directory | Responsibility |
|-----------------|----------------|
| `init.ts` | Creates the `openspec/` directory structure and configures AI tools |
| `config.ts` / `config-schema.ts` | Reads and writes `openspec/config.yaml`; validates with Zod |
| `global-config.ts` | Reads and writes the user-level config in `~/.config/openspec/` |
| `archive.ts` | Moves a completed change from `changes/` to `changes/archive/` |
| `list.ts` | Discovers and lists specs or changes |
| `update.ts` | Regenerates AI tool skills and slash commands for a project |
| `validation/` | Validates spec files against the spec schema |
| `templates/` | Generates AI skill and slash-command template files per workflow |
| `command-generation/` | Generates CLI command artifacts for tool integrations |
| `artifact-graph/` | Builds a dependency graph of specs and changes for context injection |
| `specs-apply.ts` | Applies future-state specs from a change into `openspec/specs/` |
| `parsers/` | Parses markdown spec and change files into structured data |
| `schemas/` | Zod schemas for all data structures |
| `converters/` | Converts between internal types and serialization formats |
| `profiles.ts` | Manages named delivery profiles (skills vs. commands vs. both) |
| `shared/` | Constants, paths, and utilities shared across core modules |

### `src/prompts/`
Custom Inquirer prompt components, e.g. `searchable-multi-select.ts` used by `init` and
`update` for AI tool selection.

### `src/telemetry/`
PostHog-based anonymous telemetry. Opt-out is respected via `OPENSPEC_NO_TELEMETRY` env var.

### `src/ui/`
Terminal ASCII art and the animated welcome screen shown during `openspec init`.

### `src/utils/`
Shared helpers:

| File | Responsibility |
|------|----------------|
| `file-system.ts` | Cross-platform file read/write/delete helpers |
| `item-discovery.ts` | Finds spec and change directories on disk |
| `change-utils.ts` | Helper functions for change metadata |
| `change-metadata.ts` | Parses change frontmatter / YAML metadata |
| `match.ts` | Fuzzy-matching for spec/change name resolution |
| `interactive.ts` | Shared helpers for interactive terminal sessions |
| `shell-detection.ts` | Detects the current shell for completion setup |
| `task-progress.ts` | Ora spinner helpers for multi-step progress display |
| `command-references.ts` | Canonical list of CLI command names used by code generation |

## Key Data Flows

### `openspec init`
```
commands/workflow/new-change.ts
  → core/init.ts
    → core/config.ts          (writes config.yaml)
    → core/command-generation/ (generates tool commands)
    → core/templates/          (generates AI skill files)
```

### `openspec change archive <name>`
```
commands/change.ts
  → core/archive.ts
    → core/specs-apply.ts     (merges future-state specs into openspec/specs/)
    → utils/file-system.ts    (moves change directory to archive/)
```

### `openspec validate`
```
commands/validate.ts
  → core/validation/validator.ts
    → core/parsers/            (reads spec.md files)
    → core/schemas/            (validates against Zod schemas)
```

## Constraints for Code Generation

- **Never hardcode path separators.** Use `path.join()` / `path.resolve()`.
- **Use existing constants** from `src/core/shared/` for directory names; do not invent new ones.
- **Add new commands** by creating a file in `src/commands/` and registering it in `src/cli/index.ts`.
- **Add new core logic** in `src/core/`; do not put business logic in `src/commands/`.
- **Tests** live in `test/` and mirror the `src/` structure. Use Vitest.
