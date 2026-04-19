```markdown
# mastra Development Patterns

> Auto-generated skill from repository analysis

## Overview

This skill teaches the key development patterns, coding conventions, and workflows used in the `mastra` TypeScript monorepo. You'll learn how to structure code, write tests, follow commit conventions, and execute common workflows such as releasing packages, adding API endpoints, developing features, updating observability adapters, and regenerating model provider registries. This guide is suitable for contributors aiming to maintain consistency and quality across the codebase.

## Coding Conventions

- **Language:** TypeScript
- **Framework:** None detected
- **File Naming:** Use `camelCase` for file names.
  - Example: `userHandler.ts`, `apiClient.ts`
- **Import Style:** Use relative imports.
  ```ts
  import userService from '../services/userService';
  ```
- **Export Style:** Use default exports.
  ```ts
  export default function myFunction() { ... }
  ```
- **Commit Messages:** Follow [Conventional Commits](https://www.conventionalcommits.org/) with prefixes like `fix`, `chore`, and `feat`.
  - Example: `feat(server): add new user endpoint`
- **Documentation:** Update or add `.mdx` files in the `docs/` directory for new features or changes.

## Workflows

### Package Version Bump and Changelog Update
**Trigger:** When preparing for a new release, prerelease, or after merging significant changes.  
**Command:** `/release`

1. Update `.changeset/pre.json` to enter or exit prerelease mode.
2. Update `package.json` and `CHANGELOG.md` files for all affected packages.
3. Add or update `.changeset/*.md` files describing the changes.
4. Commit with a message like `chore(release): bump package versions`.

**Example:**
```sh
# Enter prerelease mode
npx changeset pre enter beta

# Add a changeset
npx changeset

# Version packages and update changelogs
npx changeset version

# Exit prerelease mode
npx changeset pre exit
```

### Add or Update API Endpoint
**Trigger:** When adding a new server API route or major API feature.  
**Command:** `/new-api-endpoint`

1. Create or update a handler file in `packages/server/src/server/handlers/`.
2. Update or add a schema file in `packages/server/src/server/schemas/`.
3. Add or update a test file in `packages/server/src/server/handlers/`.
4. Update documentation in `docs/src/content/en/reference/client-js/` or `docs/src/content/en/reference/server/routes.mdx`.

**Example:**
```ts
// packages/server/src/server/handlers/createUser.ts
import { createUserSchema } from '../schemas/createUserSchema';
export default function createUser(req, res) {
  // handler logic
}
```
```ts
// packages/server/src/server/handlers/createUser.test.ts
import { describe, it, expect } from 'vitest';
import createUser from './createUser';

describe('createUser', () => {
  it('should create a user', () => {
    // test logic
  });
});
```

### Feature Development with Tests and Docs
**Trigger:** When implementing a new feature in core, UI, or SDK packages.  
**Command:** `/feature`

1. Implement the feature in the relevant source files (`packages/*/src/**/*.ts`).
2. Add or update corresponding test files (`*.test.ts`, `*.test.tsx`).
3. Update or add documentation files in `docs/src/content/en/reference/` or `docs/src/content/en/docs/`.

**Example:**
```ts
// packages/core/src/utils/newFeature.ts
export default function newFeature() { ... }
```
```ts
// packages/core/src/utils/newFeature.test.ts
import { describe, it, expect } from 'vitest';
import newFeature from './newFeature';

describe('newFeature', () => {
  it('works as expected', () => {
    expect(newFeature()).toBe(true);
  });
});
```

### Add or Update Observability Storage Adapter
**Trigger:** When introducing or upgrading a storage adapter for observability data.  
**Command:** `/add-observability-adapter`

1. Implement or update adapter code in `stores/<adapter>/src/storage/domains/observability/`.
2. Add or update DDL, analytics, and helper files.
3. Update or add test files for the adapter.
4. Update or align core record builder tests in `packages/core/src/storage/domains/observability/record-builders.test.ts`.

**Example:**
```ts
// stores/clickhouse/src/storage/domains/observability/clickhouseAdapter.ts
export default class ClickhouseAdapter { ... }
```
```ts
// stores/clickhouse/src/storage/domains/observability/clickhouseAdapter.test.ts
import { describe, it, expect } from 'vitest';
import ClickhouseAdapter from './clickhouseAdapter';

describe('ClickhouseAdapter', () => {
  it('should store observability data', () => {
    // test logic
  });
});
```

### Regenerate Model Provider Registry and Docs
**Trigger:** When new models/providers are added or provider metadata changes.  
**Command:** `/regenerate-providers`

1. Update `docs/src/content/en/models/index.mdx` and provider docs.
2. Update `packages/core/src/llm/model/provider-registry.json`.
3. Update `packages/core/src/llm/model/provider-types.generated.d.ts`.

**Example:**
```json
// packages/core/src/llm/model/provider-registry.json
{
  "providers": [
    { "name": "openai", "models": ["gpt-4", "gpt-3.5-turbo"] }
  ]
}
```
```ts
// packages/core/src/llm/model/provider-types.generated.d.ts
export type Provider = "openai" | "anthropic";
```

## Testing Patterns

- **Framework:** [vitest](https://vitest.dev/)
- **Test File Pattern:** Files end with `.test.ts`.
- **Location:** Test files are placed alongside or near the code they test.
- **Example:**
  ```ts
  // foo.test.ts
  import { describe, it, expect } from 'vitest';
  import foo from './foo';

  describe('foo', () => {
    it('returns bar', () => {
      expect(foo()).toBe('bar');
    });
  });
  ```

## Commands

| Command                   | Purpose                                                    |
|---------------------------|------------------------------------------------------------|
| /release                  | Bump package versions and update changelogs                |
| /new-api-endpoint         | Add or update an API endpoint and its documentation        |
| /feature                  | Develop a new feature with tests and docs                  |
| /add-observability-adapter| Add or update an observability storage adapter             |
| /regenerate-providers     | Regenerate model provider registry and update docs/types    |
```