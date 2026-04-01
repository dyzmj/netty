---
name: test-stabilization-or-diagnostic-improvement
description: Workflow command scaffold for test-stabilization-or-diagnostic-improvement in netty.
allowed_tools: ["Bash", "Read", "Write", "Grep", "Glob"]
---

# /test-stabilization-or-diagnostic-improvement

Use this workflow when working on **test-stabilization-or-diagnostic-improvement** in `netty`.

## Goal

Improves the stability or diagnostic output of flaky or timing-sensitive tests, often by adding timeouts, barriers, stack trace capture, or other mechanisms to make failures more informative and tests less flaky.

## Common Files

- `*/src/test/java/**/*.java`

## Suggested Sequence

1. Understand the current state and failure mode before editing.
2. Make the smallest coherent change that satisfies the workflow goal.
3. Run the most relevant verification for touched files.
4. Summarize what changed and what still needs review.

## Typical Commit Signals

- Identify the problematic test method(s) in test files.
- Add synchronization primitives (e.g., barriers, latches) to coordinate threads.
- Increase or adjust timeouts.
- Capture and report stack traces or exceptions from worker threads.
- Sometimes add or adjust annotations (e.g., @Isolated) to control test isolation.

## Notes

- Treat this as a scaffold, not a hard-coded script.
- Update the command if the workflow evolves materially.