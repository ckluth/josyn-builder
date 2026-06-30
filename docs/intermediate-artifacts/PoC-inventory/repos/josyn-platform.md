# Deep dive — `josyn-platform`

- Pass: 2 (first targeted deep dive — the central repo)
- Date: 2026-06-30
- Location: `C:\DevGit\josyn-platform`
- Provisional ADR 0002 role: `platform-docs` (and *provisional* pilot-seat — a
  role ADR 0003 defers; the new pilot-seat will be a separate repo, never
  `josyn-builder`).
- Source: repo `README.md` and folder scan; no code (this repo has none).

## What it is

> "This repo is the authoritative architectural reference for the entire JOSYN
> platform. Start here before working in any other repo. No code … just
> documentation: architecture, decisions, and cross-cutting concepts."

It is the hub of the PoC. It carries **two concerns in one home** (its own README
flags this as deliberate-but-provisional):

1. **Architectural reference** — stable, structural. This is the `platform-docs`
   role in ADR 0002 terms.
2. **Agentic pilot-seat** — the single place an AI agent reads before operating in
   any JOSYN repo (coding standards, sanity criteria, agent rules). Explicitly
   provisional; expected to migrate as org-level agent infra matures. ADR 0002's
   `pilot-seat` is exactly this, and ADR 0003 defers committing the seat.

Implication for the migration: when the platform is rebuilt, **these two concerns
should likely split** into a `platform-docs` repo and a separate `pilot-seat`
repo — consistent with ADR 0002's one-concern-per-repo principle.

## Structure (top level)

| Folder | Contents | Inventory value |
|--------|----------|-----------------|
| `decisions/` | **45 ADR files** (ADR-001 … ADR-035, plus B-series sub-ADRs) | The richest harvest source — the PoC's entire decision history |
| `architecture/` | 7 docs: `overview`, `coding-standards`, `naming-conventions`, `repo-structure-conventions`, `storage`, `local-build`, `docs-index-vocabulary` | Directly feeds the naming-convention & manifest ADRs |
| `repos/` | Per-repo overviews (`josyn-backend/`, plus `commons/foundation/jap/job-host/jrp/session-broker`.md) | Coarse per-repo facts already curated upstream |
| `sanity/` | `criteria-review`, `overview`, `triggers`, `README` | Quality/review bar the re-start must meet |
| `solution-architecture/`, `architecture/` | Solution + component architecture | Dependency-graph ADR input |
| `docs/` | `docs-index.json`, site-maps (`site-map.yaml`, `site-map-josyn-guide.yaml`), enrich prompt | Shows how `josyn-docs`/`josyn-guide` are generated |
| `guides/`, `proposals/`, `thinking/` | 2 / 1 / 1 files | Narrative + in-flight thinking |
| `plans/`, `temp/` | Working plans, scratch | Mostly transient |
| `ROADMAP.md`, `MAINTAINERS.md`, `AGENTS.md` | Root governance docs | Governance/agent rules |

## High-value harvest targets (for later passes / ADRs)

- **`architecture/naming-conventions.md` + `repo-structure-conventions.md`** →
  primary input for the **naming-convention ADR** (the cheapest deferred decision,
  tackled next per plan 0001).
- **`decisions/ADR-001-platform-naming.md`** → existing naming rationale to carry
  forward or supersede.
- **`repos/*.md` + `architecture/overview.md` + README dependency diagram** →
  input for the **dependency-graph ADR**.
- **README "all repos at `1.0.0-preview01`"** → input for the **versioning ADR**.
- **`docs/docs-index.json` + site-maps** → input for the **overview/manifest ADR**
  (the platform already derives a docs index; the manifest idea is the same move).

## Key facts established

- The platform proper is a small, layered set: `foundation` → (`commons`, `jap`,
  `jrp`, `job-host`, `adapter-contracts`) → (`backend`, `session-broker`,
  `surface`). IPC is named-pipe with GUID session isolation.
- `josyn-platform` itself ships **no artifact** — pure docs → cleanly
  `platform-docs`, the one ambiguity being the bundled pilot-seat concern.
- Decision density is high (45 ADRs). Any "carry forward vs re-decide" judgement in
  `josyn-builder` should consult the relevant upstream ADR first.

## Open questions raised by this deep dive

1. Split `platform-docs` from `pilot-seat`? (ADR 0002 says one concern per repo;
   ADR 0003 defers the seat.)
2. Are `josyn-docs` and `josyn-guide` *derived outputs* of `josyn-platform` +
   `josyn-toolbox`, and therefore not first-class repos under ADR 0002?
3. How much of the 45-ADR history is carried forward vs re-decided fresh in the
   re-start? (Needs a deliberate policy — itself a candidate ADR in `josyn-builder`.)
