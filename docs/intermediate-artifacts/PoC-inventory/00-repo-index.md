# PoC inventory — Pass 1 coarse repo index

- Pass: 1 (a cheap orientation map — a by-product, not the deliverable)
- Scope: `josyn-*` repo family under `C:\DevGit`
- Date: 2026-06-30
- Sources: each repo's `README.md` plus `josyn-platform` (README, `repos/`,
  `decisions/`) — the platform repo is the authoritative architectural reference
  and describes most of the family.

> **Why this exists.** This index is orientation only. The inventory is
> decision-driven: real gathering happens per deferred ADR (see "Next passes").
> The provisional role column is a *by-product* — we are **not** trying to fully
> classify every repo here.
>
> Provisional roles are first-pass guesses against the
> [ADR 0002](../../decisions/0002-repo-landscape-poly-repo-principle.md) taxonomy
> (`artifact` / `concern` / `pilot-seat` / `platform-docs`). A trailing `?` marks
> low confidence. `out-of-scope` means not a platform component (scratch, consumer,
> demo, or this workshop). "Deep dive?" flags repos a later pass should examine
> before its classification is trusted.

## The 17 josyn-\* repos

| Repo | One-line purpose | Primary output | Provisional role | Deep dive? |
|------|------------------|----------------|------------------|------------|
| `josyn-foundation` | Infrastructure primitives — Result pattern, PropertyBag, JIP transport | NuGet packages (`JOSYN.Foundation.*`) | `artifact?` / `concern?` | yes — artifact-vs-concern (infra capability shipped as packages) |
| `josyn-commons` | Domain-agnostic utility helpers, open for growth | NuGet packages (`JOSYN.Commons.*`) | `artifact?` / `concern?` | yes — same artifact-vs-concern question |
| `josyn-jap` | JAP protocol contracts (`JOSYN.Jap.Contract`) | NuGet package | `artifact` | maybe — confirm single shippable |
| `josyn-jrp` | JRP (REST protocol) wire contracts — surface↔gateway (ADR-033) | NuGet packages (launch + surface) | `artifact?` | yes — two packages in one repo vs poly-repo principle |
| `josyn-job-host` | Job execution runtime library linked by every job exe | NuGet library (`JOSYN.JobHost`) | `artifact` | no |
| `josyn-adapter-contracts` | Adapter contract packages (ADR-023) | NuGet packages | `artifact?` | yes — package count / grouping |
| `josyn-backend` | Scheduler & session-orchestration layer | Executable (`JOSYN.Backend.*`) | `artifact` | yes — central, active dev; map deps |
| `josyn-session-broker` | Per-session boundary EXE (ADR-025, ex-JAPServer) | Executable (`JOSYN.SessionBroker`) | `artifact` | maybe |
| `josyn-surface` | Human window into the headless platform (ADR-030/031) | Executable/app | `artifact?` | yes — delivery strategy still evolving |
| `josyn-platform` | Architecture, decisions, cross-cutting docs (45 ADRs) — also *provisional* pilot-seat | Documentation | `platform-docs` (+ pilot-seat, deferred per ADR 0003) | yes — central; harvest source (see deep dive) |
| `josyn-builder` | **This workshop** — consolidate the PoC, design the re-start; temporary | Documentation (decisions) | `out-of-scope` (dissolves when done) | no |
| `josyn-contoso` | Demo company adapter — fake `IConfigSource` (ADR-009) | Sample/demo code | `out-of-scope?` (demo) | maybe — is a demo adapter a platform artifact? |
| `josyn-playground` | Consumer of the platform; explicitly not a platform component | Consumer code | `out-of-scope` | no |
| `josyn-toolbox` | Maintainer/operational tooling (site-builder, deploy scripts) | Tooling (executables/scripts) | `concern?` (tooling) | yes — README says "not a platform component" vs ADR concern role |
| `josyn-docs` | Generated HTML documentation site (build target of toolbox) | Generated HTML (derived) | `platform-docs?` / derived | yes — derived target vs first-class repo |
| `josyn-guide` | HTML guide site (start/index.html, mermaid) | Generated HTML | `platform-docs?` / derived | yes — relation to josyn-docs unclear |
| `josyn-roadmap` | Roadmap / planning notes & prompts | Planning notes | `out-of-scope?` | maybe — planning vs platform-docs |

## Pass 1 observations (to carry into the deferred ADRs)

- **Two clean clusters already visible:** *contract/library NuGet repos*
  (`foundation`, `commons`, `jap`, `jrp`, `job-host`, `adapter-contracts`) vs
  *executable repos* (`backend`, `session-broker`, `surface`). This maps directly
  onto the `artifact` role and will feed the dependency-graph and versioning ADRs.
- **The artifact-vs-concern boundary is the main open classification question.**
  Infra/utility repos (`foundation`, `commons`) ship NuGet packages (reads as
  `artifact`) yet "own a shared capability" (reads as `concern`). ADR 0002's
  tie-breaker (classify by primary output) needs applying per repo.
- **Several "not a platform component" repos** (`playground`, `toolbox`,
  `builder`, `contoso`) sit outside the dependency graph. The taxonomy has no
  explicit "external/consumer" role — worth noting for the naming/manifest ADRs.
- **Documentation is split across three repos** (`platform`, `docs`, `guide`) with
  `docs`/`guide` looking *derived*. ADR 0002 allows exactly one `platform-docs`;
  reconciling this is a real decision.
- **`josyn-jrp` and `josyn-adapter-contracts` each hold multiple packages** — a
  direct test of the strict one-repo-per-artifact principle and its escape hatch.
- **All repos are at `1.0.0-preview01`** today (uniform), which is itself input to
  the versioning/release-strategy ADR.

## Next passes (decision-driven — not done here)

Each pass gathers for the *next* deferred ADR, then stops:

1. **Naming-convention ADR (next, cheapest per plan 0001).** Gather: the actual
   repo names above, `josyn-platform/architecture/naming-conventions.md` +
   `repo-structure-conventions.md`, `ADR-001-platform-naming`, and the naming
   inconsistencies a new scheme must resolve. → this is the first *real*
   deliverable.
2. **Dependency-graph ADR.** Gather: inter-repo references (the layering above) and
   package dependencies.
3. **Versioning ADR.** Gather: current versions (all `1.0.0-preview01`) and any
   lockstep/independent release signals.
4. **Overview/manifest ADR.** Gather: how `docs`/`guide` are derived
   (`docs/docs-index.json`, site-maps) as a model for a platform manifest.

The provisional role column above gets *resolved per repo only if and when* a
decision needs it — not as a standalone exercise.
