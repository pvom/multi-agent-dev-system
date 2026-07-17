# Case study — applying the model to a production healthcare SaaS (MedTrack)

> Anonymized where it touches anything private. MedTrack is my own public product, so it
> is named; no patient data, credentials, or infra details appear here.

## Context

MedTrack is a healthcare SaaS with real physicians as users. Changes ship to people who
depend on the product working on their phones. That raises the cost of a bad merge — the
exact situation where an undisciplined single agent is dangerous.

## The model in practice

- **Lead** turned each request into atomic SDD tasks with verification criteria, and
  sequenced them into waves.
- **Arq** fixed the interfaces once, so parallel Coders couldn't diverge.
- **Coder ‖** implemented independent tasks in parallel, each leaving a ready work tree.
- **QA** ran the gate — see the companion repo [`agentic-qa-gate`](../agentic-qa-gate),
  which is this QA role made real: a Playwright suite plus a **runtime design-system
  color audit** that blocks regressions static analysis can't catch.
- **Security** scanned for secrets/PII/brand leakage before anything outward-facing.
- **Ops** committed atomically and deployed, with a rollback path.

## What the discipline bought

- **No self-grading**: the agent that wrote a change never also approved and shipped it.
- **Auditable history**: atomic, traceable commits instead of large mixed diffs.
- **A real gate with teeth**: the QA role rejected merges with a concrete
  `X/130 · file:line` verdict, not an opinion.
- **Context stayed small**: role isolation kept each agent on-scope and the coordinator
  free to coordinate.

## Honest scope

This is a **methodology**, and the numbers here describe my own workflow — they are an
operating result, not a benchmark. The transferable claim is the **structure**: role
separation + hard gates + SDD makes agent-built software reviewable and safe to ship. The
[`agentic-qa-gate`](../agentic-qa-gate) repo is the part you can run and verify yourself.
