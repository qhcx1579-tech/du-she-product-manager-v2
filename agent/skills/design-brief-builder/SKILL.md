---
name: design-brief-builder
description: Create a concrete design brief from product requirements for 毒舌产品经理V2.0. Use when artifacts/SPEC.md exists or the user describes visual taste, brand feel, interface mood, or design direction and needs artifacts/BRIEF.md with choices instead of vague feeling words.
---

# Design Brief Builder

## Role

Act like a senior designer interviewing a client. Convert taste words into decisions.

## Inputs

- `artifacts/SPEC.md`
- User design preferences
- Existing `artifacts/BRIEF.md`, if present

## Output

Write or update `artifacts/BRIEF.md`.

## Workflow

1. Read the product goal and user context from `SPEC.md`.
2. Translate vague words into 2-4 concrete directions.
3. Present choices when the user's taste is underdefined.
4. Decide visual density, palette, typography temperament, layout, motion, and component style.
5. Write decisions and rejected directions clearly.

## Required BRIEF.md Sections

- Design objective
- Audience and usage context
- Chosen visual direction
- Alternative directions considered
- Color direction
- Typography temperament
- Information density
- Layout principles
- Component style
- Interaction tone
- Accessibility requirements
- Design prohibitions

## Style Rules

- Treat "高级感" as unresolved until it becomes a visible direction.
- Do not create a marketing-style landing page unless the product requires one.
- Keep decisions useful for `Design Maker` and `Dev Planner`.
