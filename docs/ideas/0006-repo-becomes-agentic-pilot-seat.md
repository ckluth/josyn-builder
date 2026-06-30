# 6. This repo becomes the agentic pilot-seat

- Status: seed
- Date: 2026-06-30
- Discussed in: [ADR 0003](../decisions/0003-repo-continuity-defer-pilot-seat.md)

## The thought

Despite the currently open, seeded ideas and the active plan, this idea wants to
be discussed *first* — because it changes the premise the others rest on.

Should we change the character of this repo from now on? Instead of being a
*temporary* migration/consolidation workshop that disappears when its work is
done, this repo **"will be"** the **agentic pilot-seat** mentioned in
[idea 0001](0001-repo-landscape-structuring.md) (the one single repo as the only
agentic pilot-seat).

If we accept that, the double-existence dissolves and several burdens fall away:

- No migration- and exit-strategy is needed — there is no second repo to hand off
  to.
- No future copying of ADRs into a fresh repo.
- No rebuilding and re-learning the decision-trail method elsewhere.
- No need to find the "right moment" to abolish this repo.

The name `josyn-builder` would already be fine, because `josyn-xxx` "will be" the
naming convention for all other repos (see
[idea 0005](0005-repo-naming-convention.md)).

## Why it might matter / open tensions

- This collides with the repo's stated **two-level rule** and its self-described
  *temporary* nature (README, `AGENTS.md`). Accepting it would mean rewriting that
  framing — a significant shift, not a casual edit.
- It reframes the active plan and the other seeded ideas, which currently assume a
  builder → target-platform separation. Their scope and wording would need review.
- Tension to weigh: does collapsing the two levels lose the clarity the
  separation was meant to protect (workshop reasoning vs. clean output), or does
  it simply remove ceremony that never paid for itself?

When this matures, promote it to its own ADR.
