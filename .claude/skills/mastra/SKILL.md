```markdown
# mastra Development Patterns

> Auto-generated skill from repository analysis

## Overview

This skill teaches the core development patterns, coding conventions, and common workflows used in the `mastra` TypeScript codebase. It covers file organization, commit conventions, testing strategies, and step-by-step guides for frequent tasks such as releasing, adding features, updating APIs, and managing provider registries. The goal is to help contributors quickly align with the project's standards and streamline their workflow.

## Coding Conventions

- **File Naming:** Use `camelCase` for file names.
  - Example: `myFeatureHandler.ts`
- **Import Style:** Use relative imports.
  - Example:
    ```typescript
    import myUtil from '../utils/myUtil'
    ```
- **Export Style:** Use default exports.
  - Example:
    ```typescript
    export default function myFunction() { ... }
    ```
- **Commit Messages:** Follow [Conventional Commits](https://www.conventionalcommits.org/) with prefixes like `fix:`, `chore:`, and `feat:`.
  - Example:
    ```
    feat: add support for custom provider configs
    ```

## Workflows

### Package Version Bump and Changelog Update
**Trigger:** When releasing a new version, entering/exiting prerelease mode, or after a batch of changes is ready for publication.  
**Command:** `/release`

1. Update `.changeset/pre.json` to reflect the new version or prerelease state.
2. Update `package.json` and `CHANGELOG.md` in all affected packages.
3. Commit all updated files together.

**Example commit:**
```
chore: release v1.2.0 and update changelogs
```

### Add Feature or Fix with Changeset
**Trigger:** When implementing a new feature or bugfix that should be tracked for release notes and versioning.  
**Command:** `/feature`

1. Implement the feature or fix in the relevant source files.
2. Add or update tests if applicable.
3. Create a `.changeset/*.md` file describing the change.
4. Commit all files together.

**Example changeset file (`.changeset/feature-new-api.md`):**
```markdown
---
"mastra": minor
---

Add new API endpoint for user profile management.
```

### Add or Update API Endpoint
**Trigger:** When a new API route is needed or an existing route requires changes.  
**Command:** `/new-endpoint`

1. Create or modify the handler in `packages/server/src/server/handlers/*.ts`.
2. Update or add the schema in `packages/server/src/server/schemas/*.ts`.
3. Update the server-adapter route in `packages/server/src/server/server-adapter/routes/*.ts`.
4. Add or update tests in `packages/server/src/server/handlers/*.test.ts`.
5. Update documentation in `docs/src/content/en/reference/server/routes.mdx` or related docs.

**Example handler:**
```typescript
// packages/server/src/server/handlers/getUserProfile.ts
export default function getUserProfile(req, res) {
  // handler logic
}
```

### Regenerate Provider Registry and Model Docs
**Trigger:** When new models/providers are added or updated, or as part of automated documentation sync.  
**Command:** `/regenerate-providers`

1. Regenerate `packages/core/src/llm/model/provider-registry.json`.
2. Regenerate `packages/core/src/llm/model/provider-types.generated.d.ts`.
3. Update documentation in `docs/src/content/en/models/**/*.mdx`.
4. Commit all regenerated files together.

**Example commit:**
```
chore: regenerate provider registry and update model docs
```

### Add ECC Bundle or Agent Skill
**Trigger:** When onboarding a new agent, skill, or ECC bundle for the system.  
**Command:** `/add-ecc-bundle`

1. Create a new ECC bundle or skill definition file in one of:
   - `.claude/commands/`
   - `.codex/agents/`
   - `.agents/skills/`
2. Commit the new file.

**Example:**
```yaml
# .agents/skills/myNewSkill.yaml
name: myNewSkill
description: Custom agent skill for advanced routing
```

## Testing Patterns

- **Framework:** [vitest](https://vitest.dev/)
- **Test File Pattern:** Files end with `.test.ts`
  - Example: `myFeature.test.ts`
- **Test Example:**
    ```typescript
    import { describe, it, expect } from 'vitest'
    import myFunction from './myFunction'

    describe('myFunction', () => {
      it('should return true', () => {
        expect(myFunction()).toBe(true)
      })
    })
    ```

## Commands

| Command                | Purpose                                                      |
|------------------------|--------------------------------------------------------------|
| /release               | Bump package versions and update changelogs for a release    |
| /feature               | Add a new feature or fix with a changeset                    |
| /new-endpoint          | Add or update an API endpoint and related documentation      |
| /regenerate-providers  | Regenerate provider registry and update model docs           |
| /add-ecc-bundle        | Add a new ECC bundle, agent skill, or configuration file     |
```