```markdown
# mastra Development Patterns

> Auto-generated skill from repository analysis

## Overview

This skill teaches you the core development patterns, coding conventions, and common workflows used in the `mastra` TypeScript codebase. The repository is organized as a monorepo with multiple packages, uses conventional commits, and emphasizes test-driven development, changelog management, and documentation updates as part of its workflows. No specific framework is enforced, but best practices for modular TypeScript projects are followed.

## Coding Conventions

- **File Naming:**  
  Use `camelCase` for file names.  
  _Example:_  
  ```
  getUserData.ts
  apiResponseHandler.ts
  ```

- **Import Style:**  
  Use **relative imports** for internal modules.  
  _Example:_  
  ```ts
  import getUserData from './getUserData'
  import { validateSchema } from '../utils/validateSchema'
  ```

- **Export Style:**  
  Use **default exports** for modules.  
  _Example:_  
  ```ts
  // getUserData.ts
  const getUserData = () => { /* ... */ }
  export default getUserData
  ```

- **Commit Messages:**  
  Follow the **conventional commit** style with prefixes like `fix:`, `feat:`, and `chore:`.  
  _Example:_  
  ```
  feat: add support for custom API endpoints
  fix: resolve issue with provider registry update
  ```

## Workflows

### Package Version Bump and Changelog Update
**Trigger:** When preparing for a new release, prerelease, or after merging significant changes.  
**Command:** `/version-bump`

1. Update `.changeset/pre.json` to enter/exit prerelease or mark a new version.
2. Update `package.json` and `CHANGELOG.md` for each affected package.
3. Optionally, add or update `.changeset/*.md` files with release notes.

_Example:_
```bash
# Enter prerelease mode
npx changeset pre enter beta

# Bump versions and update changelogs
npx changeset version

# Exit prerelease mode
npx changeset pre exit
```

### Add or Update API Endpoint
**Trigger:** When introducing a new API route or modifying an existing endpoint.  
**Command:** `/new-api-endpoint`

1. Create or update handler file in `packages/server/src/server/handlers/` (e.g., `responses.ts`).
2. Update or create corresponding schema in `packages/server/src/server/schemas/`.
3. Add or update tests in `packages/server/src/server/handlers/*.test.ts`.
4. Update or create route in `packages/server/src/server/server-adapter/routes/`.
5. Update client SDKs if needed (e.g., `client-sdks/client-js/src/resources/`).
6. Update documentation in `docs/src/content/en/reference/client-js/` or similar.

_Example handler:_
```ts
// packages/server/src/server/handlers/newEndpoint.ts
const newEndpoint = (req, res) => {
  // implementation
}
export default newEndpoint
```

### Feature Development with Tests and Docs
**Trigger:** When adding significant new functionality to the codebase.  
**Command:** `/feature`

1. Implement the feature in relevant source files.
2. Add or update tests (unit/integration) for the new feature.
3. Update or create documentation in `docs/`.
4. Add a `.changeset/*.md` entry describing the feature.

_Example changeset entry:_
```md
---
"packages/core": minor
---

Add support for advanced filtering in the API.
```

### Bugfix with Changeset and Tests
**Trigger:** When a bug is discovered and needs to be resolved.  
**Command:** `/bugfix`

1. Fix the bug in the relevant source file(s).
2. Add or update a `.changeset/*.md` file describing the fix.
3. Update or add tests to verify the bug is fixed.

_Example test:_
```ts
// packages/core/src/utils/fixBug.test.ts
import fixBug from './fixBug'

test('should resolve the bug', () => {
  expect(fixBug()).toBe(true)
})
```

### Regenerate Provider Registry and Model Docs
**Trigger:** When new model providers are added or existing ones are updated.  
**Command:** `/regenerate-providers`

1. Regenerate `packages/core/src/llm/model/provider-registry.json` and `provider-types.generated.d.ts`.
2. Update `docs/src/content/en/models/index.mdx` and related provider `.mdx` files.
3. Optionally, add or update `.changeset/*.md` entries.

_Example:_
```bash
# Regenerate provider registry (assumed script)
npm run generate:providers
```

## Testing Patterns

- **Framework:** [vitest](https://vitest.dev/)
- **Test File Pattern:** Files should be named with `.test.ts` suffix and placed alongside or near the code under test.
- **Test Example:**
  ```ts
  // packages/server/src/server/handlers/exampleHandler.test.ts
  import exampleHandler from './exampleHandler'

  test('returns correct response', () => {
    const result = exampleHandler({ /* mock req */ })
    expect(result).toEqual({ /* expected */ })
  })
  ```

## Commands

| Command                | Purpose                                                         |
|------------------------|-----------------------------------------------------------------|
| /version-bump          | Bump package versions and update changelogs for a new release   |
| /new-api-endpoint      | Add or update an API endpoint, schema, tests, and docs          |
| /feature               | Start a new feature with implementation, tests, and docs        |
| /bugfix                | Fix a bug, add a changeset entry, and update/add tests          |
| /regenerate-providers  | Regenerate provider registry and update model/provider docs      |
```
