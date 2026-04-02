```markdown
# mastra Development Patterns

> Auto-generated skill from repository analysis

## Overview

This skill teaches you how to contribute effectively to the `mastra` TypeScript monorepo. You'll learn the project's coding conventions, commit patterns, testing approach, and the main development workflows—such as releasing new versions, adding features, fixing bugs, updating API endpoints, and regenerating provider registries. This guide is designed to help you write code and collaborate in a way that's consistent with the team's established practices.

## Coding Conventions

- **Language:** TypeScript
- **Framework:** None detected
- **File Naming:** Use `camelCase` for file and directory names.
  - Example: `providerRegistry.ts`, `apiHandler.ts`
- **Import Style:** Use relative imports.
  - Example:
    ```typescript
    import myUtil from './myUtil';
    ```
- **Export Style:** Use default exports.
  - Example:
    ```typescript
    export default function myFunction() { /* ... */ }
    ```
- **Commit Messages:** Follow [Conventional Commits](https://www.conventionalcommits.org/) with prefixes like `fix`, `feat`, `chore`.
  - Example: `feat: add support for new provider registry format`

## Workflows

### Version Bump and Release
**Trigger:** When preparing a new release or prerelease of the monorepo packages.  
**Command:** `/version-bump`

1. Update `.changeset/pre.json` to enter or exit prerelease mode, or as part of a version bump.
2. Update all relevant `package.json` and `CHANGELOG.md` files across packages.
3. Add or update `.changeset/*.md` files describing the changes.
4. Commit all version, changelog, and changeset changes together.

**Example commit:**
```
chore: bump version and update changelogs for release
```

### Feature Addition with Tests and Docs
**Trigger:** When adding a new capability or API to the codebase.  
**Command:** `/new-feature`

1. Implement the feature in the relevant `src/` files.
2. Add or update corresponding test files (e.g., `*.test.ts` or `__tests__/*.test.ts`).
3. Update or add documentation files (e.g., `docs/src/content/en/...` or `README.md`).
4. Add a `.changeset/*.md` entry describing the feature.

**Example:**
```typescript
// packages/core/src/myFeature.ts
export default function myFeature() { /* ... */ }
```
```typescript
// packages/core/src/myFeature.test.ts
import myFeature from './myFeature';
import { describe, it, expect } from 'vitest';

describe('myFeature', () => {
  it('works as expected', () => {
    expect(myFeature()).toBe(/* expected value */);
  });
});
```

### Bugfix with Test and Changeset
**Trigger:** When a bug is found and needs to be fixed.  
**Command:** `/bugfix`

1. Modify the relevant source file(s) to fix the bug.
2. Add or update a test file to cover the bug scenario.
3. Add a `.changeset/*.md` file describing the fix.

**Example commit:**
```
fix: handle edge case in provider registry parsing
```

### Regenerate Provider Registry and Docs
**Trigger:** When provider models or registry entries are changed or new providers are added.  
**Command:** `/regenerate-providers`

1. Update `packages/core/src/llm/model/provider-registry.json` and `provider-types.generated.d.ts`.
2. Update `docs/src/content/en/models/index.mdx` and related provider docs.
3. Commit all generated and documentation files together.

**Example commit:**
```
chore: regenerate provider registry and update docs
```

### Add or Update API Endpoint
**Trigger:** When a new API endpoint is needed or an existing one is changed.  
**Command:** `/new-api-endpoint`

1. Create or update handler in `packages/server/src/server/handlers/*.ts`.
2. Update or add schema in `packages/server/src/server/schemas/*.ts`.
3. Add or update test in `packages/server/src/server/handlers/*.test.ts`.
4. Update docs if public API is affected.
5. Add a `.changeset/*.md` entry.

**Example:**
```typescript
// packages/server/src/server/handlers/newEndpoint.ts
export default function newEndpointHandler(req, res) { /* ... */ }
```
```typescript
// packages/server/src/server/handlers/newEndpoint.test.ts
import newEndpointHandler from './newEndpoint';
import { describe, it, expect } from 'vitest';

describe('newEndpointHandler', () => {
  it('returns expected response', () => {
    // test logic
  });
});
```

## Testing Patterns

- **Framework:** [Vitest](https://vitest.dev/)
- **Test File Pattern:** `*.test.ts` (located alongside source files or in `__tests__` directories)
- **Example Test:**
  ```typescript
  import myFunction from './myFunction';
  import { describe, it, expect } from 'vitest';

  describe('myFunction', () => {
    it('should return true', () => {
      expect(myFunction()).toBe(true);
    });
  });
  ```

## Commands

| Command               | Purpose                                                        |
|-----------------------|----------------------------------------------------------------|
| /version-bump         | Prepare and commit a new release or prerelease                 |
| /new-feature          | Add a new feature with tests and documentation                 |
| /bugfix               | Fix a bug and add/update corresponding tests and changeset     |
| /regenerate-providers | Regenerate provider registry files and update related docs     |
| /new-api-endpoint     | Add or update an API endpoint, schema, tests, and docs         |
```