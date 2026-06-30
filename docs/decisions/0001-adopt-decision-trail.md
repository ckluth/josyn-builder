# 1. Adopt decision-trail

- Status: accepted
- Date: 2026-06-30

## Context

This project needs a reasonable, structured, reproducible, economic way to work
that survives the end of a session and keeps its reasoning in plain markdown.

`decision-trail` is a generic, borrowed-standards method that provides exactly this: a
lifecycle (idea → proposal → decision → plan → execution) across three artifact
families, described in [`docs/working-method.md`](../working-method.md).

## Decision

This project adopts **decision-trail at version v2.2** (see
https://github.com/ckluth/decision-trail and its `CHANGELOG.md`).

- We work the lifecycle in `docs/ideas/`, `docs/decisions/`, `docs/plans/` as
  described in `docs/working-method.md`.
- This project's ADR log starts here, at 0001, and is independent of
  decision-trail's own construction history.

## Consequences

- Every later decision in this project is recorded as an ADR in `decisions/`,
  numbered from 0002 onward.
- To take a newer version of decision-trail, re-copy its `starter/docs/working-method.md`
  (and note the change in a new ADR), since the method text is copied, not
  referenced.
