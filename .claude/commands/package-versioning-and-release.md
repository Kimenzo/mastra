---
name: package-versioning-and-release
description: Workflow command scaffold for package-versioning-and-release in mastra.
allowed_tools: ["Bash", "Read", "Write", "Grep", "Glob"]
---

# /package-versioning-and-release

Use this workflow when working on **package-versioning-and-release** in `mastra`.

## Goal

Bumps versions across multiple packages, updates changelogs, and manages prerelease mode for coordinated releases.

## Common Files

- `.changeset/pre.json`
- `**/package.json`
- `**/CHANGELOG.md`
- `.changeset/*.md`

## Suggested Sequence

1. Understand the current state and failure mode before editing.
2. Make the smallest coherent change that satisfies the workflow goal.
3. Run the most relevant verification for touched files.
4. Summarize what changed and what still needs review.

## Typical Commit Signals

- Update .changeset/pre.json to enter or exit prerelease mode
- Update package.json and CHANGELOG.md files for affected packages
- Optionally add or update .changeset/*.md files describing changes

## Notes

- Treat this as a scaffold, not a hard-coded script.
- Update the command if the workflow evolves materially.