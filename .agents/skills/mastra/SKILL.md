```markdown
# mastra Development Patterns

> Auto-generated skill from repository analysis

## Overview

This skill teaches the core development patterns, coding conventions, and collaborative workflows used in the `mastra` TypeScript monorepo. You'll learn how to structure code, write and organize tests, follow commit conventions, and execute common release and contribution workflows using standardized commands. This guide is ideal for new contributors or anyone seeking to understand and participate effectively in the `mastra` project.

## Coding Conventions

- **Language:** TypeScript (no framework detected)
- **File Naming:** Use `camelCase` for file and directory names.
  - Example: `providerRegistry.ts`, `myFeatureHandler.ts`
- **Import Style:** Use relative imports.
  - Example:
    ```typescript
    import myUtil from './myUtil';
    ```
- **Export Style:** Use default exports.
  - Example:
    ```typescript
    export default function myFunction() { ... }
    ```
- **Commit Messages:** Use [Conventional Commits](https://www.conventionalcommits.org/) with prefixes like `fix:`, `feat:`, `chore:`.
  - Example: `fix: correct typo in provider registry`
- **Documentation:** Update or add markdown files in `docs/src/content` or `README.md` when adding features or making changes.

## Workflows

### Package Version Bump and Changelog Update

**Trigger:** When preparing for a release, prerelease, or after merging significant changes.  
**Command:** `/version-bump`

1. Update `.changeset/pre.json` to enter or exit prerelease mode as needed.
2. Update `package.json` and `CHANGELOG.md` for all affected packages (e.g., `client`, `deployers`, `integrations`, `observability`, `core`, etc.).
3. Commit all updated files together.

**Files involved:**
- `.changeset/pre.json`
- `*/CHANGELOG.md`
- `*/package.json`

---

### Add Feature with Docs and Tests

**Trigger:** When introducing a new API, processor, or major capability.  
**Command:** `/feature`

1. Implement the feature in the relevant source files.
   - Example: `packages/my-package/src/newFeature.ts`
2. Add or update related test files.
   - Example: `packages/my-package/src/newFeature.test.ts`
3. Add or update documentation files.
   - Example: `docs/src/content/en/new-feature.mdx` or update `README.md`
4. Add a `.changeset/*.md` entry describing the change.

---

### Bugfix with Changeset and Tests

**Trigger:** When a bug is discovered and needs to be fixed.  
**Command:** `/fix`

1. Fix the bug in the relevant source file(s).
   - Example: `packages/core/src/llm/model/providerRegistry.ts`
2. Add or update test files to cover the fix.
   - Example: `packages/core/src/llm/model/providerRegistry.test.ts`
3. Add a `.changeset/*.md` entry describing the fix.

---

### Regenerate Provider Registry and Docs

**Trigger:** When providers are added/removed or their metadata changes.  
**Command:** `/regenerate-providers`

1. Regenerate `packages/core/src/llm/model/provider-registry.json`.
2. Regenerate `packages/core/src/llm/model/provider-types.generated.d.ts`.
3. Update documentation in `docs/src/content/en/models/**/*.mdx`.

---

### Add Changeset for Release Notes

**Trigger:** When a PR introduces a fix or feature that should be included in release notes.  
**Command:** `/changeset`

1. Create a `.changeset/*.md` file summarizing the change.
2. Commit it alongside code or documentation changes.

---

## Testing Patterns

- **Test Framework:** [vitest](https://vitest.dev/)
- **Test File Pattern:** Test files are named with the `.test.ts` suffix and placed alongside or near the code they test.
  - Example: `myFeature.test.ts`
- **Test Example:**
  ```typescript
  import { describe, it, expect } from 'vitest';
  import myFeature from './myFeature';

  describe('myFeature', () => {
    it('should return expected result', () => {
      expect(myFeature()).toBe('expected');
    });
  });
  ```

## Commands

| Command                | Purpose                                                                 |
|------------------------|-------------------------------------------------------------------------|
| /version-bump          | Bump package versions and update changelogs for a new (pre)release      |
| /feature               | Add a new feature with docs, tests, and a changeset entry               |
| /fix                   | Fix a bug, update/add tests, and add a changeset entry                  |
| /regenerate-providers  | Regenerate provider registry/types and update related documentation      |
| /changeset             | Add a changeset entry for release notes                                 |
```