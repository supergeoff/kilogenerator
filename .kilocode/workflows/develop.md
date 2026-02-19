---
name: develop
---

# Develop Workflow (Orchestrator → Plan → Code)

You are executing the DEVELOP WORKFLOW. Follow this strict sequence.

**State File**: `.kilocode/.develop-state.json`

## Phase 1: Orchestrator Mode (Current)

### 1.1 Context Loading
- Scan `context/` directory at workspace root
- Read all files present
- If non-existent/empty: note "first run" and proceed
- **SAVE** loaded context summary to state file under `contextSummary`

### 1.2 Codebase Analysis
- Project structure (glob patterns)
- Tech stack detection (package.json, requirements.txt, etc.)
- Existing conventions and patterns
- **SAVE** analysis to state file under `codebaseAnalysis`

### 1.3 Questioning
- **READ** state file to get contextSummary and codebaseAnalysis
- Call the `questioning` skill with this context
- The skill will read the state file and generate contextual questions
- Ask EXACTLY 7 questions using the `Question` tool
- Wait for ALL user responses before proceeding
- **SAVE** full user responses (verbatim) to state file under `userResponses`
- **STOP**: Display a summary of all gathered information
- **VALIDATION**: Ask: "Information gathered. Is this correct and complete? Type 'continue' to move to planning, or provide more details."
- Do NOT proceed to Phase 1.4 without explicit "continue" or "proceed"

### 1.4 Transition to Plan Mode
- **READ** state file and include in the prompt:
  - contextSummary
  - codebaseAnalysis  
  - full userResponses (verbatim)
- Original user request
- Instruction: "Generate a structured implementation plan"
- Call `new_task()` to architect mode

## Phase 2: Plan Mode (Architect)

### 2.1 Plan Generation
- **READ** state file to understand full context
- Produce a structured plan with:
  - **Objective**: Clear, measurable goal
  - **Steps**: Numbered implementation steps
  - **Files**: List of files to create/modify
  - **Context Requirements**: What to update in `context/` after implementation
  - **Risks**: Potential issues and mitigations
- **SAVE** generated plan to state file under `generatedPlan`

### 2.2 User Validation & Model Change
- **PRESENT** the complete, detailed plan
- **STOP OBLIGATOIRE**
- Display the following message:
  """
  ⚠️ **PLAN VALIDATION REQUIRED** ⚠️
  
  Please review the plan above.
  - To approve and start coding: type **'continue'** or **'approved'**
  - To change model for coding: **switch model now**, then type **'continue'**
  - To modify the plan: describe your changes
  """
- Wait for explicit approval
- Incorporate modifications if requested
- **SAVE** approved plan to state file under `approvedPlan`
- Do NOT proceed to Phase 2.3 without validation

### 2.3 Transition to Code Mode
- After validation, call `new_task()` to code mode with:
  - **READ** state file and include in prompt:
    - approvedPlan
    - context update requirements from the plan
- Instruction: "Execute the plan systematically. You MUST call update-context at the end."

## Phase 3: Code Mode

### 3.1 Implementation
- **READ** state file to get approvedPlan
- Execute each step of the validated plan
- Write/modify files as specified
- Follow existing project conventions

### 3.2 Context Update Validation
- At completion, call the `update-context` skill
- **STOP**: Present proposed context updates to the user
- **VALIDATION**: Ask: "I have prepared the following context updates based on what was learned. Approve these changes? (yes/no/modify)"
- Only apply changes after explicit approval
- **DOCUMENT**: Record decisions made and any deviations
- **CLEAR** state file after workflow completion

## State File Structure

```json
{
  "workflow": "develop",
  "phases": {
    "orchestrator": {
      "contextSummary": "...",
      "codebaseAnalysis": "...",
      "userResponses": ["response1", "response2", ...]
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

## Absolute Rules

1. **Always use state file** - Read at each phase start, write after each phase completes
2. **No code in Orchestrator or Plan modes** - only analysis and planning
3. **Exactly 7 questions** with 3 choices + free-form
4. **Explicit validation required** before Code mode
5. **Always update context** at the end of Code mode
6. **Use `new_task()` for all mode transitions**
7. **Clear state file** at end of workflow (Phase 3.2)
