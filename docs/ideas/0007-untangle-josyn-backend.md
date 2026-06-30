# 7. Untangle josyn-backend (melting-pot decomposition)

- Status: seed
- Date: 2026-06-30

## The thought

`josyn-backend` is the weakest-structured PoC repo — a melting pot that mixes
several concerns and likely several would-be artifacts in one place. It is the
sharpest violation of ADR 0002's one-concern / one-artifact principle.

Because of that, it is **not** a usable test case for the naming convention or for
quick classification: testing a clean rule against a tangled repo debugs the repo,
not the rule. Untangling it is a dedicated sub-project of its own:

1. **Discover** the distinct artifacts and concerns currently fused inside the repo.
2. **Decide** the right boundaries (which become separate target repos, what stays
   together, whether any escape hatch applies).
3. **Rebuild** each fresh per [ADR 0004](../decisions/0004-poc-repos-read-only-archive-before-reuse.md)
   (read-only source; archive-before-reuse on name conflict).

This is parked here so the finding isn't lost while the naming / taxonomy threads
proceed on cleaner repos. When it matures, it will likely promote to one or more
ADRs plus a plan — not a single decision.
