# Working method — decision-trail (reference)

> This project works **decision-trail** — carrying a thought through its whole life
> (idea → proposal → decision → plan → execution) in plain markdown.
>
> Based on **decision-trail v2.2** — https://github.com/ckluth/decision-trail

<!--
Sync note — this file is CANONICAL.
This is the single source of truth for the method spec. This repo's `AGENTS.md`
(in the decision-trail repo) is a DERIVED rendering of this file; it is regenerated
wholesale, never hand-patched. The only legitimate differences (deltas) between
the two renderings are:
  - paths: adopters use `docs/`-prefixed families (`docs/ideas/`, `docs/decisions/`,
    `docs/plans/`); the decision-trail repo uses repo-root families;
  - construction-ADR cross-references (ADR-00NN) appear only in the decision-trail
    repo's rendering, not here;
  - the `Based on decision-trail vX.Y` provenance citation is adopter-only (this file);
  - entry-point framing: here `AGENTS.md` points to this file; in the decision-trail
    repo `AGENTS.md` carries the text.
Edit the method here; regenerate the other rendering.
-->

This file is the terse **reference** for *how we work* — the contract, lifecycle,
layout, cross-link vocabulary, and how to start. For a narrative introduction that
teaches the method, read [`guide.md`](guide.md). The repository's root `AGENTS.md`
points here and carries the agent operating guidance. What the project *is* belongs
in its own README.

## The contract — eight promises

1. **Continuity** — pick up cheaply after the session ends.
2. **Economy** — cheap to write, cheap to resume.
3. **Transparency** — plain, human-readable markdown; nothing hidden in a tool.
4. **Lifecycle for thoughts** — idea → proposal → decision → plan → execution.
5. **Agility** — any thread can be refined or overthrown; nothing is locked.
6. **Budding** — one idea can spawn another; the parent-child link is kept.
7. **Genericity** — nothing is bound to a particular project.
8. **Borrow, don't invent** — lean on existing portable standards (ADRs,
   spec-driven stages, agent hand-off files); invent nothing we can borrow.

## The lifecycle

A thought travels **idea → proposal → decision → plan → execution**, across three
artifact families:

| Stage | Where it lives | Status values |
|-------|----------------|---------------|
| idea | `docs/ideas/NNNN-*.md` | `seed` → `promoted` / `dropped` |
| proposal | `docs/decisions/NNNN-*.md` | `proposed` |
| decision | `docs/decisions/NNNN-*.md` (same file) | `accepted` / `rejected` |
| plan | `docs/plans/NNNN-*.md` | `draft` → `active` → `done` / `abandoned` |
| execution | `docs/plans/NNNN-*.md` (same file) | the plan ticking its checkboxes |

- **Ideas** are cheap to write; a matured idea is *promoted* to a proposal.
- **Decisions** are ADRs — a proposal *becomes* a decision in place when accepted.
  Use the classic template (Status / Context / Decision / Consequences); add
  **Decision Drivers** / **Considered Options** when weighing alternatives.
- **Plans** carry an accepted decision into action: the ADR is the spec, the plan
  is the *how*, execution is the plan in motion. Tasks use GitHub task-list
  markdown (`- [ ]` / `- [x]`).

Every idea, decision, and plan carries a `Date:` (creation date) in its header —
**mandatory**. Artifact numbers are **ordinal only**: assign the next unused
number in that family (`docs/ideas/`, `docs/decisions/`, `docs/plans/` are
independent sequences). Never derive a number from a related artifact — a plan
implementing ADR-0004 is not named `0004`; it takes the next free plan slot.
Relationships are expressed via cross-link fields (`Implements:`, `Promoted
to:`, etc.), never via matching numbers. `docs/overview.md` is a derived status index over all three
families: a single dated snapshot of each artifact's name, creation date, and
state. It is **regenerated wholesale from the artifact headers** (never
hand-patched) and stamped "as of <date>". Regenerate it whenever the user
explicitly asks.

  **Refresh procedure:** scan each family for `# N. Title` (line 1) and
  `- Status:` / `- Date:` (header block) → rewrite the three tables in
  `docs/overview.md`. Nothing else is needed.

## Layout

```
AGENTS.md               repo root — points here; carries agent guidance
docs/guide.md           narrative introduction (read this first)
docs/working-method.md  this file — the terse reference
docs/overview.md        derived status index (regenerated dated snapshot)
docs/ideas/             idea artifacts
docs/decisions/         proposal + decision artifacts (ADRs)
docs/plans/             plan + execution artifacts
```

Decision records use `docs/decisions/` — the conventional location for ADRs — so
the structure reads as a normal, well-organized repo, with no project-specific
folders imposed.

## Cross-link vocabulary

Artifacts reference each other with relative markdown links and fixed, greppable
field names in their headers:

| From | Field | To | Meaning |
|------|-------|----|---------|
| idea | `Parent:` | idea | budded from another idea |
| idea | `Promoted to:` / ADR `Promoted from:` | ADR | matured into a proposal (reciprocal) |
| ADR | `Amends:` / `Amended by:` | ADR | part of a decision changed |
| ADR | `Supersedes:` / `Superseded by:` | ADR | one decision replaces another |
| plan | `Implements:` | ADR | carries out a decision |

Forward link always; add the reciprocal back-link for amend/supersede **and
promotion**. A link is reciprocal only when *both* ends are single and write-once
(promotion: one idea ↔ one ADR); `Parent` and `Implements` stay forward-only
because their reverse side accumulates (one parent → many children; one ADR → many
plans).

## How to start working

1. Capture a thought as an idea in `docs/ideas/`.
2. When it matures, open an ADR in `docs/decisions/` with `Status: proposed`.
3. Accept or reject it; an accepted ADR is a decision.
4. Write a `docs/plans/` file that `Implements:` the decision and lists tasks.
5. Execute by moving the plan `active` → `done`, ticking checkboxes.

This repo's own `docs/decisions/0001-adopt-decision-trail.md` records the decision
to adopt decision-trail. Everything else starts from there.
