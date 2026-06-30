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
- [ ] Naming-convention ADR — promote
      [idea 0005](../ideas/0005-repo-naming-convention.md); cheapest, unblocks
      creating any target repo.
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
