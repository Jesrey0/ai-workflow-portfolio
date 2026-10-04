# Case Study — Codex Connect

## Problem

I wanted ChatGPT to do more than answer questions about a machine. It needed a
durable way to inspect and operate the host, delegate bounded work to Codex, recover
lost or long-running state, and verify outcomes without turning everything into one
unstructured autonomous agent.

## My role

I developed the operating model and requirements, decided how authority should be
split, directed implementation and review through AI agents, and repeatedly tested
the live system. I did not manually write most of the low-level Rust code.

## Core design choices

- **HostPlane** owns deterministic filesystem, process, Git, deployment, and
  runtime state.
- **WorkerPlane** owns delegated Codex threads, turns, reviews, and requests.
- **PlatformPlane** remains responsible for ChatGPT-native capabilities and
  continuation.
- Prefer upstream Codex App Server primitives instead of inventing duplicate state
  machines in the connector.
- Retain command and worker handles so interruption or transport loss does not
  automatically cause duplicate work.
- Separate source, tests, Git, deployment, live runtime, and external connection
  verification.

## What this demonstrates

Agent orchestration, authority design, recovery-oriented workflows, testable
acceptance criteria, and iterative architecture refinement around a fast-moving AI
runtime.

## Verified outcome

I use Codex Connect as a live operating path for repository work and host
maintenance. I have exercised retained commands, delegated implementation and
read-only review, interruption recovery, concurrent workstreams, and terminal
event continuation. A release is accepted only after the relevant source/tests,
host state, deployed runtime, and external connection have each been checked at
their owning layer rather than relying on an agent's completion message.
