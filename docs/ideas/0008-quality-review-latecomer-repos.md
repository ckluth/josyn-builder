# 8. Quality-review the latecomer repos (josyn-jrp, josyn-surface)

- Status: seed
- Date: 2026-06-30

## The thought

`josyn-jrp` and `josyn-surface` are **latecomers** to the PoC, built with a lot of
unattended AI work and **not yet thoroughly quality-reviewed**. Their structure may
look clean on the surface, but it is not yet trustworthy enough to serve as a
reference case — e.g. for testing the naming convention or for classification.

So they are parked: before anything from these repos is treated as signal (carried
forward, or used to validate a convention), they need a deliberate quality review
to separate sound design from unreviewed AI output.

This is distinct from [idea 0007](0007-untangle-josyn-backend.md) (backend is a
structural melting pot); here the issue is **provenance / review confidence**, not
tangled structure.

When matured, this likely becomes a review task (possibly per-repo), feeding the
"carry forward vs rebuild" decision for each.
