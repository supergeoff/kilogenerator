---
title: "Workflow Patterns"
description: "Patterns for structuring multi-phase development workflows"
---

# Workflow Patterns

## Phase Structure

Multi-phase workflows typically follow a pattern:

```
┌─────────────────┐   STOP & VALIDATE   ┌─────────────────┐   STOP & VALIDATE   ┌─────────────────┐   STOP & VALIDATE   ┌──────────────┐
│   ORCHESTRATOR  │ ──────────────────► │      PLAN       │ ──────────────────► │      CODE       │ ──────────────────► │  UPDATE CTX  │
│                 │      User OK        │                 │      User OK        │                 │      User OK        │              │
└─────────────────┘                     └─────────────────┘   + Model Switch    └─────────────────┘                     └──────────────┘

### Phase 1: Analysis (Orchestrator)

- Load context from project documentation
- Analyze codebase structure and patterns
- Gather requirements through **Contextualized Questioning**
- **STOP**: Present gathered info and wait for user "continue"
- Persist full Q&R verbatim to state file

### Phase 2: Planning (Architect)

- Receive full context from Orchestrator
- Generate comprehensive plan
- **STOP**: Present complete plan for user validation
- **USER OPPORTUNITY**: Change model before coding
- Iterate on feedback until approved

### Phase 3: Implementation (Code)

- Receive approved plan
- Implement each step systematically
- Follow project conventions
- **STOP**: Present proposed context updates
- Update context only after explicit approval

## Mandatory Stops & Validation

A workflow must never proceed automatically between major phases. User validation is required at each transition to ensure alignment and allow for model adjustments.

1. **Post-Questioning**: Validate that the agent correctly understood the requirements.
2. **Post-Planning**: Validate the technical approach and switch model if necessary.
3. **Post-Implementation**: Validate what is persisted in the long-term context.

### Phase 1: Analysis (Orchestrator)

- Load context from project documentation
- Analyze codebase structure and patterns
- Gather requirements through questioning
- Collect and synthesize user responses
- **Persist to state file**

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

## State Transmission Pattern

For complex workflows requiring context persistence across phases, use a state file.

### State File Location

```
.kilocode/.develop-state.json
```

### State Structure

```json
{
  "workflow": "develop",
  "phases": {
    "orchestrator": {
      "contextSummary": "...",
      "codebaseAnalysis": "...",
      "userResponses": []
    },
    "architect": {
      "generatedPlan": "...",
      "approvedPlan": "..."
    },
    "code": {
      "implementation": "..."
    }
  },
  "metadata": {
    "created": "ISO timestamp",
    "updated": "ISO timestamp"
  }
}
```

### Phase Operations

| Phase | Operations |
|-------|------------|
| 1.1 Context Loading | WRITE: contextSummary |
| 1.2 Codebase Analysis | WRITE: codebaseAnalysis |
| 1.3 Questioning | READ: context, WRITE: userResponses |
| 1.4 Transition | READ: full state for prompt |
| 2.1 Plan Generation | READ: state, WRITE: generatedPlan |
| 2.2 User Validation | UPDATE: approvedPlan |
| 3.1 Implementation | READ: approvedPlan |
| 3.2 Context Update | CLEAR: delete state file |

### Best Practices

1. **Always read state at phase start** - Don't assume state exists
2. **Include timestamps** - Track when data was last updated
3. **Clear on completion** - Avoid stale state for next workflow run
4. **Handle missing file** - Create new state if needed
5. **Use manage-state skill** - Standardized operations for state management

## Validation Requirements

- User validation required before destructive actions
- Plans must be approved before code execution
- Context updates happen after completion

## Context Update

At workflow completion:
- Document new patterns discovered
- Record decisions made
- Update conventions as they evolve
