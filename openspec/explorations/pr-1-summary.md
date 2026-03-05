# PR #1 Summary: Add Three-Layer Architecture to openspec/

## Overview

**Title:** feat: add three-layer architecture to openspec/ for AI-assisted development
**Author:** Copilot (copilot-swe-agent)
**Status:** Open (Draft)
**Branch:** `copilot/refactor-openspec-architecture` → `main`
**Changes:** 4 files changed, 283 additions, 2 deletions (no source code or tests modified)

---

## What This PR Does

Refactors the `openspec/` directory to introduce a structured, AI-readable layout that separates system documentation, feature specs, and change management. The goal is to enable AI agents to reliably navigate the repository and generate compatible code by following a defined reading order.

---

## New Files Added

### 1. `openspec/architecture/system-overview.md`

Establishes the **three-layer architecture** of the `openspec/` directory:

```
openspec/
├── architecture/   # Layer 1 — System & module documentation
├── specs/          # Layer 2 — Active feature specifications
└── changes/        # Layer 3 — Change management (active + archive)
```

Key sections:
- **Development Loop:** `Change → Spec → AI code generation → Tests → Spec update → Archive change`
- **AI Agent Contract:** A required 6-step reading order (system-overview → module-overview → spec-index → spec.md → proposal.md → change specs)
- **Technology Stack:** TypeScript/ESM, Node.js ≥ 20.19.0, pnpm, Commander.js, Vitest, ESLint
- **Cross-Platform Requirements:** All file paths use `path.join()` / `path.resolve()`

### 2. `openspec/architecture/module-overview.md`

A detailed map of every `src/` subdirectory with:
- Full directory tree of `src/`
- Per-file responsibility table for `src/core/`, `src/utils/`, and other modules
- **Key data flows** for three core commands:
  - `openspec init`
  - `openspec change archive`
  - `openspec validate`
- **Code generation constraints:** no hardcoded separators, use existing constants, register new commands in `src/cli/index.ts`

### 3. `openspec/specs/spec-index.md`

An indexed table of all **36 active capability specs** across five categories:

| Category | Count |
|----------|-------|
| CLI Commands | 13 |
| Core System Capabilities | 10 |
| Schema Commands | 4 |
| AI Workflow Skills | 6 |
| Conventions & Telemetry | 3 |

Each entry includes a one-line description and a direct link to the corresponding `spec.md`.

---

## Other Changes

- **`package-lock.json`:** Version bump from `1.1.1` → `1.2.0`

---

## Impact

- No source code or tests were modified — this is a documentation-only change
- Provides AI agents with a structured, reliable navigation contract for the repository
- Lays the foundation for the three-layer architecture going forward
