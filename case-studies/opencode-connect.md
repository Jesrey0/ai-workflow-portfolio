# Case Study — OpenCode Connect

## Problem

After building around Codex, I wanted a second way to run coding work so the whole
workflow did not depend on one runtime.

## My role

I compared the experience against Codex Connect, questioned where the two systems
really needed to match, and pushed back when making them look alike started making
either one less natural to use.

ChatGPT and delegated agents handled the technical implementation. My role was to
keep the work tied to the practical goal: another useful execution option without
flattening both runtimes into the same generic interface.

## Where the design landed

These choices were worked out through comparison and repeated use:

- Preserve OpenCode's native sessions, message identities, agents, permissions,
  worktrees, and terminal primitives.
- Keep what is shared at the **operator workflow** level instead of forcing both
  runtimes to look the same.
- Expose only the operational information the connector actually needs.
- Keep each runtime independently deployable and responsible for its own worker
  lifecycle.
- Use the second implementation to test whether the overall workflow still made
  sense on a different runtime.

## Why it matters

This shows how I compare approaches in practice: if making two systems look alike
makes the workflow worse, I would rather keep the difference.

## Verified outcome

The same primary operator can use OpenCode as a separate execution path while
retaining OpenCode's native sessions, agents, worktrees, permissions, and terminal
behavior. I had ChatGPT run the connector's automated contract and
runtime tests, then I tested real persisted sessions from ChatGPT myself. Where a
platform capability differs—for example event-driven continuation—I keep it as a
real limitation instead of hiding it behind a compatibility layer.
