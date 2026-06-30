# Copilot instructions for josyn-builder

This is a **documentation-only repository**. There is no application code, and no
build, test, or lint tooling — work here is reading and writing plain markdown
under `docs/`. The repo's canonical guidance lives in `AGENTS.md`,
`docs/working-method.md`, and `docs/guide.md`; this file summarizes what an agent
most needs to act correctly.

## What this repo is (and the two-level rule)

`josyn-builder` is a **temporary** migration/consolidation tool. Its job is to
consolidate an existing multi-repo PoC and design a fresh re-start: future repo
structure, working method, architecture, and which existing artifacts to carry
forward. The deliverables are a *set of other, clean repos* — not code in this
repo. When that work is done, this repo disappears.

Never mix the two levels of work:

- **This repo** = the workshop: ideas, decisions (ADRs), and plans that reason
  about the migration.
- **The target platform** = the output: clean, well-documented, future-proof
  repos produced as a result of decisions made here.

Nothing from the old PoC is transferred without a thorough discussion, an ADR,
and documentation. Everything produced must withstand review by future
collaborators (this is currently a one-person project being made
collaboration-ready), so favor thorough ADRs and clear documentation.

## Working method: decision-trail

The repo follows **decision-trail v2.2** (https://github.com/ckluth/decision-trail).
A thought travels: **idea → proposal → decision → plan → execution** across three
independent artifact families.

| Stage | Lives in | Status values |
|-------|----------|---------------|
| idea | `docs/ideas/NNNN-*.md` | `seed` → `promoted` / `dropped` |
| proposal → decision | `docs/decisions/NNNN-*.md` (ADR, same file) | `proposed` → `accepted` / `rejected` |
| plan → execution | `docs/plans/NNNN-*.md` (same file) | `draft` → `active` → `done` / `abandoned` |

- Ideas are cheap; a matured idea is *promoted* to a proposal.
- A proposal *becomes* a decision in place — flip its status, never move the file.
  ADRs use the classic template (Status / Context / Decision / Consequences); add
  Decision Drivers / Considered Options when weighing alternatives.
- A plan `Implements:` an accepted ADR and breaks it into GitHub task-list
  checkboxes (`- [ ]` / `- [x]`). Execution is the plan ticking its boxes.
- **Never edit a decision away.** To change a decision, write a *new* ADR that
  `Amends`/`Supersedes` the old one and link them. The trail is history, not a
  current-state snapshot.

## Conventions that are easy to get wrong

- **Confirmation guard.** Do not rush into writing, editing, or implementing.
  First briefly explain what you intend to do, then wait for explicit approval.
  Discussing and proposing is always fine; acting needs a green light.
- **PoC repos are read-only ([ADR 0004](../docs/decisions/0004-poc-repos-read-only-archive-before-reuse.md)).**
  The sibling `josyn-*` PoC repos under `C:\DevGit` are read-only *sources* — only
  ever read from (extract / copy / re-implement), **never edited in place**, even
  "in the heat of the editing moment." Target repos are rebuilt fresh. On a name
  conflict, the existing repo is **moved into an archive first** (with its `.git`
  intact), then the fresh repo is created — never overwrite or delete a source.
- **Artifact numbers are ordinal only.** Assign the next unused number in that
  family. `ideas/`, `decisions/`, and `plans/` are independent sequences. Never
  derive a number from a related artifact — a plan implementing ADR-0004 is *not*
  `0004`; it takes the next free plan slot. Relationships are expressed only via
  cross-link fields, never matching numbers.
- **Every idea, decision, and plan header carries a `Date:`** (creation date) —
  mandatory.
- **Cross-link vocabulary** (fixed, greppable header fields with relative md links):
  - `Parent:` (idea → idea) — forward-only.
  - `Promoted to:` / `Promoted from:` (idea ↔ ADR) — reciprocal.
  - `Amends:` / `Amended by:` (ADR ↔ ADR) — reciprocal.
  - `Supersedes:` / `Superseded by:` (ADR ↔ ADR) — reciprocal.
  - `Implements:` (plan → ADR) — forward-only.
  - Rule: add the back-link only when *both* ends are single and write-once.
- **`docs/overview.md` is derived.** It is a dated status index regenerated
  *wholesale* from artifact headers — never hand-patched. Regenerate (and update
  the "As of:" stamp) only when the user explicitly asks. Refresh procedure: scan
  each family for the `# N. Title` line and the `- Status:` / `- Date:` header
  fields, then rewrite the three tables.
- **The method is settled.** Use decision-trail; don't casually redesign the
  *method* itself. (Project decisions about the migration are normal work,
  captured as ideas/ADRs/plans.)

## Layout

```
AGENTS.md               repo root — points to the method; carries agent guidance
README.md               what this repo is and why it's temporary
docs/guide.md           narrative introduction (read first)
docs/working-method.md  terse canonical reference for the method
docs/overview.md        derived, dated status index
docs/ideas/             idea artifacts
docs/decisions/         proposal + decision artifacts (ADRs); starts at 0001
docs/plans/             plan + execution artifacts
```

`docs/working-method.md` is the canonical source for the method spec; the root
`AGENTS.md` is a derived rendering — edit the method in `working-method.md`, then
regenerate the other rendering rather than hand-patching it.
