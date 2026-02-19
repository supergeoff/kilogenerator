---
name: update-context
description: Updates the context/ folder after implementation. Activate this skill at the end of each implementation to standardize.
---

# Skill: Update Context

## Objective

Maintain `context/` as the source of truth.

## Input

Received from plan mode:
- Validated plan
- Context update requirements

## Process

1. **ANALYZE**: Read existing `context/` and compare with the current state of the code after implementation.
2. **PROPOSE**: Generate a list of proposed changes (Create, Add, Modify, Delete).
3. **PREVIEW**: Present these changes to the user in a clear format (e.g., Markdown table or list).
4. **VALIDATE**: Wait for user approval: "Approve these context updates? (yes/no/modify)".
5. **APPLY**: Only write to the `context/` directory after explicit approval.

## Rules

1. Read existing `context/`
2. Compare with implemented code
3. Apply requirements received from the plan
4. Context = current state of the code
5. **USER APPROVAL IS MANDATORY** before any write operation to the `context/` directory.
6. Record any deviations from the plan in the documentation.
