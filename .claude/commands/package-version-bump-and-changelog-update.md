---
name: package-version-bump-and-changelog-update
description: Workflow command scaffold for package-version-bump-and-changelog-update in mastra.
allowed_tools: ["Bash", "Read", "Write", "Grep", "Glob"]
---

# /package-version-bump-and-changelog-update

Use this workflow when working on **package-version-bump-and-changelog-update** in `mastra`.

## Goal

Bump package versions and update changelogs across multiple packages, usually as part of a release or prerelease process.

## Common Files

- `.changeset/pre.json`
- `**/package.json`
- `**/CHANGELOG.md`

## Suggested Sequence

1. Understand the current state and failure mode before editing.
2. Make the smallest coherent change that satisfies the workflow goal.
3. Run the most relevant verification for touched files.
4. Summarize what changed and what still needs review.

## Typical Commit Signals

- Update .changeset/pre.json to enter/exit prerelease mode or mark a new version.
- Update package.json and CHANGELOG.md files for multiple packages (client, server, integrations, observability, etc).
- Commit all updated files together.

## Notes

- Treat this as a scaffold, not a hard-coded script.
- Update the command if the workflow evolves materially.