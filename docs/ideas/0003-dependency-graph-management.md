# 3. Dependency-graph management

- Status: seed
- Date: 2026-06-30
- Raised by: [ADR 0002](../decisions/0002-repo-landscape-poly-repo-principle.md)

## The thought

A deferred decision called for by ADR 0002. Many strictly-separated repos imply a
non-trivial inter-repo dependency graph. We need a deliberate approach to
declaring, viewing, and constraining dependencies between repos so the graph stays
comprehensible and acyclic.

When this matures, promote it to its own ADR.
