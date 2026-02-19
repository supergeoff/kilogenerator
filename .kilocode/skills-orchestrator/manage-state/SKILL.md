---
name: manage-state
description: Manages workflow state file (read, write, clear operations). Use this skill to persist and retrieve context across workflow phases.
---

# Skill: Manage State

## Objective

Manage the workflow state file `.kilocode/.develop-state.json` for passing context between workflow phases.

## Input

- **operation**: The operation to perform (read, write, update, clear)
- **key**: The JSON key to read/update (optional for read operations)
- **value**: The value to write (required for write/update operations)

## State File Location

```
.kilocode/.develop-state.json
```

## Operations

### READ
Read the entire state file or a specific key:
- Read entire file: `read_state()` 
- Read specific key: read `phases.orchestrator.contextSummary` etc.

### WRITE / UPDATE `userResponses`

When saving user responses, preserve the FULL context of the questioning:

```json
{
  "phases": {
    "orchestrator": {
      "userResponses": [
        {
          "q": "Q1: [Full Title]",
          "context": "[The specific context provided for this question]",
          "options": ["A", "B", "C"],
          "answer": "[Selected label OR user's free-form text]",
          "raw_response": "[If multiple choices were allowed or additional text provided]"
        }
      ]
    }
  }
}
```

**CRITICAL**: Do NOT summarize the responses into a simplified JSON. Keep the questions and answers verbatim to ensure no context is lost for the Architect phase.

## Operations

### APPEND_RESPONSE
Add a single response to the `userResponses` array while preserving existing ones.

### UPDATE_STATE
Update any key in the state file. If updating `userResponses`, ensure it is an array of objects as defined above.

### CLEAR
Delete the state file after workflow completion:
- Use at end of Phase 3.2 (Context Update)
- Ensures clean state for next workflow run

## Workflow Usage

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

## Rules

1. **Always use JSON format** for state file
2. **Include metadata** with timestamps on every write
3. **Preserve existing data** when updating specific keys
4. **Clear on completion** to avoid stale state
5. **Handle missing file** gracefully (create new if needed)
