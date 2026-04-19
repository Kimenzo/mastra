```markdown
# mastra Development Patterns

> Auto-generated skill from repository analysis

## Overview
This skill introduces the core development patterns, coding conventions, and collaborative workflows used in the `mastra` TypeScript monorepo. It covers commit standards, file organization, code style, release management, API and provider registry updates, and best practices for testing and observability adapters. By following these patterns, contributors can ensure consistency, maintainability, and smooth collaboration across the codebase.

## Coding Conventions

- **File Naming:**  
  Use camelCase for file names.
  ```
  // Good
  modelProvider.ts
  apiHandler.ts

  // Bad
  model_provider.ts
  ApiHandler.ts
  ```

- **Import Style:**  
  Use relative imports within packages.
  ```typescript
  // Good
  import utils from './utils'
  import { getModel } from '../modelProvider'

  // Bad
  import utils from 'utils'
  import { getModel } from 'mastra/modelProvider'
  ```

- **Export Style:**  
  Use default exports for modules.
  ```typescript
  // Good
  export default function handler() { ... }

  // Bad
  export function handler() { ... }
  ```

- **Commit Messages:**  
  Use [Conventional Commits](https://www.conventionalcommits.org/) with these prefixes:
    - `feat`: New features
    - `fix`: Bug fixes
    - `chore`: Maintenance and tooling

  Example:
  ```
  feat: add support for new provider registry format
  fix: correct schema validation for API endpoint
  chore: update dependencies
  ```

## Workflows

### Package Version Bump and Changelog Update
**Trigger:** When preparing for a release, prerelease, or after merging significant changes.  
**Command:** `/release-packages`

1. Update `.changeset/pre.json` to enter or exit prerelease mode.
2. Update `package.json` and `CHANGELOG.md` files for all affected packages.
3. (If needed) Add new `.changeset/*.md` files describing changes.
4. Commit with a message like:
   ```
   chore: release packages
   ```
5. Push and create a release PR if not automated.

### Regenerate Provider Registry and Docs
**Trigger:** When a new model provider is added or provider metadata changes.  
**Command:** `/regenerate-providers`

1. Regenerate `packages/core/src/llm/model/provider-registry.json`.
2. Regenerate `packages/core/src/llm/model/provider-types.generated.d.ts`.
3. Update documentation in `docs/src/content/en/models/**/*.mdx`.
4. Commit with:
   ```
   chore: regenerate provider registry and docs
   ```

### Feature or Fix with Changeset
**Trigger:** When a new feature or bugfix is merged that should be tracked in the release notes.  
**Command:** `/feature-with-changeset`

1. Modify implementation files (e.g., `src/**/*.ts`, `.tsx`).
2. Add or update corresponding tests.
3. Add a `.changeset/*.md` file describing the change:
   ```markdown
   ---
   'mastra-core': minor
   ---

   Add support for new analytics endpoint.
   ```
4. Commit with a conventional message, e.g.:
   ```
   feat: add analytics endpoint (with changeset)
   ```

### Add or Update API Endpoint
**Trigger:** When a new API route is needed or an existing one is changed.  
**Command:** `/new-api-endpoint`

1. Create or modify handler in `packages/server/src/server/handlers/*.ts`.
2. Update or add schema in `packages/server/src/server/schemas/*.ts`.
3. Add or update tests in `packages/server/src/server/handlers/*.test.ts`.
4. Update route index if necessary.
5. Commit with:
   ```
   feat: add new API endpoint for [feature]
   ```

   **Example handler:**
   ```typescript
   // packages/server/src/server/handlers/newEndpoint.ts
   export default function newEndpointHandler(req, res) {
     // handler logic
   }
   ```

### Add or Update Observability Storage Adapter
**Trigger:** When supporting a new observability backend or adding analytics features.  
**Command:** `/add-observability-adapter`

1. Add or update DDL/storage logic in `stores/*/src/storage/domains/observability/**/*.ts`.
2. Add or update tests in `stores/*/src/storage/domains/observability/**/*.test.ts`.
3. Update core record builders/types if schema changes (`packages/core/src/storage/domains/observability/record-builders.ts`).
4. Commit with:
   ```
   feat: add ClickHouse observability adapter
   ```

## Testing Patterns

- **Framework:** [Vitest](https://vitest.dev/)
- **Test File Pattern:** `*.test.ts`
- **Placement:** Test files are placed alongside or near the code they test.

**Example:**
```typescript
// packages/server/src/server/handlers/myHandler.test.ts
import { describe, it, expect } from 'vitest'
import handler from './myHandler'

describe('myHandler', () => {
  it('should return 200 for valid input', () => {
    const result = handler({ /* mock req */ }, { /* mock res */ })
    expect(result.status).toBe(200)
  })
})
```

## Commands

| Command                  | Purpose                                                      |
|--------------------------|--------------------------------------------------------------|
| /release-packages        | Bump versions and update changelogs for release              |
| /regenerate-providers    | Regenerate provider registry and update documentation        |
| /feature-with-changeset  | Add a feature/fix and document it for release notes          |
| /new-api-endpoint        | Add or update an API endpoint and related schema/tests       |
| /add-observability-adapter | Add or enhance an observability storage adapter           |
```
