# 4. PoC repos are read-only; rebuild fresh; archive-before-reuse on name conflict

- Status: accepted
- Date: 2026-06-30

## Context

The migration consolidates an existing multi-repo PoC (~16 `josyn-*` repos) into a
fresh re-start (see `README.md`, two-level rule). As soon as we begin producing
target repos, two risks become concrete:

1. **Damaging a source.** The existing PoC repos are the only record of "much gold
   and also a lot of poor stuff." Editing one in place, or overwriting it while
   creating its replacement, is an **irreversible** loss of provenance.
2. **Name collisions.** Most target repos will reuse PoC names (e.g. a rebuilt
   `josyn-backend`, or the three `josyn-foundation-*` repos that arise from
   splitting `josyn-foundation`). The target landscape is expected to live in the
   same sibling set (`C:\DevGit\...`) as the PoC, so the fresh repo and the old one
   want the same name in the same place.

This ADR fixes the standing safety rule that governs *how* the migration touches
the existing repos, independent of any particular target decision.

## Decision Drivers

- **Reversibility first.** The one mistake we must make structurally impossible is
  destroying or mutating a source we can't get back.
- **Provenance.** Every original must stay recoverable and readable for later
  re-extraction and for review by future collaborators.
- **A clean slate per rebuild.** Each rebuilt repo should occupy a fresh,
  unambiguous slot — never a half-overwritten old one.

## Considered Options

- **Edit/upgrade PoC repos in place.** Rejected: entangles source and target,
  destroys provenance, and violates the two-level rule.
- **On name conflict, overwrite or delete the old repo.** Rejected: irreversible;
  the costliest possible mistake per the drivers above.
- **On name conflict, move the old repo into an archive first, then create the
  fresh one.** Chosen: reversible, preserves provenance, frees a clean slot.

## Decision

A migration-wide, standing rule:

1. **PoC repos are strictly read-only sources.** The migration only ever *reads*
   from an existing repo — to extract, copy, or re-implement. **No existing PoC
   repo is edited in place, ever.** They are source material, not work surfaces.

2. **Everything is rebuilt fresh, step by step.** Target repos are produced new and
   incrementally. Nothing is carried across without discussion → an accepted ADR →
   documentation. (This operationalizes the two-level rule and the README's
   "nothing shall be just transferred" principle.)

3. **Archive-before-reuse on name conflict.** When a target repo needs a name
   already held by an existing PoC sibling, the existing repo is **first moved —
   with its `.git` history intact — out of the active sibling set into a dedicated
   archive location**, freeing the name. Only *then* is the fresh target created in
   the freed slot. The original is never overwritten and remains available
   read-only.
   - **Archive location** is a dedicated place outside the active sibling set; its
     exact path is settled on first use rather than fixed here.
   - The move is a relocation, not a copy or delete — the original repo (and its
     history) survives unchanged, just elsewhere.

## Consequences

- The irreversible failure modes (editing or clobbering a source) are made
  structurally impossible: a source can only be read, or relocated wholesale.
- Every original stays recoverable for re-extraction and for collaborator review;
  provenance is preserved by default.
- Each rebuilt repo lands in a clean, unambiguous slot.
- A small, explicit archival step is required at each name collision; the archive
  accumulates the superseded PoC repos as the migration proceeds.
- **Deferred option (not decided here):** archiving *only on conflict* is the rule.
  Whether to also archive a PoC repo once it is fully processed (as a
  progress-tracking signal, independent of any name clash) is left open for a
  later decision if it proves useful.
- This rule is referenced by, but independent of, the naming-convention and
  taxonomy work in [plan 0001](../plans/0001-repo-landscape-follow-ups.md): name
  conflicts are *produced* by those decisions, and this ADR governs how they are
  safely resolved.
