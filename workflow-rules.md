# Workflow rules — the enforceable guardrails

These are the non-negotiables that make a fleet of coding agents safe to ship with.
Treat each as a checklist item; a violation blocks the pipeline.

## Separation of duties
- [ ] Only **Lead** decomposes work and writes PRs/release notes.
- [ ] Only **Ops** commits, merges, pushes, and deploys.
- [ ] No agent both authors a change and ships it.

## Gates
- [ ] **QA** must approve with **evidence** (a number, a screenshot, a `file:line`) —
      never "looks fine".
- [ ] **Security** is a hard gate: 0 secrets, 0 PII, 0 client brand names before anything
      outward-facing ships. A failure blocks Ops.
- [ ] **Human approval** is required for irreversible/outward-facing actions: creating a
      public repo, pushing, deploying.

## Spec-Driven Development
- [ ] Every task is **atomic** (one concern).
- [ ] Every task has an explicit **verification criterion** written before implementation.
- [ ] Every task **traces** to a plan/phase.
- [ ] Every task closes in an **atomic commit** (Conventional Commits).

## Context discipline
- [ ] Each agent receives only the context its role needs (no conversation inheritance).
- [ ] Skill/tool loading is scoped per role (skill isolation).
- [ ] The coordinator's context is reserved for coordination, not implementation detail.

## Parallelism
- [ ] Only independent tasks run in parallel (several **Coder** instances).
- [ ] Tasks that share state run sequentially, or are serialized behind a gate.
