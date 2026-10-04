# Case Study — OpenCode Connect

## Problem

After building around Codex, I wanted a second AI execution substrate without
making the operator depend on one provider or forcing a different runtime into the
same internal model.

## My role

I defined the compatibility boundary, decided which concepts should remain native
to OpenCode, directed AI-assisted implementation, compared behavior against the
Codex-based system, and refined the operator workflow around the differences.

## Core design choices

- Preserve OpenCode's native sessions, message identities, agents, permissions,
  worktrees, and terminal primitives.
- Keep the shared abstraction at the **operator workflow** level rather than
  manufacturing fake API parity between runtimes.
- Project only bounded, safe operational information through the connector.
- Keep each substrate independently deployable and independently authoritative for
  its own worker lifecycle.
- Use the second implementation as a way to test whether the higher-level operating
  model was truly portable.

## What this demonstrates

Abstraction judgment, comparative system design, avoiding over-generalization, and
the ability to adapt a workflow to different native capabilities instead of forcing
everything through one shape.

## Verified outcome

The same primary operator can use OpenCode as an independent execution substrate
while retaining OpenCode's native session, agent, worktree, permission, and
terminal semantics. I validated the connector with its automated contract and
runtime tests and by operating real persisted sessions from ChatGPT. Where a
platform capability differs—for example event-driven continuation—I record that
as a separate limitation instead of masking it behind a compatibility layer.
