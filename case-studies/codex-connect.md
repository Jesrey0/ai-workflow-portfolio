# Case Study — Codex Connect

## Problem

I wanted ChatGPT to do more than answer questions about a machine. It needed a
durable way to inspect and operate the host, hand coding work to Codex, recover
interrupted or long-running work, and check the result without turning everything
into one autonomous agent.

## My role

I started from a practical problem: I wanted ChatGPT to operate my host without
forcing me to move constantly between chat, terminals, and separate coding-agent
interfaces.

I shaped the system by using it, questioning where it broke or was more complicated
than it needed to be, and repeatedly redirecting the work as new problems appeared.
ChatGPT worked out the technical steps and coordinated the implementation,
including most of the low-level Rust work. I judged the workflow from the operator
side and kept pushing it toward something I could reliably use day to day.

## Where the design landed

The technical design that came out of those iterations separates the work into
three responsibilities:

- **HostPlane** handles deterministic filesystem, process, Git, deployment, and
  runtime state.
- **WorkerPlane** handles delegated Codex threads, turns, reviews, and requests.
- **PlatformPlane** handles ChatGPT-native capabilities and
  continuation.
- The connector uses upstream Codex App Server primitives instead of duplicating
  that state inside the connector.
- Retain command and worker handles so interruption or transport loss does not
  automatically cause duplicate work.
- Separate source, tests, Git, deployment, live runtime, and external connection
  verification.

## Why it matters

This is the clearest example of how I work: repeated friction became a tool I now
use, and I kept refining it after the first version worked.

## Verified outcome

I use Codex Connect for real repository and host work. I tested saved commands,
delegated coding and read-only review, interruption recovery, concurrent work, and
terminal-event continuation from the operator side. I only accept a release after
the source and tests, host state, deployed runtime, and external connection have
each been checked separately instead of relying on an agent's completion message.
