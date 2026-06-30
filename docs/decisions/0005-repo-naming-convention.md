# 5. Repo naming convention: repo name mirrors the artifact's package namespace

- Status: accepted
- Date: 2026-06-30
- Promoted from: [idea 0005](../ideas/0005-repo-naming-convention.md)
- Implements context: deferred by [ADR 0002](0002-repo-landscape-poly-repo-principle.md),
  tracked in [plan 0001](../plans/0001-repo-landscape-follow-ups.md)

## Context

ADR 0002 adopted a poly-repo landscape (one repo per shippable artifact) and
explicitly deferred the **naming convention** to a follow-up ADR. Plan 0001 lists it
as the cheapest deferred decision — it unblocks creating any target repo.

With 16+ repos, names are the primary way the landscape stays scannable. This ADR
is grounded in a concrete inventory of the *trustworthy* PoC repos (see
`docs/intermediate-artifacts/PoC-inventory/naming-convention-findings.md`), not in
abstraction. Repos that are structurally unsound (`josyn-backend`, idea 0007) or
not yet quality-reviewed (`josyn-jrp`, `josyn-surface`, idea 0008) were excluded as
unreliable evidence.

Examining the clean repos showed the platform *already* almost follows one rule —
the repo name is the artifact's package namespace, kebab-cased — with `josyn-jap`
as the lone exception. This ADR ratifies that rule.

## Decision Drivers

- **Scannability** across many repos.
- **1:1 predictability.** Given a package namespace one should derive the repo name
  mechanically, and vice-versa — no lookup table.
- **Consistency with ADR 0002.** One repo = one artifact; the name should reflect
  that unit, not a grouping.
- **Family cohesion without an escape hatch.** Related artifacts must still *read*
  as a family after grouping repos are split into poly-repo form.

## Considered Options

- **Full package namespace, kebab-cased (chosen).** Repo name = the artifact's
  package namespace with `JOSYN→josyn`, dots→hyphens, PascalCase split on case,
  acronyms kept whole. Already obeyed by `josyn-job-host`, `josyn-foundation-*`
  (on-disk subfolders), `josyn-commons-*`. Mechanical and reversible.
- **Family-stem naming** (the `josyn-jap` style: drop the leaf segment `Contract`,
  add a generic `-shared` subfolder). Rejected: it is an ad-hoc second scheme, the
  `-shared` suffix carries no meaning, and it breaks the 1:1 mapping.
- **Collapse PascalCase segments** (`resultpattern`, `propertybag`). Rejected: less
  readable, and does not match the existing on-disk subfolder names.
- **Encode the taxonomy role in the name** (e.g. `josyn-concern-*` /
  `josyn-artifact-*`). Rejected here: role is better derived from the platform
  manifest (a separate deferred ADR) than baked into every repo name; mirroring the
  namespace keeps names stable even if a role is reclassified.

## Decision

1. **Repo name = the artifact's full package namespace, kebab-cased**, by these
   mechanical steps:
   - leading `JOSYN` → `josyn`;
   - each `.` (namespace separator) → `-`;
   - each PascalCase segment split on case boundaries
     (`JobHost` → `job-host`, `IdentityHelpers` → `identity-helpers`);
   - an all-caps acronym segment is lowercased as **one** token
     (`JIP` → `jip`, never `j-i-p`).

2. **One repo = one artifact = one package**, with the repo name 1:1 with that
   package's namespace (consistent with ADR 0002's poly-repo principle).

3. **Family identity is carried by the shared name prefix**, not by a shared repo.
   `josyn-foundation-*` and `josyn-commons-*` remain visibly a family after their
   grouping repos are split — so splitting them needs **no** ADR 0002 escape hatch.

4. **Single-artifact repos use the full namespace too** — no family-stem shortcut.
   Consequently `josyn-jap` (holding `JOSYN.Jap.Contract`) is renamed on rebuild to
   **`josyn-jap-contract`**, and the generic `-shared` subfolder is dropped.

This rule governs **target** repo names produced by the migration. Per ADR 0004,
existing PoC repos are read-only; a name is only realised when a fresh repo is
built (archiving the old holder of the name first if it collides).

## Consequences

- **Grouping repos split predictably.** `josyn-foundation` →
  `josyn-foundation-result-pattern`, `-property-bag`, `-jip`; `josyn-commons` →
  `josyn-commons-helpers`, `-identity-helpers`, `-log`, `-schedule`. Each new repo's
  name falls out of the rule mechanically (and already matches today's subfolders).
- **One rename surfaced:** `josyn-jap` → `josyn-jap-contract`.
- **Validated only on contract/library repos so far.** It is *not* yet tested
  against a clean multi-concern repo — `josyn-backend` (idea 0007) and the
  latecomers (idea 0008) are parked, so a later pass may surface naming cases this
  ADR has not seen (e.g. an executable that is not a single library). Such cases, if
  found, are handled by a new amending ADR, not by editing this one.
- **Role-in-name is deferred**, not forbidden: if the platform-manifest ADR later
  wants a role hint in names, it can amend this one. For now names mirror namespaces.
- Naming no longer blocks creating target repos; the next deferred decisions
  (dependency graph, versioning, manifest) can proceed against named repos.
