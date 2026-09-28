# Beacon Studio product brief

**Status:** Proposed product  
**Source:** Owner-provided Beacon Studio Codex handoff dated September 27, 2026

## Vision

Beacon Studio is the primary browser-based AI workspace and autonomous development platform. Local models run in the background through LM Studio; a separately configured cloud supervisor plans work, reviews substantive results, redirects workers, and handles escalations. Agent Zero provides the initial agent runtime and stock UI during evaluation.

## Beacon Relay disposition

Beacon Relay was proposed as the durable communications and coordination layer for dispatching work and returning worker events. The handoff explicitly says Relay functionality may be integrated within Studio. This project therefore treats Relay as an **integrated Beacon Studio capability**, not a standalone product boundary.

Its proposed responsibilities include:

- Persisting tasks, events, and state transitions so work survives process or connection interruptions.
- Dispatching bounded assignments to local workers and accepting structured completion reports.
- Triggering cloud review on meaningful events, such as assignment, completion, blocker, or escalation, rather than maintaining a continuously running cloud session.
- Supporting retries, checkpoints, idempotency, cancellation, approval requests, and recovery.
- Later supporting text notifications and two-way approvals tied to durable, authenticated requests.

The suggested lifecycle states are CREATED, PLANNED, QUEUED, RUNNING, BLOCKED, AWAITING_REVIEW, REVISION_REQUIRED, AWAITING_APPROVAL, COMPLETED, FAILED, and CANCELLED. These are proposals from the handoff, not implemented or approved schema.

## Product principles

- Keep authoritative project, conversation, task, and event history in Beacon-owned storage.
- Make projects first-class records connected to chats, workspaces, repositories, knowledge, tasks, approvals, and evidence.
- Keep local execution scoped to authorized workspaces; prefer branches and isolated worktrees.
- Never treat elapsed time or a worker's own completion claim as proof of progress or correctness.
- Keep cloud conversation and project inspection available when local inference is offline.
- Start with a disposable repository and expand access incrementally.
- Build the unified responsive Studio interface after the autonomous lifecycle is proven.

## Conceptual architecture

```text
Beacon Studio browser UI
        |
Beacon backend: projects, conversations, permissions, persistent state
        |
        +-- Cloud supervisor (separate API instance)
        |
        +-- Integrated Relay capability: durable queue and event handoff
                  |
                  +-- Agent Zero worker / optional future execution backend
                              |
                         LM Studio local model
                              |
                   authorized tools, Git, GitHub
```

This diagram records the proposed product concept. It is not a deployment specification.

## Deferred product areas

The handoff proposes a future Studio UI for project navigation, chats, tasks, worker status, tool activity, files, diffs, tests, approvals, model selection, and API cost. It also proposes later SMS approvals, remote-access hardening, dedicated hosting, backups, monitoring, and recovery drills. These remain future work pending the stated phase gates.

## Names and boundaries

- Beacon Studio: proposed workspace and autonomous development platform.
- Beacon Relay: communications/coordination functions to be integrated into Studio.
- Beacon Assistant (BAI) and Beacon Remote: separate existing products.
- Beacon Forge: reserved for a possible future 3D project.
- Beacon Command: possible later use.
