# 1. Repo-landscape follow-ups

- Status: active
- Date: 2026-06-30
- Implements: [ADR 0002](../decisions/0002-repo-landscape-poly-repo-principle.md)

## Purpose

ADR 0002 accepted the poly-repo principle and repo taxonomy, and explicitly
deferred four mechanics to follow-up ADRs. This plan is the single place that
tracks those deferred decisions so none is lost on the journey. Each deferred
decision also has a stub idea (parked, durable); this plan tracks ordering and
progress toward turning each into its own accepted ADR.

## Tasks

Suggested order (each grounded by a prior inventory of the existing PoC repos):

- [ ] Inventory & classify the ~16 existing PoC repos against the ADR 0002
      taxonomy (analysis that grounds the decisions below).
- [x] Naming-convention ADR — promote
      [idea 0005](../ideas/0005-repo-naming-convention.md); cheapest, unblocks
      creating any target repo. → [ADR 0005](../decisions/0005-repo-naming-convention.md) (accepted)
- [ ] Dependency-graph ADR — promote
      [idea 0003](../ideas/0003-dependency-graph-management.md).
- [ ] Versioning & release-strategy ADR — promote
      [idea 0002](../ideas/0002-versioning-and-release-strategy.md); decide
      together with the dependency graph, using real data from the inventory.
- [ ] Overview / platform-manifest ADR — promote
      [idea 0004](../ideas/0004-overview-platform-manifest.md); follows once the
      repo set and naming are settled.

## Done when

All four deferred decisions have been carried into accepted ADRs (or explicitly
dropped), at which point this plan moves to `done`.

## Continuation brief (as of 2026-06-30)

Where we are and how to resume:

- **Inventory is decision-driven, not catalogue-for-its-own-sake.** It gathers only
  what the *next* deferred ADR needs, then stops. Working notes live in
  `docs/intermediate-artifacts/PoC-inventory/` (intermediate artifacts, *not*
  decision-trail artifacts): `00-repo-index.md` (coarse map),
  `repos/josyn-platform.md` (deep dive), `naming-convention-findings.md` (the
  grounded evidence behind ADR 0005).
- **Done so far.** Naming-convention ADR is **accepted** ([ADR 0005]). Two
  migration-safety / scoping decisions also landed:
  [ADR 0004](../decisions/0004-poc-repos-read-only-archive-before-reuse.md) (PoC
  repos read-only; archive-before-reuse).
- **Validated only on clean contract/library repos** (`job-host`, `foundation`,
  `commons`, `jap`). Two repos are **parked** as unreliable evidence:
  [idea 0007](../ideas/0007-untangle-josyn-backend.md) (`josyn-backend` is a
  melting pot — needs its own untangling sub-project) and
  [idea 0008](../ideas/0008-quality-review-latecomer-repos.md) (`josyn-jrp`,
  `josyn-surface` are unreviewed latecomers).
- **Concrete naming results carried forward:** `josyn-foundation` and
  `josyn-commons` split one-repo-per-package (no escape hatch needed; family
  cohesion via name prefix); `josyn-jap` → `josyn-jap-contract`.
- **Next likely step:** the dependency-graph ADR
  ([idea 0003](../ideas/0003-dependency-graph-management.md)) — its edges are
  artifact-to-artifact, and the artifact-level data started in the inventory feeds
  it. Versioning ([idea 0002](../ideas/0002-versioning-and-release-strategy.md))
  pairs with it; the manifest ADR
  ([idea 0004](../ideas/0004-overview-platform-manifest.md)) follows.
- **Open meta-question** (raised in the platform deep dive): how much of the PoC's
  45-ADR history is carried forward vs re-decided — may warrant its own ADR.

[ADR 0005]: ../decisions/0005-repo-naming-convention.md
