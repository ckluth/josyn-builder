# PoC inventory — intermediate artifacts

**This is scaffolding, not a decision-trail artifact.** Nothing in this folder is
an idea, ADR, or plan, and none of it carries decision-trail status semantics. It
is a working notebook that supports the inventory task in
[plan 0001](../../plans/0001-repo-landscape-follow-ups.md), checkbox 1.

**Purpose (decision-driven, not catalogue-for-its-own-sake).** The inventory's only
job is to **supply the specific facts the four deferred ADRs in plan 0001 need**
(naming convention, dependency graph, versioning, overview/manifest). It is an
*input to decisions*, not an end in itself. We gather what the *next* decision
needs and stop — we do **not** aim for a complete neutral classification of every
repo against the ADR 0002 taxonomy. (Classification is just one fact some of those
ADRs happen to want.)

When the inventory has served its purpose — i.e. the deferred ADRs it grounds are
written — this folder can be discarded along with the rest of `josyn-builder`. It
exists only so the multi-pass gathering of facts has somewhere durable to live
without polluting the method.

## Why intermediate artifacts

decision-trail has no notion of temporary or working artifacts. The inventory is
exactly that: a long-running, costly fact-gathering exercise whose output is an
*input* to decisions, not a decision itself. Rather than stretch the method to
cover it, we keep these notes clearly *outside* the three artifact families.

## Multi-pass model (decision-driven, detail on demand)

A deep scan of every PoC repo at once would be slow and expensive — and pointless
if no pending decision needs the detail. So each pass is steered by the *next*
deferred ADR: gather exactly what that decision asks, then stop.

- **Pass 1 — a cheap map (by-product).** One row per repo in
  [`00-repo-index.md`](00-repo-index.md): name, one-line purpose, a *provisional*
  role guess, and which decision it's relevant to. Sourced from READMEs and
  existing platform docs — minimal code reading. This is orientation, not the
  deliverable.
- **Pass 2+ — gather for the next decision.** Before each deferred ADR, gather only
  the facts that ADR needs (e.g. for the naming-convention ADR: current repo
  names, the existing naming docs, and the inconsistencies a new scheme must
  resolve). Per-repo detail lands in `repos/<name>.md` only when a decision pulls
  for it. Most repos never get a file.

## Conventions

- **Provisional means provisional.** Role guesses in the index are first-pass and
  flagged; the actual ADR 0002 classification is real work done per repo, later.
- **Scope.** Current scope is the `josyn-*` repo family (the clear platform
  repos). Other `C:\DevGit` siblings are out of scope unless promoted in.
- **Source of truth stays upstream.** These notes *summarise* the PoC repos; they
  do not replace them. When in doubt, the repo itself wins.

## Files

| File | Pass | Contents |
|------|------|----------|
| [`00-repo-index.md`](00-repo-index.md) | 1 | Coarse one-row-per-repo index of the `josyn-*` family |
| `repos/<name>.md` | 2+ | Deep dive of a single repo, created on demand |
