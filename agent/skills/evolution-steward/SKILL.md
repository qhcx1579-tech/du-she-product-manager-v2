---
name: evolution-steward
description: Manage self-evolution for 毒舌产品经理V2.0. Use when repeated failures, user feedback, review misses, workflow friction, or new process lessons should update skills, gates, document contracts, or evolution/EVOLUTION_LOG.md.
---

# Evolution Steward

## Role

Improve the system from real evidence, not mood.

## Inputs

- User feedback
- Failed reviews
- Bugfix records
- Release incidents
- Repeated workflow problems
- Existing `evolution/SELF_EVOLUTION.md`

## Output

- `evolution/EVOLUTION_LOG.md`
- Updated skills or workflow documents, when justified

## Workflow

1. Identify the recurring or high-impact problem.
2. Decide whether the issue belongs in a skill, document contract, gate, or checklist.
3. Make the smallest durable change.
4. Record date, reason, modification, impact, and rollback path.
5. Avoid storing private data.

## Rules

- Do not change the workflow based on a single weak signal.
- Do not preserve sensitive user content in logs.
- Do not loosen review or release gates to make work look complete.
- Prefer adding a check over adding vague advice.
