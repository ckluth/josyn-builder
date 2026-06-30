# 3. Repo continuity: defer the pilot-seat question; do not delete josyn-builder

- Status: accepted
- Date: 2026-06-30
- Amends: [ADR 0002](0002-repo-landscape-poly-repo-principle.md)
- Raised by: [idea 0006](../ideas/0006-repo-becomes-agentic-pilot-seat.md)

## Context

ADR 0002 §3 committed positively that this repo is **temporary** — that
`josyn-builder` is only the migration workshop, dissolves once its work is done,
and explicitly does **not** become the `pilot-seat`; a new, separate seat repo
would be created later.

[Idea 0006](../ideas/0006-repo-becomes-agentic-pilot-seat.md) reopened that: why
maintain a double-existence at all? If this repo simply *is* the agentic
pilot-seat, the migration/exit machinery, the copying of ADRs into a fresh repo,
the re-bootstrapping of decision-trail, and the search for the "right moment" to
abolish the repo all fall away — and the `josyn-builder` name already fits the
`josyn-xxx` convention.

Discussing it surfaced that the apparent dilemma fuses three independent knobs:

1. does the repo **physically persist** (never deleted)?
2. does the repo **carry the role** of pilot-seat?
3. does the repo **die** when migration ends?

Two lenses then separated them:

- **Reversibility.** Nearly all of idea 0006's prize (no copying, no re-learning,
  no death-timing) comes from *not destroying the repo*, not from the label.
  Keeping the repo alive is cheap and reversible; **deletion** is the one
  irreversible act. So the costly mistake is deleting prematurely, not labelling
  wrong today.
- **Permanent vs one-time weight.** The rework costs are one-time and transient;
  content-purity (what a colleague sees in the seat repo for years) is permanent
  and recurring. A durable structural property should not be dictated by a
  one-time cost — *unless* the migration trail is genuine provenance, in which
  case purity is a feature, not a cost. That verdict cannot be made confidently
  until the existing PoC repos are inventoried (plan 0001).

## Decision

We **amend ADR 0002 §3**. Specifically:

1. **Do not delete.** `josyn-builder` persists. It is no longer treated as a
   repo scheduled for dissolution. Premature deletion is off the table.
2. **Defer the role label.** Whether this repo *becomes* the `pilot-seat`
   (taxonomy role per ADR 0002 §2) is an **open, deferred question** — not
   decided here either way.
3. **Resolve after the inventory.** The role question is to be settled by a
   later ADR, once the inventory & classification of the existing PoC repos
   (first task of [plan 0001](../plans/0001-repo-landscape-follow-ups.md)) gives
   real data on what the pilot-seat must do and whether the migration trail reads
   as signal or noise.

ADR 0002's poly-repo principle and four taxonomy roles are **unchanged**; only
§3's "this repo is temporary / does not become the pilot-seat / a separate seat
is created later" claim is downgraded from a commitment to a deferred question.

## Consequences

- The double-existence and exit-strategy framing is paused, not abolished. The
  one-time rework savings idea 0006 identified are preserved by simply keeping
  the repo alive.
- [Idea 0006](../ideas/0006-repo-becomes-agentic-pilot-seat.md)'s full thesis
  ("this repo *is* the permanent pilot-seat") remains **seeded/parked**, to be
  revisited — promoted or dropped — after the inventory.
- `README.md` and `AGENTS.md` still describe the repo as "temporary." That
  framing is left untouched for now: deferral postpones the verdict rather than
  overturning it. It will be revised only when the role question is actually
  decided.
- A future ADR will either: (a) accept idea 0006 and assign this repo the
  `pilot-seat` role (likely also superseding §3 outright and updating
  README/AGENTS), or (b) reaffirm a separate clean seat — at which point the
  question of when, if ever, to retire this repo returns.
