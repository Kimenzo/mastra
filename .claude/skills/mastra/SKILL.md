```markdown
# mastra Development Patterns

> Auto-generated skill from repository analysis

## Overview

This skill teaches the core development patterns and workflows used in the `mastra` TypeScript codebase. You'll learn how to follow the project's coding conventions, manage releases, add features, maintain changelogs, regenerate provider registries, and write effective tests. The repository is structured as a multi-package monorepo, with a focus on clear commit practices and automation for common tasks.

## Coding Conventions

- **Language:** TypeScript
- **Framework:** None detected (custom architecture)
- **File Naming:** Use `camelCase` for files and folders.
  - Example: `agentLogic.ts`, `providerRegistry.json`
- **Import Style:** Use relative imports.
  - Example:
    ```typescript
    import agentLogic from './agentLogic'
    ```
- **Export Style:** Use default exports.
  - Example:
    ```typescript
    export default function agentLogic() { ... }
    ```
- **Commit Messages:** Follow [Conventional Commits](https://www.conventionalcommits.org/) with prefixes like `fix`, `chore`, `feat`.
  - Example: `feat(server): add new API endpoint for user profiles`

## Workflows

### Package Version Bump and Changelog Update
**Trigger:** When preparing for a new release, prerelease, or after merging significant changes.  
**Command:** `/bump-version`

1. Update `.changeset/pre.json` to enter or exit prerelease mode, or mark a version bump.
2. Update `package.json` and `CHANGELOG.md` files for all relevant packages (client, server, adapters, observability, etc).
3. Commit all updated files together.

**Example:**
```bash
# Enter prerelease mode
npx changeset pre enter beta

# Bump versions and update changelogs
npx changeset version

# Commit changes
git add .changeset/pre.json **/package.json **/CHANGELOG.md
git commit -m "chore(release): bump versions and update changelogs"
```

---

### Add Feature with Docs, Tests, and Examples
**Trigger:** When adding a major new API, endpoint, or capability.  
**Command:** `/new-feature`

1. Implement the feature in the appropriate package (e.g., add API handler, update agent logic).
2. Add or modify schema files as needed.
3. Add or update tests for the new feature.
4. Update or add documentation files (e.g., `docs/src/content/en/docs`, `reference`).
5. Add or update example/demo code in `examples/`.

**Example:**
```typescript
// packages/server/src/server/handlers/newFeature.ts
export default function newFeatureHandler(req, res) {
  // Implementation here
}
```
```typescript
// packages/server/src/server/handlers/newFeature.test.ts
import newFeatureHandler from './newFeature'
import { describe, it, expect } from 'vitest'

describe('newFeatureHandler', () => {
  it('should handle the request', () => {
    // Test logic here
  })
})
```

---

### Add or Update Changeset for Release
**Trigger:** When a PR introduces a fix or feature that should be included in release notes.  
**Command:** `/add-changeset`

1. Create or update one or more `.changeset/*.md` files describing the change.
2. Commit `.changeset/*.md` with related code changes.

**Example:**
```markdown
# .changeset/awesome-feature.md
---
"@mastra/server": minor
---

Add support for the awesome new feature in the server package.
```

---

### Regenerate Provider Registry and Docs
**Trigger:** When model providers are added/updated or on a regular schedule.  
**Command:** `/regenerate-providers`

1. Regenerate `packages/core/src/llm/model/provider-registry.json` and `provider-types.generated.d.ts`.
2. Update documentation in `docs/src/content/en/models` and related files.
3. Commit all updated files together.

**Example:**
```bash
# Run the script to regenerate provider registry
npm run generate:providers

# Commit changes
git add packages/core/src/llm/model/provider-registry.json \
        packages/core/src/llm/model/provider-types.generated.d.ts \
        docs/src/content/en/models/
git commit -m "chore: regenerate provider registry and update docs"
```

---

### Fix or Improve Feature with Test
**Trigger:** When a bug is found or a small improvement is needed.  
**Command:** `/fix-feature`

1. Modify implementation file(s) to fix the issue.
2. Update or add corresponding test files.
3. Optionally, add a `.changeset/*.md` entry.

**Example:**
```typescript
// packages/core/src/agent/feature.ts
export default function improvedFeature() {
  // Bug fix or improvement here
}
```
```typescript
// packages/core/src/agent/feature.test.ts
import improvedFeature from './feature'
import { describe, it, expect } from 'vitest'

describe('improvedFeature', () => {
  it('should work as expected', () => {
    // Updated test logic here
  })
})
```

## Testing Patterns

- **Framework:** [vitest](https://vitest.dev/)
- **Test File Pattern:** `*.test.ts` (tests live alongside implementation files)
- **Example:**
  ```typescript
  // packages/core/src/agent/agentLogic.test.ts
  import agentLogic from './agentLogic'
  import { describe, it, expect } from 'vitest'

  describe('agentLogic', () => {
    it('should perform its task', () => {
      expect(agentLogic()).toBeDefined()
    })
  })
  ```

## Commands

| Command              | Purpose                                                     |
|----------------------|-------------------------------------------------------------|
| /bump-version        | Bump package versions and update changelogs for a release   |
| /new-feature         | Add a new feature with docs, tests, and examples            |
| /add-changeset       | Add or update a changeset for release notes                 |
| /regenerate-providers| Regenerate provider registry and update related docs         |
| /fix-feature         | Apply a bug fix or improvement with corresponding test      |
```