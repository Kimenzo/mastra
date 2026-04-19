```markdown
# mastra Development Patterns

> Auto-generated skill from repository analysis

## Overview

This skill teaches the core development patterns, coding conventions, and common workflows used in the `mastra` TypeScript monorepo. It covers how to structure code, write tests, manage releases, and contribute features or fixes. The guide is based on observed repository practices and is intended for both new and experienced contributors.

## Coding Conventions

- **Language:** TypeScript (no framework detected)
- **File Naming:** Use `camelCase` for file names.
  - Example: `modelProvider.ts`, `apiClient.test.ts`
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
  - Example: `feat: add support for new provider registry`

## Workflows

### Package Version Bump and Changelog Update
**Trigger:** When preparing for a new release, prerelease, or after merging significant changes.  
**Command:** `/version-bump`

1. Update `.changeset/pre.json` to enter/exit prerelease mode or mark a new version.
2. Update `package.json` and `CHANGELOG.md` files for all affected packages.
3. Optionally, add or update `.changeset/*.md` files to describe changes.
4. Commit all version and changelog changes together.

**Example Commit:**
```
chore: bump package versions and update changelogs
```

### Regenerate Provider Registry and Docs
**Trigger:** When a new model provider is added or provider metadata changes.  
**Command:** `/regenerate-providers`

1. Regenerate `packages/core/src/llm/model/provider-registry.json` and `provider-types.generated.d.ts`.
2. Update documentation files under `docs/src/content/en/models/` and related sidebars.
3. Commit all generated and updated files together.

**Example Commit:**
```
chore: regenerate provider registry and update docs
```

### Add or Update Changeset for Feature or Fix
**Trigger:** When implementing a new feature, bug fix, or other significant change that should be tracked in release notes.  
**Command:** `/add-changeset`

1. Create or update a `.changeset/*.md` file describing the change.
2. Modify relevant source code files (implementation, tests, docs).
3. Commit the `.changeset` file and code changes together.

**Example Changeset File:**
```markdown
---
"@mastra/core": minor
---

Add support for new logging provider.
```

### Feature Development with Tests and Docs
**Trigger:** When adding a significant new capability (e.g., API, storage adapter, logging feature).  
**Command:** `/new-feature`

1. Add or modify implementation files (e.g., `src/feature.ts`).
2. Add or update corresponding test files (e.g., `src/feature.test.ts`).
3. Update or add documentation (e.g., `docs/src/content/en/reference/feature.mdx`).
4. Optionally, add a `.changeset/*.md` entry.

**Example File Structure:**
```
packages/my-feature/
  src/
    myFeature.ts
    myFeature.test.ts
docs/src/content/en/reference/myFeature.mdx
.changeset/feature-xyz.md
```

### Fix with Test Update
**Trigger:** When a bug is discovered and needs to be resolved with regression coverage.  
**Command:** `/fix-bug`

1. Modify source code to fix the bug.
2. Update or add relevant test files to cover the fixed case.
3. Optionally, add a `.changeset/*.md` entry.
4. Commit fix and test changes together.

**Example Commit:**
```
fix: correct provider metadata parsing and add regression test
```

## Testing Patterns

- **Framework:** [Vitest](https://vitest.dev/)
- **Test File Pattern:** Files end with `.test.ts` and are placed alongside implementation files.
  - Example: `src/myFeature.ts` and `src/myFeature.test.ts`
- **Typical Test Example:**
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

| Command               | Purpose                                                      |
|-----------------------|--------------------------------------------------------------|
| /version-bump         | Bump package versions and update changelogs for a release    |
| /regenerate-providers | Regenerate provider registry files and update documentation  |
| /add-changeset        | Add or update a changeset for a feature or fix              |
| /new-feature          | Start a new feature with tests and documentation            |
| /fix-bug              | Fix a bug and update/add tests                              |
```
