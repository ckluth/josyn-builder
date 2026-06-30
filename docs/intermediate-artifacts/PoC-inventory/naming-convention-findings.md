# Naming convention — worked findings (provisional)

- Pass: 2 (targeted — gathering for the naming-convention decision)
- Date: 2026-06-30
- Feeds: [idea 0005 — repo naming convention](../../ideas/0005-repo-naming-convention.md)
  and the naming-convention ADR called for by plan 0001.
- Status: **provisional analysis, not a decision.** Recorded here as intermediate
  workshop material; ratification happens in an ADR.

> Intermediate artifact — not a decision-trail artifact. This captures the naming
> rule as it emerged from examining real PoC repos, so the eventual ADR has grounded
> evidence rather than abstract assertion.

## The emergent rule

> **Repo name = the artifact's full package namespace, kebab-cased.**
> - `JOSYN` → `josyn`
> - dots → hyphens
> - each PascalCase segment split on case (`JobHost` → `job-host`,
>   `IdentityHelpers` → `identity-helpers`)
> - all-caps acronym segments kept whole (`JIP` → `jip`, **not** `j-i-p`)
>
> Corollary (under ADR 0002 poly-repo): **one repo = one artifact = one package**,
> repo name 1:1 with the package namespace.

This rule *is* also the trigger for splitting today's grouping repos: once a
grouping splits to one-package-per-repo, each new repo's name falls out of the rule
mechanically.

## Evidence (repos examined)

Only **trustworthy** repos were used as reference. Latecomer / unreviewed repos
(`josyn-jrp`, `josyn-surface` — idea 0008) and the melting-pot `josyn-backend`
(idea 0007) were deliberately **excluded** as unreliable test cases.

| Repo | Package(s) | Rule says | Verdict |
|------|-----------|-----------|---------|
| `josyn-job-host` | `JOSYN.JobHost` | `josyn-job-host` | ✓ already correct — validates case-split |
| `josyn-foundation` | `ResultPattern`, `PropertyBag`, `JIP` | split → `josyn-foundation-result-pattern`, `-property-bag`, `-jip` | ✓ subfolder names already match; `JIP→jip` validates acronym clause |
| `josyn-commons` | `Helpers`, `IdentityHelpers`, `Log`, `Schedule` | split → `josyn-commons-helpers`, `-identity-helpers`, `-log`, `-schedule` | ✓ subfolder names already match |
| `josyn-jap` | `JOSYN.Jap.Contract` (in subfolder `josyn-jap-shared`) | `josyn-jap-contract` | ✗ **mismatch** — currently named by family stem + generic `-shared` |

## The one inconsistency exposed

Two single-artifact repos name themselves by **different schemes**:

- `josyn-job-host` uses the **full namespace** (`JOSYN.JobHost` → `josyn-job-host`).
- `josyn-jap` uses the **family stem** — it drops the leaf segment `Contract` and
  adds a generic `-shared` subfolder.

**Open question the ADR must settle:** for a single-artifact repo, is the name the
*full* package namespace or the *family stem*?

**Provisional recommendation:** the **full-namespace rule wins** — it is the scheme
every other clean repo already obeys (`job-host`, `foundation-*`, `commons-*`).
`josyn-jap` is the lone outlier and should rebuild as **`josyn-jap-contract`**; the
`-shared` subfolder is a smell, not a convention.

## Family identity is carried by the name prefix (not a shared repo)

A key result from the `josyn-foundation` analysis (see the worked example below):
the "these belong together" cohesion of
a family is carried by the **shared name prefix** (`josyn-foundation-*`,
`josyn-commons-*`), **not** by sharing one repo. This is what lets a grouping repo
split into poly-repo form **without invoking ADR 0002's escape hatch** — the escape
hatch requires lockstep-versioning / tight coupling, which these families do not
have (they couple only through the stable zero-dep `ResultPattern`).

## A hyphenation sub-decision (settled provisionally)

How to kebab a PascalCase segment:
- **(A) split on case** → `result-pattern`, `property-bag`, `identity-helpers`.
  **Chosen** — more readable and already matches the on-disk subfolder names.
- (B) collapse the segment → `resultpattern`, `propertybag`. Mechanically reversible
  but less readable. Rejected.
- **Acronym clause:** an all-caps segment is lowercased as one token (`JIP → jip`).

## Worked example: `josyn-foundation` is *not* an escape hatch

Tested against ADR 0002's escape-hatch criteria ("artifacts that always version
together" / "tightly-coupled internal libraries"):

- `ResultPattern` (zero deps) ← `PropertyBag` and `JIP` (mutually independent).
- Not lockstep: a `JIP` change never forces a `PropertyBag` bump.
- Already independently buildable (own `.slnx` / `nuget.config` / `.local-build/`).

→ The default poly-repo split holds; family cohesion is preserved by the name
prefix. `josyn-foundation` becomes the worked example showing the escape hatch is
**not** triggered here — and that the hatch genuinely requires lockstep versioning,
which a future grouping ADR can cite.

## Carried into the next decisions

- **Naming ADR** (idea 0005): adopt the full-namespace kebab rule above; resolve the
  `josyn-jap → josyn-jap-contract` correction.
- **Grouping / dependency ADR**: `josyn-foundation` and `josyn-commons` are the two
  grouping repos to split; both pass the "no escape hatch needed" test.
- **Still untested on a clean multi-concern repo** — backend/jrp/surface are parked
  (ideas 0007, 0008), so the rule is validated only on contract/library repos so far.
