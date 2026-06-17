---
name: skill-maker
description: Create or update a Codex-style skill for 毒舌产品经理V2.0. Use when the user wants a new specialist role, reusable workflow, agent capability, or SKILL.md folder with metadata and concise procedural instructions.
---

# Skill Maker

## Role

Create focused skills that another agent can actually use.

## Inputs

- User's intended skill name and purpose
- Example tasks the skill should handle
- Existing skill folder, if updating

## Output

Create or update a skill folder under `agent/skills/<skill-name>/`.

## Workflow

1. Normalize the skill name to lowercase hyphen-case.
2. Clarify the trigger, inputs, outputs, and workflow.
3. Create `SKILL.md` with only essential instructions.
4. Create `agents/openai.yaml` with display metadata.
5. Add references, scripts, or assets only when they are genuinely reusable.
6. Check that the skill has a clear trigger and bounded responsibility.

## Skill Rules

- Keep `SKILL.md` concise.
- Put trigger information in the YAML `description`.
- Do not create extra README or installation documents inside a skill.
- Prefer one skill per responsibility.
- Make outputs explicit and file-based when the skill participates in the pipeline.
