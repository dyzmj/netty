---
name: auto-port-fix-or-feature-to-4-1
description: Workflow command scaffold for auto-port-fix-or-feature-to-4-1 in netty.
allowed_tools: ["Bash", "Read", "Write", "Grep", "Glob"]
---

# /auto-port-fix-or-feature-to-4-1

Use this workflow when working on **auto-port-fix-or-feature-to-4-1** in `netty`.

## Goal

Automatically ports a fix or feature from another branch to the 4.1 branch, usually by cherry-picking a commit and updating relevant files (Java, C, or test files) in the appropriate module.

## Common Files

- `*/src/main/java/**/*.java`
- `*/src/main/c/**/*.c`
- `*/src/test/java/**/*.java`
- `.github/workflows/autoport-41.yml`

## Suggested Sequence

1. Understand the current state and failure mode before editing.
2. Make the smallest coherent change that satisfies the workflow goal.
3. Run the most relevant verification for touched files.
4. Summarize what changed and what still needs review.

## Typical Commit Signals

- Cherry-pick the relevant commit from the source branch.
- Apply changes to the same files in the 4.1 branch.
- Update or add corresponding test files if necessary.
- Commit with a message starting with 'Auto-port 4.1:' and referencing the original PR/commit.
- Co-author attribution if applicable.

## Notes

- Treat this as a scaffold, not a hard-coded script.
- Update the command if the workflow evolves materially.