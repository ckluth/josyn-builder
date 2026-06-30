# 2. Repo-landscape: poly-repo principle and repo taxonomy

- Status: accepted
- Date: 2026-06-30
- Promoted from: [idea 0001](../ideas/0001-repo-landscape-structuring.md)
- Amended by: [ADR 0003](0003-repo-continuity-defer-pilot-seat.md)

## Context

We are migrating an existing PoC that already spans about 16 repositories into a
fresh platform. Before producing any target repos, we need a deliberate decision
about how the repository landscape is structured — its organizing principle and
the kinds of repos that may exist.

Per the two-level rule (see `README.md`), this repo (`josyn-builder`) is the
temporary workshop where this reasoning happens; the deliverables are the clean
target repos themselves.

This ADR is intentionally **narrow**: it commits only to the organizing
*principle* and the repo *taxonomy*. The mechanics it implies — versioning,
dependency-graph management, an overview mechanism, and naming conventions — are
deferred to named follow-up ADRs (see Consequences), so each can be reviewed on
its own.

## Decision Drivers

- Strict separation of concerns: one artifact / one concern should not be
  entangled with another.
- Collaboration- and review-readiness: the structure must withstand the critical
  view of future colleagues.
- Two named risks to keep in check rather than ignore: loss of overview across
  many repos, and a complicated dependency graph / versioning strategy.

We frame the choice as **poly-repo as a default decided by criteria**, not as an
absolute claim that poly-repo is universally superior — the criteria above are
what the default must serve.

## Considered Options

- **Pure poly-repo** — one repo per shippable artifact, strictly, no exceptions.
- **Poly-repo with grouping** — related artifacts that always version together may
  share a repo.
- **Hybrid** — poly-repo for shippables plus a small monorepo for tightly-coupled
  internal libraries.
- **Monorepo (the main counter-option)** — one (or few) repos holding everything.
  Its real strengths are acknowledged: atomic cross-cutting changes (one commit /
  one PR across many artifacts), a single source of truth, no cross-repo version
  dance, and simpler refactors across boundaries. We do **not** choose it because
  it weakens strict separation of concerns and the per-artifact ownership and
  review boundaries we value for collaboration-readiness; it concentrates rather
  than separates. The cost we accept in return — coordination across many repos —
  is exactly what the deferred follow-up ADRs (versioning, dependency graph,
  overview) must make manageable. If those mechanics prove unworkable, this
  counter-option is the natural place to reconsider.

## Decision

We adopt a **poly-repo** landscape, with the following commitments:

1. **Poly-repo principle.** One repository per shippable artifact (a NuGet package
   or an executable), and one concern per repository. No multi-purpose repos.
   - **Escape hatch:** exceptions to strict one-repo-per-artifact (grouping of
     artifacts that always version together, or a monorepo for tightly-coupled
     internal libraries) are permitted **only** when justified by a future ADR.
     The principle is the default, not dogma.

2. **Repo taxonomy.** Every repository belongs to exactly one of a closed set of
   roles. The **classification rule**: a repo is an `artifact` if its *primary
   output* is a versioned shippable consumed by others; it is a `concern` if it
   *owns a shared capability* consumed by artifacts rather than shipping a product
   of its own. When a repo could read as both (e.g. a tooling repo that also ships
   an executable), classify it by its primary output — the executable makes it an
   `artifact`; if it primarily provides shared capability, it is a `concern`.
   - `artifact` — produces one shippable artifact (one NuGet or one executable).
   - `concern` — owns one separable cross-artifact concern (e.g. database,
     tooling, infrastructure).
   - `pilot-seat` — exactly one repo, the single agentic control / orchestration
     seat for the platform.
   - `platform-docs` — exactly one repo, holding all cross-cutting and
     architecturally platform-relevant documentation.

3. **This repo is temporary.** `josyn-builder` is the migration workshop and
   dissolves once its work is done. It does **not** become the pilot-seat; the
   `pilot-seat` repo is a new, separate repo created later.

## Consequences

- The landscape will contain many repositories (the PoC already has ~16). The two
  named risks are accepted here and their *resolution* is deferred to follow-up
  ADRs that this decision calls for:
  - **Versioning & release strategy** across independently-versioned repos.
  - **Dependency-graph management** between repos.
  - **Overview mechanism** — a regenerated *platform manifest* listing every repo,
    its role and version, so overview is derived rather than lost (conceptually
    the same move decision-trail uses for `docs/overview.md`).
  - **Repo naming convention** — a predictable scheme so many repos stay
    scannable.
- Until those ADRs exist, no repo may claim an exception to the poly-repo
  principle, and the four taxonomy roles are the only permitted repo kinds.
- Producing target repos can proceed against this taxonomy once accepted.
