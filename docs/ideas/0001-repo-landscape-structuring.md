# 1. Repo-landscape structuring

- Status: promoted
- Date: 2026-06-30
- Promoted to: [ADR 0002](../decisions/0002-repo-landscape-poly-repo-principle.md)

## The thought

Clarifying how the repository landscape is structured should be a first task.

The core idea: have **many, strictly separated repositories** — no multi-repos.
Every artifact and every concern lives in its own single repo.

- An artifact may be a NuGet package or an executable.
- Possibly further repos for separable concerns such as: database, tooling, …
- One single repo as the only **agentic pilot-seat**.
- One major **docs repo** for all cross-cutting and architecturally
  platform-relevant documentation.

## Why it might matter / open tensions

This will lead to *really many* repos (the current PoC already has about 16).

Foreseeable downsides to weigh:

- A possible **lack of overview** across so many repos.
- A potentially **complicated dependency graph** and **versioning strategy**.
