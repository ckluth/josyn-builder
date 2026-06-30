# josyn-builder

A temporary migration and consolidation workshop. Its job is to consolidate an
existing multi-repo PoC and design a fresh re-start for the platform — repo
structure, working method, architecture, and which existing artifacts to carry
forward. The deliverables are a set of other, clean repos; when that work is done,
this repo disappears. See [`README.md`](README.md) for the full purpose and the
two-level rule.

## How we work

This project follows **decision-trail** — a generic method for carrying a thought
through its whole life (idea → proposal → decision → plan → execution) in plain
markdown. New here? Start with the guide in [`docs/guide.md`](docs/guide.md). The
terse reference is [`docs/working-method.md`](docs/working-method.md); decision
records live in [`docs/decisions/`](docs/decisions/), starting with
[`0001-adopt-decision-trail.md`](docs/decisions/0001-adopt-decision-trail.md).

Based on decision-trail v2.2 — https://github.com/ckluth/decision-trail

## Agent operating guidance

These rules are for an AI agent working in this repo:

- **Artifact numbers are ordinal only.** When creating an artifact, assign the
  next unused number in that family (`docs/ideas/`, `docs/decisions/`,
  `docs/plans/` are independent sequences). Never derive a number from a related
  artifact — a plan implementing ADR-0004 is not named `0004`; it gets the next
  free plan slot. Relationships are expressed via cross-link fields
  (`Implements:`, `Promoted to:`, etc.), never via matching numbers.
- **The method is settled.** Use decision-trail; don't redesign the *method*
  casually. (Your project's own decisions are normal work — captured as ideas,
  ADRs, and plans under `docs/`.)
- **Confirmation guard.** Never rush into writing, editing, or implementing. First
  briefly explain what you intend to do, then wait for explicit approval.
  Discussing and proposing is always fine — acting requires a green light.
- **Keep `docs/overview.md` current.** It is a derived snapshot, regenerated
  wholesale from the artifact headers (never hand-patched) and stamped "as of
  <date>". Regenerate it — and update the stamp — whenever the user explicitly
  asks. A user may flip a state directly in an artifact; the next regeneration
  reconciles the index.
