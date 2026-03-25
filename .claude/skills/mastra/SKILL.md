```markdown
# mastra Development Patterns

> Auto-generated skill from repository analysis

## Overview

This skill teaches you the core development patterns, coding conventions, and collaborative workflows used in the `mastra` TypeScript codebase. You'll learn how to structure code, write and organize tests, follow commit conventions, and execute common repository workflows such as releasing, adding storage domains, and developing features with proper documentation and testing.

## Coding Conventions

- **File Naming:** Use camelCase for file names.
  - Example: `providerRegistry.ts`, `featureToggle.ts`
- **Import Style:** Use relative imports.
  - Example:
    ```typescript
    import myUtil from './utils/myUtil';
    ```
- **Export Style:** Use default exports.
  - Example:
    ```typescript
    export default function myFunction() { ... }
    ```
- **Commit Messages:** Follow [Conventional Commits](https://www.conventionalcommits.org/) with prefixes:
  - `chore:`, `fix:`, `feat:`
  - Example: `feat: add support for new storage domain`
- **Documentation:** Update or add documentation in `README.md` or under `docs/src/content/en/`.

## Workflows

### Version Bump and Changelog Release
**Trigger:** When preparing a new release, prerelease, or after merging significant changes.  
**Command:** `/release-bump`

1. Update `.changeset/pre.json` to reflect new version or prerelease state.
2. Update `package.json` and `CHANGELOG.md` in all relevant packages.
3. Commit all version and changelog changes together.

**Files involved:**
- `.changeset/pre.json`
- `**/CHANGELOG.md`
- `**/package.json`

---

### Regenerate Provider Registry and Model Docs
**Trigger:** When a new model provider is added or provider metadata is updated.  
**Command:** `/regenerate-providers`

1. Regenerate `packages/core/src/llm/model/provider-registry.json`.
2. Regenerate `packages/core/src/llm/model/provider-types.generated.d.ts`.
3. Update `docs/src/content/en/models/index.mdx` and provider docs in `docs/src/content/en/models/providers/*.mdx`.
4. Commit regenerated files.

**Files involved:**
- `packages/core/src/llm/model/provider-registry.json`
- `packages/core/src/llm/model/provider-types.generated.d.ts`
- `docs/src/content/en/models/index.mdx`
- `docs/src/content/en/models/providers/*.mdx`

---

### Add or Update Storage Domain
**Trigger:** When supporting a new data domain in a backend store.  
**Command:** `/add-storage-domain`

1. Implement new domain logic in `stores/<backend>/src/storage/domains/<domain>/index.ts` and related files.
2. Update `stores/<backend>/src/storage/index.ts` to register the new domain.
3. Add or update tests for the new domain.
4. Add or update `.changeset/*.md` for release notes.

**Files involved:**
- `stores/*/src/storage/domains/*/index.ts`
- `stores/*/src/storage/index.ts`
- `stores/*/src/storage/domains/*/*.ts`
- `stores/*/src/__tests__/*.test.ts`
- `.changeset/*.md`

---

### Feature Development with Tests and Docs
**Trigger:** When developing a new feature or major enhancement.  
**Command:** `/feature`

1. Implement feature in relevant source files.
2. Add or update unit/integration tests.
3. Update or add documentation (`README.md`, `docs/src/content/en/*`).
4. Add `.changeset/*.md` describing the change.

**Files involved:**
- `*/src/**/*.ts`
- `*/src/**/*.test.ts`
- `*/README.md`
- `docs/src/content/en/**/*.mdx`
- `.changeset/*.md`

---

### Bugfix with Test and Changeset
**Trigger:** When a bug is discovered and fixed.  
**Command:** `/bugfix`

1. Fix bug in relevant source file(s).
2. Add or update test(s) to cover the bug scenario.
3. Add or update `.changeset/*.md` for release notes.

**Files involved:**
- `*/src/**/*.ts`
- `*/src/**/*.test.ts`
- `.changeset/*.md`

---

### UI Component or Dashboard Feature
**Trigger:** When introducing a new UI feature or dashboard (e.g., metrics dashboard, entity lists).  
**Command:** `/ui-feature`

1. Implement or update React components in `packages/playground-ui/src/domains/*/components/`.
2. Add or update supporting hooks/utilities.
3. Wire up new feature in `packages/playground/src/pages/`.
4. Add `.changeset/*.md` for release notes.

**Files involved:**
- `packages/playground-ui/src/domains/*/components/**/*.tsx`
- `packages/playground-ui/src/domains/*/hooks/**/*.ts`
- `packages/playground/src/pages/**/*.tsx`
- `.changeset/*.md`

---

### Experimental Feature Toggle
**Trigger:** When rolling out a new experimental feature for testing.  
**Command:** `/experimental-feature`

1. Implement feature in codebase (UI and/or backend).
2. Add feature flag logic (e.g., check `process.env` or config).
3. Wire up feature in relevant pages/components.
4. Add `.changeset/*.md` for release notes.

**Files involved:**
- `packages/playground-ui/src/domains/**/*.tsx`
- `packages/playground/src/pages/**/*.tsx`
- `packages/cli/src/commands/**/*.ts`
- `.changeset/*.md`

---

## Testing Patterns

- **Testing Framework:** [Vitest](https://vitest.dev/)
- **Test File Pattern:** Files end with `.test.ts`.
  - Example: `featureToggle.test.ts`
- **Test Placement:** Place tests alongside source files or in `__tests__` directories.
- **Test Example:**
  ```typescript
  import { describe, it, expect } from 'vitest';
  import myFunction from './myFunction';

  describe('myFunction', () => {
    it('should return true when input is valid', () => {
      expect(myFunction('valid')).toBe(true);
    });
  });
  ```

## Commands

| Command                | Purpose                                                      |
|------------------------|--------------------------------------------------------------|
| /release-bump          | Bump versions and update changelogs for a release cycle      |
| /regenerate-providers  | Regenerate provider registry and model documentation         |
| /add-storage-domain    | Add or update a storage domain in a backend store            |
| /feature               | Start a new feature with tests and documentation             |
| /bugfix                | Fix a bug, add tests, and update release notes               |
| /ui-feature            | Add or update a UI component or dashboard feature            |
| /experimental-feature  | Introduce or update an experimental feature with a flag      |
```