---
title: "Workflow Patterns"
description: "Patterns for structuring multi-phase development workflows"
---

# Workflow Patterns

## Phase Structure

Multi-phase workflows typically follow a pattern:

```
┌─────────────────┐     new_task()     ┌─────────────────┐     new_task()     ┌─────────────────┐
│   ORCHESTRATOR  │ ─────────────────► │      PLAN       │ ─────────────────► │      CODE       │
│                 │                    │                 │                    │                 │
└─────────────────┘                    └─────────────────┘                    └─────────────────┘
```

### Phase 1: Analysis (Orchestrator)

- Load context from project documentation
- Analyze codebase structure and patterns
- Gather requirements through questioning
- Collect and synthesize user responses

### Phase 2: Planning (Architect)

- Receive context from Orchestrator
- Generate comprehensive plan:
  - Clear objective
  - Numbered implementation steps
  - Files to create/modify
  - Context update requirements
  - Risk assessment
- Present plan for user validation
- Iterate on feedback

### Phase 3: Implementation (Code)

- Receive validated plan
- Implement each step systematically
- Follow project conventions
- Update context at completion

## Mode Transitions

All transitions use `new_task()` with explicit context passing:

```markdown
Call new_task() to target mode with:
- Loaded context summary
- User responses
- Original request
- Specific instruction
```

## Validation Requirements

- User validation required before destructive actions
- Plans must be approved before code execution
- Context updates happen after completion

## Context Update

At workflow completion:
- Document new patterns discovered
- Record decisions made
- Update conventions as they evolve
