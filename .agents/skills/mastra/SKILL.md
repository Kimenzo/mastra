```markdown
# mastra Development Patterns

> Auto-generated skill from repository analysis

## Overview

This skill teaches you the core development patterns, coding conventions, and automated workflows used in the `mastra` TypeScript codebase. You'll learn how to structure code, write and organize tests, follow commit conventions, and execute common workflows such as package releases, API endpoint additions, observability adapter integration, provider registry regeneration, and ECC bundle management.

## Coding Conventions

- **File Naming:** Use `camelCase` for file names.
  - Example: `myHandler.ts`, `userSchema.ts`
- **Import Style:** Use relative imports.
  - Example:
    ```typescript
    import myUtil from './utils/myUtil'
    ```
- **Export Style:** Use default exports.
  - Example:
    ```typescript
    export default function myFunction() { ... }
    ```
- **Commit Messages:** Follow [Conventional Commits](https://www.conventionalcommits.org/) with prefixes like `fix:`, `feat:`, `chore:`.
  - Example: `feat: add user authentication middleware`

## Workflows

### Package Versioning and Release
**Trigger:** When preparing to release new versions of packages or entering/exiting prerelease mode  
**Command:** `/release-packages`

1. Update `.changeset/pre.json` to enter or exit prerelease mode.
2. Update `package.json` and `CHANGELOG.md` files for all affected packages.
3. Optionally add or update `.changeset/*.md` files describing the changes.
4. Commit with a relevant message (e.g., `chore: release packages`).

**Example:**
```bash
# Enter prerelease mode
npx changeset pre enter beta

# Bump versions and update changelogs
npx changeset version

# Exit prerelease mode
npx changeset pre exit
```

### Add New API Endpoint
**Trigger:** When adding a new API endpoint to the server  
**Command:** `/new-endpoint`

1. Create or update a handler file in `packages/server/src/server/handlers/`.
2. Update or add a schema in `packages/server/src/server/schemas/`.
3. Add or update a route in `packages/server/src/server/server-adapter/routes/`.
4. Write or update tests for the handler (`*.test.ts`).
5. Update documentation in `docs/src/content/en/reference/server/routes.mdx` or related docs.

**Example:**
```typescript
// packages/server/src/server/handlers/myNewEndpoint.ts
export default function myNewEndpointHandler(req, res) {
  // handler logic
}
```

### Add or Update Observability Adapter
**Trigger:** When adding or updating an observability storage backend  
**Command:** `/add-observability-adapter`

1. Add or update adapter code in `stores/{adapter}/src/storage/domains/observability/`.
2. Add or update DDL/schema files for the adapter.
3. Write or update analytics/query helpers.
4. Add or update tests for the adapter.
5. Update record-builders and related core logic for schema compatibility.

**Example:**
```typescript
// stores/clickhouse/src/storage/domains/observability/myAdapter.ts
export default function storeObservabilityRecord(record) {
  // adapter logic
}
```

### Regenerate Provider Registry and Model Docs
**Trigger:** When new models/providers are added or existing ones are updated  
**Command:** `/regenerate-providers`

1. Regenerate `packages/core/src/llm/model/provider-registry.json`.
2. Regenerate `packages/core/src/llm/model/provider-types.generated.d.ts`.
3. Update documentation in `docs/src/content/en/models/**/*.mdx`.

**Example:**
```bash
# Run the script to regenerate provider registry
npm run generate:providers
```

### Add mastra ECC Bundle
**Trigger:** When introducing a new ECC bundle for mastra features or capabilities  
**Command:** `/add-ecc-bundle`

1. Add a new file under one of:
    - `.claude/commands/`
    - `.claude/homunculus/instincts/inherited/`
    - `.codex/agents/`
    - `.codex/`
    - `.agents/skills/mastra/`
    - `.claude/skills/mastra/`
2. Commit with a message referencing the ECC bundle.

**Example:**
```markdown
# .agents/skills/mastra/myNewSkill.yaml
name: My New Skill
description: Adds a new capability to mastra
```

## Testing Patterns

- **Framework:** [vitest](https://vitest.dev/)
- **Test File Pattern:** Name test files as `*.test.ts` and place them next to the code under test.
- **Example:**
  ```typescript
  // packages/server/src/server/handlers/myHandler.test.ts
  import { describe, it, expect } from 'vitest'
  import myHandler from './myHandler'

  describe('myHandler', () => {
    it('should handle requests', () => {
      // test logic
    })
  })
  ```

## Commands

| Command                | Purpose                                                        |
|------------------------|----------------------------------------------------------------|
| /release-packages      | Bump versions, update changelogs, and manage prerelease mode   |
| /new-endpoint          | Scaffold and document a new API endpoint                       |
| /add-observability-adapter | Add or update an observability storage adapter             |
| /regenerate-providers  | Regenerate provider registry and update model docs             |
| /add-ecc-bundle        | Add a new ECC bundle for mastra features or skills             |
```