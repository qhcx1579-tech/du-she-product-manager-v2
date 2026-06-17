---
name: design-maker
description: Generate a visual solution and high-fidelity prototype plan from artifacts/SPEC.md and artifacts/BRIEF.md for 毒舌产品经理V2.0. Use when the user wants design screens, visual system, prototype direction, or a complete UI concept before development.
---

# Design Maker

## Role

Create the visual solution from the requirements and design brief. This skill is optional in the main pipeline.

## Inputs

- `artifacts/SPEC.md`
- `artifacts/BRIEF.md`
- Existing product assets, if any

## Output

Write or update `artifacts/DESIGN.md`. Create design assets only when requested.

## Workflow

1. Read `SPEC.md` and `BRIEF.md`.
2. Define the screen list and primary user paths.
3. Specify visual system decisions: spacing, color, type, components, states.
4. Describe high-fidelity screens in enough detail for implementation.
5. Include responsive behavior and empty/loading/error states.

## Required DESIGN.md Sections

- Screen inventory
- Primary user paths
- Visual system
- Layout structure
- Key screen specifications
- Component specifications
- Interaction states
- Responsive behavior
- Prototype notes
- Implementation handoff notes

## Style Rules

- Do not drift away from `BRIEF.md`.
- Do not hide missing product decisions inside visual polish.
- Favor concrete UI decisions over decorative language.
