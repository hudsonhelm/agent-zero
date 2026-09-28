# Stock Agent Zero evaluation plan

**Status:** Preparation only; no deployment or benchmark has been run.  
**Source:** Owner-provided handoff dated September 27, 2026.

## Objective

Determine whether unmodified Agent Zero paired with a 27B-class local model can complete real software-development work using tools. Manual intervention and manual ChatGPT review are permitted for this first test. Avoid paid cloud fallbacks so the benchmark measures local capability.

## Environment recorded in the handoff

- Persephone (Dell Precision 3591): LM Studio inference server; 32 GB RAM and RTX 500 Ada with 4 GB VRAM. Do not plan around an additional 16 GB module until it is installed.
- Plex server: existing Docker host on the same home LAN; temporary Agent Zero deployment and disposable execution repository. Preserve existing containers and performance.
- Hermes: remote administration/browser host; no inference or Docker role required.
- WireGuard: private remote access. Keep the Agent Zero UI on trusted private access during the test and model traffic on the LAN.
- GitHub: disposable repository or branch only if needed; no production repository.

These are handoff-provided facts, not independently checked in this workspace.

## Proposed starting configuration

The handoff proposes Qwen3.5-27B GGUF Q4_K_M, 16,384 context, one loaded model, and as much GPU offload as remains stable. Availability, current model packaging, LM Studio compatibility, Agent Zero image/version, provider settings, authentication, ports, persistent-data paths, and exact commands still require verification against current upstream sources before deployment.

Do not assume `host.docker.internal` reaches Persephone from a container on Plex. Configure the actual Persephone LAN endpoint and verify model-list and test-completion requests from inside the Agent Zero container. Restrict access to trusted LAN hosts, use authentication where supported, and do not expose LM Studio to the internet.

## Benchmark assignments

1. **Tools:** inspect directories, create files, execute shell/Python, and independently verify output.
2. **Repository comprehension:** explain architecture, dependencies, entry points, and tests for a modest repository; check claims against files.
3. **Feature development:** deliver a bounded multi-file feature against explicit acceptance criteria.
4. **Debugging:** reproduce a failing test, diagnose, fix, and rerun it.
5. **Git:** create a feature branch, inspect the diff, test, and commit; do not push the default branch.
6. **Extended task:** complete repeated implementation/test/fix cycles while preserving objective and progress.
7. **Delegation:** test superior/subordinate assignment and result reporting with local inference if supported by the pinned version.

Acceptance criteria for each assignment must be written before execution in its benchmark record. Verify artifacts and outputs independently; never accept an agent's “done” statement as verification.

## Evidence to capture

For each run record the prompt, Agent Zero version and image digest, configuration, model build, elapsed time, token speed where available, RAM/VRAM use, tool-call errors, human interventions, logs, resulting diff/commit, repeated failures, and whether acceptance criteria were met. Set safe iteration limits and detect no-progress loops.

Use [the run record template](../../evaluation/templates/run-record.md). Keep secrets out of this repository and its commits.

## Safety and deployment constraints

- Use an isolated disposable repository and scoped workspace permissions.
- Do not disturb Plex services or existing containers.
- Use persistent storage suitable for later migration and back it up.
- Enable built-in login; restrict UI access to LAN/WireGuard.
- Do not grant blanket Windows-host, Exchange, Active Directory, production-repository, or credential access.
- Never permit default-branch pushes, force-pushes, destructive filesystem actions, production changes, or merges without explicitly configured authority and approval.
- Pin the working Agent Zero version/image digest after validation.

## Phase-one gate

Deliver reproducible benchmark evidence and a candid assessment of what stock Agent Zero plus local inference can and cannot do. Only then decide whether to fork Agent Zero or integrate OpenCode as an execution backend.

## Scope distinction

This evaluation plan prepares the first experiment. It does not implement Beacon Studio, an integrated Relay controller, cloud supervision, production deployment, or the broader product roadmap.
