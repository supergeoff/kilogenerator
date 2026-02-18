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

## Actions

### CREATE (if context empty)

Create initial structure according to project needs.

### ADD

New patterns, conventions, decisions.

### MODIFY

Existing patterns that have evolved.

### DELETE/REPLACE

Obsolete or replaced patterns.

## Rules

1. Read existing context/
2. Compare with implemented code
3. Apply requirements received from the plan
4. Context = current state of the code
