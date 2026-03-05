# System Overview

## Purpose

OpenSpec is an AI-native, spec-driven development system. It provides a structured workflow for
proposing, implementing, and archiving changes to a codebase using markdown-based specifications
that both humans and AI agents can read and act on.

## Three-Layer Architecture

The repository is organized into three layers to separate concerns:

```
openspec/
├── architecture/          # Layer 1 — System & module documentation (this layer)
│   ├── system-overview.md # High-level system description for AI agents
│   └── module-overview.md # Per-module breakdown for AI agents
├── specs/                 # Layer 2 — Feature specifications (current deployed capabilities)
│   ├── spec-index.md      # Index of all active specs
│   └── [capability]/      # One directory per spec
│       ├── spec.md        # WHAT and WHY (behavior contracts)
│       └── design.md      # HOW (optional, for complex patterns)
└── changes/               # Layer 3 — Change management
    ├── [change-name]/     # Active change under development
    │   ├── proposal.md    # Why, what, and impact
    │   ├── tasks.md       # Implementation checklist
    │   ├── design.md      # Technical decisions (optional)
    │   └── specs/         # Future state of affected specs
    └── archive/           # Completed and merged changes
```

## Development Loop

```
Change → Spec → AI code generation → Tests → Spec update → Archive change
```

1. A change is proposed in `openspec/changes/<change-name>/`.
2. The proposal describes intent; the `specs/` sub-directory holds the future state of all
   affected capability specs.
3. AI agents read these specs and generate code + tests.
4. Once implemented and verified, the change is archived to `openspec/changes/archive/`.
5. The canonical specs in `openspec/specs/` are updated to reflect the merged state.

## AI Agent Contract

AI agents interacting with this repository MUST follow this reading order:

| Step | Read | Purpose |
|------|------|---------|
| 1 | `openspec/architecture/system-overview.md` | Understand overall system structure |
| 2 | `openspec/architecture/module-overview.md` | Understand per-module responsibilities |
| 3 | `openspec/specs/spec-index.md` | Discover all active capability specs |
| 4 | `openspec/specs/<capability>/spec.md` | Understand specific feature behavior |
| 5 | `openspec/changes/<name>/proposal.md` | Understand what is changing and why |
| 6 | `openspec/changes/<name>/specs/` | Understand the target state of affected specs |

## Technology Stack

| Concern | Choice |
|---------|--------|
| Language | TypeScript (ESM modules) |
| Runtime | Node.js ≥ 20.19.0 |
| Package manager | pnpm |
| CLI framework | Commander.js |
| Build | `node build.js` (custom esbuild wrapper) |
| Test runner | Vitest |
| Linter | ESLint (flat config) |

## Cross-Platform Requirements

- All file paths use `path.join()` / `path.resolve()` — never hardcoded slashes.
- Tests use `path.join()` for expected path values.
- The CLI runs on macOS, Linux, and Windows.
