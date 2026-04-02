```markdown
# mastra Development Patterns

> Auto-generated skill from repository analysis

## Overview

This skill teaches you how to contribute effectively to the `mastra` TypeScript monorepo. You'll learn the project's coding conventions, commit patterns, and the main workflows for adding features, managing releases, updating observability adapters, and maintaining documentation. The guide also covers how to write and organize tests, and provides handy commands for common development tasks.

---

## Coding Conventions

- **Language:** TypeScript (no framework detected)
- **File Naming:** Use `camelCase` for file names.
  - Example: `recordBuilders.ts`, `providerRegistry.json`
- **Imports:** Use relative import paths.
  - Example:
    ```typescript
    import recordBuilders from './recordBuilders';
    ```
- **Exports:** Use default exports.
  - Example:
    ```typescript
    export default function processRecord() { /* ... */ }
    ```
- **Commit Messages:** Follow [Conventional Commits](https://www.conventionalcommits.org/) with prefixes:
  - `fix:`, `feat:`, `chore:`
  - Example: `feat: add ClickHouse observability adapter`
- **Documentation:** Use Markdown (`.mdx`) for docs and examples.

---

## Workflows

### Package Version Bump and Changelog Update
**Trigger:** When preparing for a new release, prerelease, or after merging significant changes.  
**Command:** `/version-bump`

1. Update `.changeset/pre.json` to enter/exit prerelease mode or mark a new version.
2. Update `package.json` and `CHANGELOG.md` files for all relevant packages (e.g., `client`, `server`, `integrations`, `observability`).
3. Commit all updated files together.

**Example:**
```bash
# Bump version and update changelogs
/version-bump
git add .changeset/pre.json **/package.json **/CHANGELOG.md
git commit -m "chore: bump versions and update changelogs"
```

---

### Add Feature with Docs and Tests
**Trigger:** When introducing a new API endpoint, feature, or major capability.  
**Command:** `/add-feature`

1. Implement the feature in source files (e.g., add new handler, processor, or adapter).
2. Add or update related schema or type definitions.
3. Add or update tests for the new feature.
4. Add or update documentation in `docs/` or `examples/`.

**Example:**
```typescript
// packages/server/src/server/handlers/newFeature.ts
export default function newFeatureHandler(req, res) { /* ... */ }
```
```typescript
// packages/server/src/server/handlers/__tests__/newFeature.test.ts
import { describe, it, expect } from 'vitest';
import newFeatureHandler from '../newFeature';

describe('newFeatureHandler', () => {
  it('should handle requests', () => {
    // test logic
  });
});
```

---

### Add or Update Observability Storage Adapter
**Trigger:** When adding support for a new observability backend or upgrading an existing one.  
**Command:** `/add-observability-adapter`

1. Implement or update storage adapter files (e.g., `v-next/ddl.ts`, `v-next/index.ts`).
2. Add or update analytics/query helpers and discovery methods.
3. Update or add relevant tests.
4. Update core record builders and schemas if needed.
5. Document changes in a changeset.

**Example:**
```typescript
// stores/clickhouse/src/storage/domains/observability/v-next/ddl.ts
export default function createObservabilityTables() { /* ... */ }
```
```markdown
# .changeset/add-clickhouse-adapter.md
---
'@mastra/clickhouse': minor
---

Add ClickHouse observability adapter with analytics helpers.
```

---

### Regenerate Provider Registry and Docs
**Trigger:** When new models/providers are added or provider metadata changes.  
**Command:** `/regenerate-providers`

1. Regenerate `provider-registry.json` and `provider-types.generated.d.ts`.
2. Update docs for models and providers (`index.mdx`, `providers/*.mdx`).
3. Commit all regenerated files together.

**Example:**
```bash
# Regenerate provider registry and types
/regenerate-providers
git add packages/core/src/llm/model/provider-registry.json packages/core/src/llm/model/provider-types.generated.d.ts docs/src/content/en/models/
git commit -m "chore: regenerate provider registry and docs"
```

---

### Add Changeset for Feature or Bugfix
**Trigger:** When submitting a PR for a new feature, bugfix, or breaking change.  
**Command:** `/add-changeset`

1. Create a new `.changeset/*.md` file describing the change.
2. Include the changeset in the commit with the code changes.
3. The changeset will be used in the version bump workflow.

**Example:**
```markdown
# .changeset/add-new-api-endpoint.md
---
'@mastra/server': minor
---

Add new API endpoint for advanced analytics.
```

---

## Testing Patterns

- **Framework:** [Vitest](https://vitest.dev/)
- **Test File Pattern:** `*.test.ts` (unit/integration tests), often in `__tests__` directories.
- **Example Test:**
  ```typescript
  // packages/core/src/utils/__tests__/mathUtils.test.ts
  import { describe, it, expect } from 'vitest';
  import add from '../mathUtils';

  describe('add', () => {
    it('adds two numbers', () => {
      expect(add(1, 2)).toBe(3);
    });
  });
  ```
- **Location:** Tests are placed alongside source files or in `__tests__` subdirectories.

---

## Commands

| Command                  | Purpose                                                        |
|--------------------------|----------------------------------------------------------------|
| /version-bump            | Bump package versions and update changelogs for a release      |
| /add-feature             | Scaffold a new feature with docs and tests                    |
| /add-observability-adapter | Add or update an observability storage adapter                |
| /regenerate-providers    | Regenerate provider registry and update related docs           |
| /add-changeset           | Create a changeset file for a feature or bugfix               |
```
